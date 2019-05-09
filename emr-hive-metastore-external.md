# Using an External MySQL Database or Amazon Aurora<a name="emr-hive-metastore-external"></a>

To use an external MySQL database or Amazon Aurora as your Hive metastore, you override the default configuration values for the metastore in Hive to specify the external database location, either on an Amazon RDS MySQL instance or an Amazon Aurora instance\.

**Note**  
Hive neither supports nor prevents concurrent write access to metastore tables\. If you share metastore information between two clusters, you must ensure that you do not write to the same metastore table concurrently, unless you are writing to different partitions of the same metastore table\.

The following procedure shows you how to override the default configuration values for the Hive metastore location and start a cluster using the reconfigured metastore location\.

**To create a metastore located outside of the EMR cluster**

1. Create a MySQL or Aurora database\. 

   For information about how to create an Amazon RDS database, see [https://aws\.amazon\.com/rds/](https://aws.amazon.com/rds/)\.

1. Modify your security groups to allow JDBC connections between your database and the **ElasticMapReduce\-Master** security group\.

   For information about how to modify your security groups for access, see [https://aws\.amazon\.com/rds/faqs/\#security](https://aws.amazon.com/rds/faqs/#security)\.

1. Set JDBC configuration values in `hive-site.xml`:

   1. 
**Important**  
If you supply sensitive information, such as passwords, to the Amazon EMR configuration API, this information is displayed for those accounts that have sufficient permissions\. If you are concerned that this information could be displayed to other users, create the cluster with an administrative account and limit other users \(IAM users or those with delegated credentials\) to accessing services on the cluster by creating a role which explicitly denies permissions to the `elasticmapreduce:DescribeCluster` API key\.

     Create a configuration file called `hiveConfiguration.json` containing edits to `hive-site.xml` as shown in the following example\.

      *hostname*> is the DNS address of the Amazon RDS instance running the database\. <*username*> and <*password*> are the credentials for your database\. For more information about connecting to MySQL and Aurora database instances, see [Connecting to a DB Instance Running the MySQL Database Engine](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html) and [Connecting to an Athena DB Cluster](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Connect.html) in the *Amazon RDS User Guide*\. `javax.jdo.option.ConnectionURL` is the JDBC connect string for a JDBC metastore\. `javax.jdo.option.ConnectionDriverName` is the driver class name for a JDBC metastore\.

     The MySQL JDBC drivers are installed by Amazon EMR\. 

     The value property can not contain any spaces or carriage returns\. It should appear all on one line\.

     ```
     [
         {
           "Classification": "hive-site",
           "Properties": {
             "javax.jdo.option.ConnectionURL": "jdbc:mysql:\/\/hostname:3306\/hive?createDatabaseIfNotExist=true",
             "javax.jdo.option.ConnectionDriverName": "org.mariadb.jdbc.Driver",
             "javax.jdo.option.ConnectionUserName": "username",
             "javax.jdo.option.ConnectionPassword": "password"
           }
         }
       ]
     ```

     Reference the `hiveConfiguration.json` file when you create the cluster as shown in the following AWS CLI command\. In this command, the file is stored locally, you can also upload the file to Amazon S3 and reference it there, for example, `s3://mybucket/hiveConfiguration.json`\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

     ```
     aws emr create-cluster --release-label emr-5.23.0 --instance-type m4.large --instance-count 2 \
     --applications Name=Hive --configurations ./hiveConfiguration.json --use-default-roles
     ```

1. Connect to the master node of your cluster\. 

   For information about how to connect to the master node, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. Create your Hive tables specifying the location on Amazon S3 by entering a command similar to the following:

   ```
   CREATE EXTERNAL TABLE IF NOT EXISTS table_name
   (
   key int,
   value int
   )
   LOCATION s3://mybucket/hdfs/
   ```

1. Add your Hive script to the running cluster\.

Your Hive cluster runs using the metastore located in Amazon RDS\. Launch all additional Hive clusters that share this metastore by specifying the metastore location\. 