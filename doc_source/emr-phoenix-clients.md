# Phoenix Clients<a name="emr-phoenix-clients"></a>

You connect to Phoenix using either a JDBC client built with full dependencies or using the "thin client" that uses the Phoenix Query Server and can only be run on a master node of a cluster \(e\.g\. by using an SQL client, a step, command line, SSH port forwarding, etc\.\)\. When using the "fat" JDBC client, it still needs to have access to all nodes of the cluster because it connects to HBase services directly\. The "thin" Phoenix client only needs access to the Phoenix Query Server at a default port 8765\. There are several [scripts](https://github.com/apache/phoenix/tree/master/bin) within Phoenix that use these clients\. 

**Use an Amazon EMR step to query using Phoenix**

The following procedure restores a snapshot from HBase and uses that data to run a Phoenix query\. You can extend this example or create a new script that leverages Phoenix's clients to suit your needs\. 

1. Create a cluster with Phoenix installed, using the following command:

   ```
   aws emr create-cluster --name "Cluster with Phoenix" --log-uri s3://myBucket/myLogFolder --release-label emr-5.29.0 \
   --applications Name=Phoenix Name=HBase --ec2-attributes KeyName=myKey \
   --instance-type m5.xlarge --instance-count 3 --use-default-roles
   ```

1. Create then upload the following files to Amazon S3:

   copySnapshot\.sh

   ```
   sudo su hbase -s /bin/sh -c 'hbase snapshot export \
    -D hbase.rootdir=s3://us-east-1.elasticmapreduce.samples/hbase-demo-customer-data/snapshot/ \
   -snapshot customer_snapshot1 \
   -copy-to hdfs://masterDNSName:8020/user/hbase \
   -mappers 2 -chuser hbase -chmod 700'
   ```

   runQuery\.sh

   ```
   aws s3 cp s3://myBucket/phoenixQuery.sql /home/hadoop/
   /usr/lib/phoenix/bin/sqlline-thin.py http://localhost:8765 /home/hadoop/phoenixQuery.sql
   ```

   phoenixQuery\.sql

   ```
   CREATE VIEW "customer" (
   pk VARCHAR PRIMARY KEY, 
   "address"."state" VARCHAR,
   "address"."street" VARCHAR,
   "address"."city" VARCHAR,
   "address"."zip" VARCHAR,
   "cc"."number" VARCHAR,
   "cc"."expire" VARCHAR,
   "cc"."type" VARCHAR,
   "contact"."phone" VARCHAR);
   
   CREATE INDEX my_index ON "customer" ("customer"."state") INCLUDE("PK", "customer"."city", "customer"."expire", "customer"."type");
   
   SELECT "customer"."type" AS credit_card_type, count(*) AS num_customers FROM "customer" WHERE "customer"."state" = 'CA' GROUP BY "customer"."type";
   ```

   Use the AWS CLI to submit the files to the S3 bucket:

   ```
   aws s3 cp copySnapshot.sh s3://myBucket/
   aws s3 cp runQuery.sh s3://myBucket/
   aws s3 cp phoenixQuery.sql s3://myBucket/
   ```

1. Create a table using the following step submitted to the cluster that you created in Step 1:

   createTable\.json

   ```
   [
     {
       "Name": "Create HBase Table",
       "Args": ["bash", "-c", "echo $'create \"customer\",\"address\",\"cc\",\"contact\"' | hbase shell"],
       "Jar": "command-runner.jar",
       "ActionOnFailure": "CONTINUE",
       "Type": "CUSTOM_JAR"
     }
   ]
   ```

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
   --steps file://./createTable.json
   ```

1. Use `script-runner.jar` to run the `copySnapshot.sh` script that you previously uploaded to your S3 bucket:

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
   --steps Type=CUSTOM_JAR,Name="HBase Copy Snapshot",ActionOnFailure=CONTINUE,\
   Jar=s3://region.elasticmapreduce/libs/script-runner/script-runner.jar,Args=["s3://myBucket/copySnapshot.sh"]
   ```

   This runs a MapReduce job to copy your snapshot data to the cluster HDFS\.

1. Restore the snapshot that you copied to the cluster using the following step:

   restoreSnapshot\.json

   ```
   [
     {
       "Name": "restore",
       "Args": ["bash", "-c", "echo $'disable \"customer\"; restore_snapshot \"customer_snapshot1\"; enable \"customer\"' | hbase shell"],
       "Jar": "command-runner.jar",
       "ActionOnFailure": "CONTINUE",
       "Type": "CUSTOM_JAR"
     }
   ]
   ```

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
   --steps file://./restoreSnapshot.json
   ```

1. Use `script-runner.jar` to run the `runQuery.sh` script that you previously uploaded to your S3 bucket:

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
   --steps Type=CUSTOM_JAR,Name="Phoenix Run Query",ActionOnFailure=CONTINUE,\
   Jar=s3://region.elasticmapreduce/libs/script-runner/script-runner.jar,Args=["s3://myBucket/runQuery.sh"]
   ```

   The query runs and returns the results to the step's `stdout`\. It may take a few minutes for this step to complete\.

1. Inspect the results of the step's `stdout` at the log URI that you used when you created the cluster in Step 1\. The results should look like the following:

   ```
   +------------------------------------------+-----------------------------------+
   |             CREDIT_CARD_TYPE             |              NUM_CUSTOMERS        |
   +------------------------------------------+-----------------------------------+
   | american_express                         | 5728                              |
   | dankort                                  | 5782                              |
   | diners_club                              | 5795                              |
   | discover                                 | 5715                              |
   | forbrugsforeningen                       | 5691                              |
   | jcb                                      | 5762                              |
   | laser                                    | 5769                              |
   | maestro                                  | 5816                              |
   | mastercard                               | 5697                              |
   | solo                                     | 5586                              |
   | switch                                   | 5781                              |
   | visa                                     | 5659                              |
   +------------------------------------------+-----------------------------------+
   ```