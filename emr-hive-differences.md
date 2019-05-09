# Differences and Considerations for Hive on Amazon EMR<a name="emr-hive-differences"></a>

## Differences between Apache Hive on Amazon EMR and Apache Hive<a name="emr-hive-apache-diff"></a>

This section describes the differences between Hive on Amazon EMR and the default versions of Hive available at [http://svn\.apache\.org/viewvc/hive/branches/](http://svn.apache.org/viewvc/hive/branches/)\. 

### Hive Authorization<a name="emr-hive-authorization"></a>

 Amazon EMR supports [Hive Authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) for HDFS but not for EMRFS and Amazon S3\. Amazon EMR clusters run with authorization disabled by default\.

### Hive File Merge Behavior with Amazon S3<a name="emr-hive-filemerge"></a>

Apache Hive merges small files at the end of a map\-only job if `hive.merge.mapfiles` is true and the merge is triggered only if the average output size of the job is less than the `hive.merge.smallfiles.avgsize` setting\. Amazon EMR Hive has exactly the same behavior if the final output path is in HDFS\. If the output path is in Amazon S3, the `hive.merge.smallfiles.avgsize` parameter is ignored\. In that situation, the merge task is always triggered if `hive.merge.mapfiles` is set to `true`\.

### ACID Transactions and Amazon S3<a name="emr-hive-acid"></a>

ACID \(Atomicity, Consistency, Isolation, Durability\) transactions are not supported with Hive data stored in Amazon S3\. Trying to create a transactional table in Amazon S3 causes an exception\. 

### Hive Live Long and Process \(LLAP\)<a name="emr-hive-LLAP"></a>

[LLAP functionality](https://cwiki.apache.org/confluence/display/Hive/LLAP) added in version 2\.0 of default Apache Hive is not supported in Hive 2\.1\.0 on Amazon EMR release 5\.0\.

## Differences in Hive Between Amazon EMR Release Version 4\.x and 5\.x<a name="emr-hive-diff"></a>

This section covers differences to consider before you migrate a Hive implementation from Hive version 1\.0\.0 on Amazon EMR release 4\.x to Hive 2\.x on Amazon EMR release 5\.x\.

### Operational Differences and Considerations<a name="emr-hive-diffs-ops"></a>
+ **Support added for [ACID \(Atomicity, Consistency, Isolation, and Durability\)transactions](https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions):** This difference between Hive 1\.0\.0 on Amazon EMR 4\.x and default Apache Hive has been eliminated\.
+ **Direct writes to Amazon S3 eliminated:** This difference between Hive 1\.0\.0 on Amazon EMR and the default Apache Hive has been eliminated\. Hive 2\.1\.0 on Amazon EMR release 5\.x now creates, reads from, and writes to temporary files stored in Amazon S3\. As a result, to read from and write to the same table you no longer have to create a temporary table in the cluster's local HDFS file system as a workaround\. If you use versioned buckets, be sure to manage these temporary files as described below\.
+ **Manage temp files when using Amazon S3 versioned buckets:** When you run Hive queries where the destination of generated data is Amazon S3, many temporary files and directories are created\. This is new behavior as described earlier\. If you use versioned S3 buckets, these temp files clutter Amazon S3 and incur cost if they're not deleted\. Adjust your lifecycle rules so that data with a `/_tmp` prefix is deleted after a short period, such as five days\. See [Specifying a Lifecycle Configuration](https://docs.aws.amazon.com/AmazonS3/latest/dev/how-to-set-lifecycle-configuration-intro.html) for more information\.
+ **Log4j updated to log4j 2:** If you use log4j, you may need to change your logging configuration because of this upgrade\. See [Apache log4j 2](http://logging.apache.org/log4j/2.x/) for details\.

### Performance differences and considerations<a name="emr-hive-diffs-perf"></a>
+ **Performance differences with Tez:** With Amazon EMR release 5\.x , Tez is the default execution engine for Hive instead of MapReduce\. Tez provides improved performance for most workflows\.
+ **ORC file performance:** Query performance may be slower than expected for ORC files\.
+ **Tables with many partitions:** Queries that generate a large number of dynamic partitions may fail, and queries that select from tables with many partitions may take longer than expected to execute\. For example, a select from 100,000 partitions may take 10 minutes or more\.

## Additional Features of Hive on Amazon EMR<a name="emr-hive-additional-features"></a>

Amazon EMR extends Hive with new features that support Hive integration with other AWS services, such as the ability to read from and write to Amazon Simple Storage Service \(Amazon S3\) and DynamoDB\.

### Variables in Hive<a name="emr-hive-variables"></a>

 You can include variables in your scripts by using the dollar sign and curly braces\. 

```
add jar ${LIB}/jsonserde.jar
```

 You pass the values of these variables to Hive on the command line using the `-d` parameter, as in the following example: 

```
-d LIB=s3://elasticmapreduce/samples/hive-ads/lib
```

 You can also pass the values into steps that execute Hive scripts\. 

**To pass variable values into Hive steps using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**\.

1. In the **Steps** section, for **Add Step**, choose **Hive Program** from the list and **Configure and add**\.

1.  In the **Add Step** dialog, specify the parameters using the following table as a guide, and then choose **Add**\.     
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive-differences.html)

1. Select values as necessary and choose **Create cluster**\.

**To pass variable values into Hive steps using the AWS CLI**

To pass variable values into Hive steps using the AWS CLI, use the `--steps` parameter and include an arguments list\.
+ 
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --name "Test cluster" --release-label emr-5.23.0 \
  --applications Name=Hive Name=Pig --use-default-roles --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 \
  --steps Type=Hive,Name="Hive Program",ActionOnFailure=CONTINUE,Args=[-f,s3://elasticmapreduce/samples/hive-ads/libs/response-time-stats.q,-d,INPUT=s3://elasticmapreduce/samples/hive-ads/tables,-d,OUTPUT=s3://mybucket/hive-ads/output/,-d,SAMPLE=s3://elasticmapreduce/samples/hive-ads/]
  ```

  For more information on using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.

**To pass variable values into Hive steps using the Java SDK**
+ The following example demonstrates how to pass variables into steps using the SDK\. For more information, see [Class StepFactory](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/elasticmapreduce/util/StepFactory.html) in the *AWS SDK for Java API Reference*\. 

  ```
  StepFactory stepFactory = new StepFactory();
  
     StepConfig runHive = new StepConfig()
       .withName("Run Hive Script")
       .withActionOnFailure("TERMINATE_JOB_FLOW")
       .withHadoopJarStep(stepFactory.newRunHiveScriptStep(“s3://mybucket/script.q”,
        Lists.newArrayList(“-d”,”LIB= s3://elasticmapreduce/samples/hive-ads/lib”));
  ```

### Amazon EMR Hive Queries to Accommodate Partial DynamoDB Schemas<a name="emr-hive-partial-schema"></a>

Amazon EMR Hive provides maximum flexibility when querying DynamoDB tables by allowing you to specify a subset of columns on which you can filter data, rather than requiring your query to include all columns\. This partial schema query technique is effective when you have a sparse database schema and want to filter records based on a few columns, such as filtering on time stamps\. 

 The following example shows how to use a Hive query to: 
+ Create a DynamoDB table\.
+ Select a subset of items \(rows\) in DynamoDB and further narrow the data to certain columns\.
+ Copy the resulting data to Amazon S3\. 

```
DROP TABLE dynamodb; 
DROP TABLE s3;

CREATE EXTERNAL TABLE dynamodb(hashKey STRING, recordTimeStamp BIGINT, fullColumn map<String, String>)
    STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
    TBLPROPERTIES ( 
     "dynamodb.table.name" = "myTable",
     "dynamodb.throughput.read.percent" = ".1000", 
     "dynamodb.column.mapping" = "hashKey:HashKey,recordTimeStamp:RangeKey"); 

CREATE EXTERNAL TABLE s3(map<String, String>)
     ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
     LOCATION 's3://bucketname/path/subpath/';

INSERT OVERWRITE TABLE s3 SELECT item fullColumn FROM dynamodb WHERE recordTimeStamp < "2012-01-01";
```

The following table shows the query syntax for selecting any combination of items from DynamoDB\.


| Query example | Result description | 
| --- | --- | 
| SELECT \* FROM table\_name; | Selects all items \(rows\) from a given table and includes data from all columns available for those items\. | 
| SELECT \* FROM table\_name WHERE field\_name =value; | Selects some items \(rows\) from a given table and includes data from all columns available for those items\. | 
| SELECT column1\_name, column2\_name, column3\_name FROM table\_name; | Selects all items \(rows\) from a given table and includes data from some columns available for those items\. | 
| SELECT column1\_name, column2\_name, column3\_name FROM table\_name WHERE field\_name =value; | Selects some items \(rows\) from a given table and includes data from some columns available for those items\. | 

### Copy Data Between DynamoDB Tables in Different AWS Regions<a name="emr-hive-cross-region-ddb-copy"></a>

Amazon EMR Hive provides a `dynamodb.region` property you can set per DynamoDB table\. When `dynamodb.region` is set differently on two tables, any data you copy between the tables automatically occurs between the specified regions\.

 The following example shows you how to create a DynamoDB table with a Hive script that sets the `dynamodb.region` property:

**Note**  
Per\-table region properties override the global Hive properties\.

```
CREATE EXTERNAL TABLE dynamodb(hashKey STRING, recordTimeStamp BIGINT, map<String, String> fullColumn)
    STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
    TBLPROPERTIES ( 
     "dynamodb.table.name" = "myTable",
     "dynamodb.region" = "eu-west-1", 
     "dynamodb.throughput.read.percent" = ".1000", 
     "dynamodb.column.mapping" = "hashKey:HashKey,recordTimeStamp:RangeKey");
```

### Set DynamoDB Throughput Values Per Table<a name="emr-hive-set-ddb-throughput"></a>

Amazon EMR Hive enables you to set the DynamoDB readThroughputPercent and writeThroughputPercent settings on a per table basis in the table definition\. The following Amazon EMR Hive script shows how to set the throughput values\. For more information about DynamoDB throughput values, see [Specifying Read and Write Requirements for Tables](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithDDTables.html#ProvisionedThroughput)\. 

```
CREATE EXTERNAL TABLE dynamodb(hashKey STRING, recordTimeStamp BIGINT, map<String, String> fullColumn)
    STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
    TBLPROPERTIES ( 
     "dynamodb.table.name" = "myTable",
     "dynamodb.throughput.read.percent" = ".4",
     "dynamodb.throughput.write.percent" = "1.0",
     "dynamodb.column.mapping" = "hashKey:HashKey,recordTimeStamp:RangeKey");
```