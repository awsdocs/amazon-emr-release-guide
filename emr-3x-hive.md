# Hive Application Specifics for Earlier AMI Versions of Amazon EMR<a name="emr-3x-hive"></a>

## Log files<a name="emr-3x-hive-log-files"></a>

Using Amazon EMR AMI versions 2\.x and 3\.x, Hive logs are saved to `/mnt/var/log/apps/`\. In order to support concurrent versions of Hive, the version of Hive that you run determines the log file name, as shown in the following table\. 


| Hive Version | Log File Name | 
| --- | --- | 
| 0\.13\.1 | hive\.log  Beginning with this version, Amazon EMR uses an unversioned file name, `hive.log`\. Minor versions share the same log location as the major version\.   | 
| 0\.11\.0 | hive\_0110\.log   Minor versions of Hive 0\.11\.0, such as 0\.11\.0\.1, share the same log file location as Hive 0\.11\.0\.   | 
| 0\.8\.1 | hive\_081\.log   Minor versions of Hive 0\.8\.1, such as Hive 0\.8\.1\.1, share the same log file location as Hive 0\.8\.1\.   | 
| 0\.7\.1 | hive\_07\_1\.log   Minor versions of Hive 0\.7\.1, such as Hive 0\.7\.1\.3 and Hive 0\.7\.1\.4, share the same log file location as Hive 0\.7\.1\.    | 
| 0\.7 | hive\_07\.log | 
| 0\.5 | hive\_05\.log | 
| 0\.4 | hive\.log | 

## Split Input Functionality<a name="emr-3x-hive-split-input"></a>

To implement split input functionality using Hive versions earlier than 0\.13\.1 \(Amazon EMR AMI versions earlier 3\.11\.0\), use the following:

```
hive> set hive.input.format=org.apache.hadoop.hive.ql.io.HiveCombineSplitsInputFormat;
hive> set mapred.min.split.size=100000000;
```

This functionality was deprecated with Hive 0\.13\.1\. To get the same split input format functionality in Amazon EMR AMI Version 3\.11\.0, use the following:

```
set hive.hadoop.supports.splittable.combineinputformat=true;
```

## Thrift Service Ports<a name="emr-3x-hive-thrift-service"></a>

 Thrift is an RPC framework that defines a compact binary serialization format used to persist data structures for later analysis\. Normally, Hive configures the server to operate on the following ports\. 


| Hive Version | Port Number | 
| --- | --- | 
| Hive 0\.13\.1 | 10000 | 
| Hive 0\.11\.0 | 10004 | 
| Hive 0\.8\.1 | 10003 | 
| Hive 0\.7\.1 | 10002 | 
| Hive 0\.7 | 10001 | 
| Hive 0\.5 | 10000 | 

 For more information about thrift services, see [http://wiki.apache.org/thrift/](http://wiki.apache.org/thrift/)\. 

## Use Hive to Recover Partitions<a name="emr-3x-hive-recover-partition"></a>

Amazon EMR includes a statement in the Hive query language that recovers the partitions of a table from table data located in Amazon S3\. The following example shows this\. 

```
CREATE EXTERNAL TABLE (json string) raw_impression 
PARTITIONED BY (dt string) 
LOCATION 's3://elastic-mapreduce/samples/hive-ads/tables/impressions';
ALTER TABLE logs RECOVER PARTITIONS;
```

The partition directories and data must be at the location specified in the table definition and must be named according to the Hive convention: for example, `dt=2009-01-01`\. 

**Note**  
After Hive 0\.13\.1 this capability is supported natively using `msck repair table` and therefore `recover partitions` is not supported\. For more information, see [https://cwiki\.apache\.org/confluence/display/Hive/LanguageManual\+DDL](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL)\.

## Pass a Hive Variable to a Script<a name="emr-3x-hive-pass-variable"></a>

To pass a variable into a Hive step using the AWS CLI, type the following command, replace *myKey* with the name of your EC2 key pair, and replace *mybucket* with your bucket name\. In this example, `SAMPLE` is a variable value preceded by the `-d` switch\. This variable is defined in the Hive script as: `${SAMPLE}`\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.9 \
--applications Name=Hue Name=Hive Name=Pig \
--use-default-roles --ec2-attributes KeyName=myKey \
--instance-type m3.xlarge --instance-count 3 \
--steps Type=Hive,Name="Hive Program",ActionOnFailure=CONTINUE,\
Args=[-f,s3://elasticmapreduce/samples/hive-ads/libs/response-time-stats.q,-d,\
INPUT=s3://elasticmapreduce/samples/hive-ads/tables,-d,OUTPUT=s3://mybucket/hive-ads/output/,\
-d,SAMPLE=s3://elasticmapreduce/samples/hive-ads/]
```

## Specify an External Metastore Location<a name="emr-3x-hive-external-metastore"></a>

The following procedure shows you how to override the default configuration values for the Hive metastore location and start a cluster using the reconfigured metastore location\.

**To create a metastore located outside of the EMR cluster**

1. Create a MySQL or Aurora database using Amazon RDS\.

   For information about how to create an Amazon RDS database, see [Getting Started with Amazon RDS](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/CHAP_GettingStarted.html)\.

1. Modify your security groups to allow JDBC connections between your database and the **ElasticMapReduce\-Master** security group\.

   For information about how to modify your security groups for access, see [Amazon RDS Security Groups](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Overview.RDSSecurityGroups.html) in the *Amazon RDS User Guide*\.

1. Set the JDBC configuration values in `hive-site.xml`:

   1. Create a `hive-site.xml` configuration file containing the following:

      ```
      <configuration>
        <property>
          <name>javax.jdo.option.ConnectionURL</name>
          <value>jdbc:mariadb://hostname:3306/hive?createDatabaseIfNotExist=true</value>
          <description>JDBC connect string for a JDBC metastore</description>
        </property>
        <property>
          <name>javax.jdo.option.ConnectionUserName</name>
          <value>hive</value>
          <description>Username to use against metastore database</description>
        </property>
        <property>
          <name>javax.jdo.option.ConnectionPassword</name>
          <value>password</value>
          <description>Password to use against metastore database</description>
        </property>
      </configuration>
      ```

      *hostname* is the DNS address of the Amazon RDS instance running the database\. *username* and *password* are the credentials for your database\. For more information about connecting to MySQL and Aurora database instances, see [Connecting to a DB Instance Running the MySQL Database Engine](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_ConnectToInstance.html) and [Connecting to an Aurora DB Cluster](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Aurora.Connecting.html) in the *Amazon RDS User Guide*\.

      The JDBC drivers are installed by Amazon EMR\. 
**Note**  
The value property should not contain any spaces or carriage returns\. It should appear all on one line\.

   1. Save your `hive-site.xml` file to a location on Amazon S3, such as `s3://mybucket/hive-site.xml`\.

1. Create a cluster, specifying the Amazon S3 location of the customized `hive-site.xml` file\.

   The following example command demonstrates an AWS CLI command that does this\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

   ```
   aws emr create-cluster --name "Test cluster" --ami-version 3.10 \
   --applications Name=Hue Name=Hive Name=Pig \
   --use-default-roles --ec2-attributes KeyName=myKey \
   --instance-type m3.xlarge --instance-count 3 \
   --bootstrap-actions Name="Install Hive Site Configuration",\
   Path="s3://region.elasticmapreduce/libs/hive/hive-script",\
   Args=["--base-path","s3://elasticmapreduce/libs/hive","--install-hive-site",\
   "--hive-site=s3://mybucket/hive-site.xml","--hive-versions","latest"]
   ```

## Connect to Hive Using JDBC<a name="emr-3x-hive-jdbc"></a>

To connect to Hive via JDBC requires you to download the JDBC driver and install a SQL client\. The following example demonstrates using SQL Workbench/J to connect to Hive using JDBC\.

**To download JDBC drivers**

1. Download and extract the drivers appropriate to the versions of Hive that you want to access\. The Hive version differs depending on the AMI that you choose when you create an Amazon EMR cluster\.
   + Hive 0\.13\.1 JDBC drivers: [https://amazon\-odbc\-jdbc\-drivers\.s3\.amazonaws\.com/public/AmazonHiveJDBC\_1\.0\.4\.1004\.zip](https://amazon-odbc-jdbc-drivers.s3.amazonaws.com/public/AmazonHiveJDBC_1.0.4.1004.zip)
   + Hive 0\.11\.0 JDBC drivers: [https://mvnrepository.com/artifact/org.apache.hive/hive-jdbc/0.11.0](https://mvnrepository.com/artifact/org.apache.hive/hive-jdbc/0.11.0)
   + Hive 0\.8\.1 JDBC drivers: [https://mvnrepository.com/artifact/org.apache.hive/hive-jdbc/0.8.1](https://mvnrepository.com/artifact/org.apache.hive/hive-jdbc/0.8.1)

1. Install SQL Workbench/J\. For more information, see [Installing and starting SQL Workbench/J](http://www.sql-workbench.net/manual/install.html) in the SQL Workbench/J Manual User's Manual\.

1. Create an SSH tunnel to the cluster master node\. The port for connection is different depending on the version of Hive\. Example commands are provided in the tables below for Linux `ssh` users and PuTTY commands for Windows users  
**Linux ssh Commands**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hive.html)  
**Windows PuTTY Tunnel Settings**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hive.html)

1. Add the JDBC driver to SQL Workbench\.

   1. In the **Select Connection Profile** dialog box, choose **Manage Drivers**\. 

   1. Choose the **Create a new entry** \(blank page\) icon\.

   1. In the **Name** field, type **Hive JDBC**\.

   1. For **Library**, click the **Select the JAR file\(s\)** icon\.

   1. Select JAR files as shown in the following table\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hive.html)

   1. In the **Please select one driver** dialog box, select a driver according to the following table and click **OK**\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hive.html)

1. When you return to the **Select Connection Profile** dialog box, verify that the **Driver** field is set to **Hive JDBC** and provide the JDBC connection string in the **URL** field according to the following table\.    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hive.html)

   If your cluster uses AMI version 3\.3\.1 or later, in the **Select Connection Profile** dialog box, type **hadoop** in the **Username** field\.