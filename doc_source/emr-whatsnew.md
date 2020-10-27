# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR 6\.x series and 5\.x series\. These release notes are also available on the [Release 6\.1\.0 Tab](emr-release-6x.md#emr-610-release) and [Release 5\.31\.0 Tab](emr-release-5x.md#emr-5310-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

**Note**  
Twenty\-five previous Amazon EMR release versions now use AWS Signature Version 4 to authenticate requests to Amazon S3\. The use of AWS Signature version 2 is being phased out and new S3 buckets created after June 24, 2020 will not support Signature Version 2 signed requests\. Existing buckets will continue to support Signature Version 2\. We recommend migrating to an Amazon EMR release that supports Signature Version 4 so you can continue accessing new S3 buckets and avoid any potential interruption to your workloads\.  
The following EMR releases are now available that supports Signature Version 4: emr\-4\.7\.4, emr\-4\.8\.5, emr\-4\.9\.6, emr\-4\.10\.1, emr\-5\.1\.1, emr\-5\.2\.3, emr\-5\.3\.2, emr\-5\.4\.1, emr\-5\.5\.4, emr\-5\.6\.1, emr\-5\.7\.1, emr\-5\.8\.3, emr\-5\.9\.1, emr\-5\.10\.1, emr\-5\.11\.4, emr\-5\.12\.3, emr\-5\.13\.1, emr\-5\.14\.2, emr\-5\.15\.1, emr\-5\.16\.1, emr\-5\.17\.2, emr\-5\.18\.1, emr\-5\.19\.1, emr\-5\.20\.1, and emr\-5\.21\.2\. EMR version 5\.22\.0 and later already support Signature Version 4\.  
You do not need to change your application code to use Signature Version 4 if you are using Amazon EMR applications, such as Apache Spark, Apache Hive, Presto, etc\. If you are using custom applications, which are not included with Amazon EMR, you may need to update your code to use Signature Version 4\. For more information about what updates may be required, see [Moving from Signature Version 2 to Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html#UsingAWSSDK-move-to-Sig4)\.

## Release 6\.1\.0 \(Latest version of Amazon EMR 6\.x series\)<a name="emr-610-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 6\.1\.0\. Changes are relative to 6\.0\.0\.

Initial release date: Sept 04, 2020

Last updated date: Oct 15, 2020

**Supported Applications**
+ AWS SDK for Java version 1\.11\.828
+ Flink version 1\.11\.0
+ Ganglia version 3\.7\.2
+ Hadoop version 3\.2\.1\-amzn\-1
+ HBase version 2\.2\.5
+ HBase\-operator\-tools 1\.0\.0
+ HCatalog version 3\.1\.2\-amzn\-0
+ Hive version 3\.1\.2\-amzn\-1
+ Hudi version 0\.5\.2\-incubating
+ Hue version 4\.7\.1
+ JupyterHub version 1\.1\.0
+ Livy version 0\.7\.0
+ MXNet version 1\.6\.0
+ Oozie version 5\.2\.0
+ Phoenix version 5\.0\.0
+ Presto version 0\.232
+ PrestoSQL version 338
+ Spark version 3\.0\.0
+ TensorFlow version 2\.1\.0
+ Zeppelin version 0\.9\.0\-preview1
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.14\.0

**New Features**
+ ARM instance types are supported starting with Amazon EMR version 5\.30\.0 and Amazon EMR version 6\.1\.0\.
+ M6g general purpose instance types are supported starting with Amazon EMR version 6\.1\.0\. For more information, see [Supported Instance Types](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-supported-instance-types.html) in the *Amazon EMR Management Guide*\.
+ The EC2 placement group feature is supported starting with Amazon EMR version 5\.23\.0 as an option for multiple master node clusters\. Currently, only master node types are supported by the placement group feature, and the `SPREAD` strategy is applied to those master nodes\. The `SPREAD` strategy places a small group of instances across separate underlying hardware to guard against the loss of multiple master nodes in the event of a hardware failure\. For more information, see [EMR Integration with EC2 Placement Group](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-placementgroup.html) in the *Amazon EMR Management Guide*\.
+ Managed Scaling – With Amazon EMR version 6\.1\.0, you can enable EMR managed scaling to automatically increase or decrease the number of instances or units in your cluster based on workload\. EMR continuously evaluates cluster metrics to make scaling decisions that optimize your clusters for cost and speed\. Managed Scaling is also available on Amazon EMR version 5\.30\.0 and later, except 6\.0\.0\. For more information, see [Scaling Cluster Resources](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scale-on-demand.html) in the *Amazon EMR Management Guide*\.
+ PrestoSQL version 338 is supported with EMR 6\.1\.0\. For more information, see [Configure Docker Integration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html)\.
  + PrestoSQL is supported on EMR 6\.1\.0 and later versions only, not on EMR 6\.0\.0 or EMR 5\.x\.
  + The application name, `Presto` continues to be used to install PrestoDB on clusters\. To install PrestoSQL on clusters, use the application name `PrestoSQL`\.
  + You can install either PrestoDB or PrestoSQL, but you cannot install both on a single cluster\. If both PrestoDB and PrestoSQL are specified when attempting to create a cluster, a validation error occurs and the cluster creation request fails\.
  + PrestoSQL is supported on both single\-master and muti\-master clusters\. On multi\-master clusters, an external Hive metastore is required to run PrestoSQL or PrestoDB\. See [Supported Applications in an EMR Cluster with Multiple Master Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-applications.html#emr-plan-ha-applications-list)\.
+ ECR auto authentication support on Apache Hadoop and Apache Spark with Docker: Spark users can use ﻿Docker﻿ images from ﻿Docker Hub﻿ and ﻿Amazon Elastic Container Registry \(Amazon ECR\)﻿ to define environment and library dependencies\.

  [Configure Docker](emr/latest/ManagementGuide/emr-plan-docker.html) and [Run Spark Applications with Docker Using Amazon EMR 6\.x](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-docker.html)\.
+ EMR supports Apache Hive ACID transactions: Amazon EMR 6\.1\.0 adds support for Hive ACID transactions so it complies with the ACID properties of a database\. With this feature, you can run INSERT, UPDATE, DELETE, and MERGE operations in Hive managed tables with data in Amazon Simple Storage Service \(Amazon S3\)\. This is a key feature for use cases like streaming ingestion, data restatement, bulk updates using MERGE, and slowly changing dimensions\. For more information, including configuration examples and use cases, see [Amazon EMR supports Apache Hive ACID transactions](https://aws.amazon.com/blogs/big-data/amazon-emr-supports-apache-hive-acid-transactions)\.

**Changes, Enhancements, and Resolved Issues**
+ Apache Flink is not supported on EMR 6\.0\.0, but it is supported on EMR 6\.1\.0 with Flink 1\.11\.0\. This is the first version of Flink to officially support Hadoop 3\. See [Apache Flink 1\.11\.0 Release Announcement](https://flink.apache.org/news/2020/07/06/release-1.11.0.html)\.
+ Ganglia has been removed from default EMR 6\.1\.0 package bundles\.

**Known Issues**
+ If you set custom garbage collection configuration with `spark.driver.extraJavaOptions` and `spark.executor.extraJavaOptions`, this will result in driver/executor launch failure with EMR 6\.1 due to conflicting garbage collection configuration\. With EMR Release 6\.1\.0, you should specify custom Spark garbage collection configuration for drivers and executors with the properties `spark.driver.defaultJavaOptions` and `spark.executor.defaultJavaOptions` instead\. Read more in [Apache Spark Runtime Environment](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) and [Configuring Spark Garbage Collection on Amazon EMR 6\.1\.0](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-configure.html#spark-gc-config)\.
+ Using Pig with Oozie \(and within Hue, since Hue uses Oozie actions to run Pig scripts\), generates an error that a native\-lzo library cannot be loaded\. This error message is informational and does not block Pig from running\.
+ Hudi Concurrency Support: Currently Hudi doesn’t support concurrent writes to a single Hudi table\. In addition, Hudi rolls back any changes being done by in\-progress writers before allowing a new writer to start\. Concurrent writes can interfere with this mechanism and introduce race conditions, which can lead to data corruption\. You should ensure that as part of your data processing workflow, there is only a single Hudi writer operating against a Hudi table at any time\. Hudi does support multiple concurrent readers operating against the same Hudi table\.
+ Known issue in clusters with multiple master nodes and Kerberos authentication

  If you run clusters with multiple master nodes and Kerberos authentication in EMR releases 5\.20\.0 and later, you may encounter problems with cluster operations such as scale down or step submission, after the cluster has been running for some time\. The time period depends on the Kerberos ticket validity period that you defined\. The scale\-down problem impacts both automatic scale\-down and explicit scale down requests that you submitted\. Additional cluster operations can also be impacted\. 

  Workaround:
  + SSH as `hadoop` user to the lead master node of the EMR cluster with multiple master nodes\.
  +  Run the following command to renew Kerberos ticket for `hadoop` user\. 

    ```
    kinit -kt <keytab_file> <principal>
    ```

    Typically, the keytab file is located at `/etc/hadoop.keytab` and the principal is in the form of `hadoop/<hostname>@<REALM>`\.
**Note**  
This workaround will be effective for the time period the Kerberos ticket is valid\. This duration is 10 hours by default, but can configured by your Kerberos settings\. You must re\-run the above command once the Kerberos ticket expires\.

## Release 5\.31\.0 \(Latest version of Amazon EMR 5\.x series\)<a name="emr-5310-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.31\.0\. Changes are relative to 5\.30\.1\.

Initial release date: Oct 9, 2020

Last updated date: Oct 15, 2020

**Upgrades**
+ Upgraded Amazon Glue connector to version 1\.13\.0
+ Upgraded Amazon SageMaker Spark SDK to version 1\.4\.0
+ Upgraded Amazon Kinesis connector to version 3\.5\.9 
+ Upgraded AWS Java SDK to version 1\.11\.852
+ Upgraded Bigtop\-tomcat to version 8\.5\.56
+ Upgraded EMR FS to version 2\.43\.0
+ Upgraded EMR MetricsAndEventsApiGateway Client to version 1\.4\.0
+ Upgraded EMR S3 Dist CP to version 2\.15\.0
+ Upgraded EMR S3 Select to version 1\.6\.0
+ Upgraded Flink to version 1\.11\.0
+ Upgraded Hadoop to version 2\.10\.0
+ Upgraded Hive to version 2\.3\.7
+ Upgraded Hudi to version 0\.6\.0
+ Upgraded Hue to version 4\.7\.1
+ Upgraded JupyterHub to version 1\.1\.0
+ Upgraded Mxnet to version 1\.6\.0
+ Upgraded OpenCV to version 4\.3\.0
+ Upgraded Presto to version 0\.238\.3
+ Upgraded TensorFlow to version 2\.1\.0

**Changes, Enhancements, and Resolved Issues**
+ Upgraded component versions\.
+ EMRFS S3EC V2 Support in 5\.31\.0\. In S3 Java SDK releases 1\.11\.837 and later, encryption client Version 2 \(S3EC V2\) has been introduced with various security enhancements\. For more information, see the following:
  + S3 blog post: [Updates to the Amazon S3 Encryption Client](https://aws.amazon.com/blogs/developer/updates-to-the-amazon-s3-encryption-client/)\.
  + AWS SDK for Java Developer Guide: [Migrate Encryption and Decryption Clients to V2](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/s3-encryption-migration.html#s3-cse-update-code)\.
  + EMR Management Guide: [Amazon S3 Client\-Side Encryption](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-encryption-cse.html)\.

  Encryption Client V1 is still available in the SDK for backward compatibility\.

**New Features**
+ With Amazon EMR 5\.31\.0, you can launch a cluster that integrates with Lake Formation\. This integration provides fine\-grained, column\-level data filtering to databases and tables in the AWS Glue Data Catalog\. It also enables federated single sign\-on to EMR Notebooks or Apache Zeppelin from an enterprise identity system\. For more information, see [Integrating Amazon EMR with AWS Lake Formation](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-lake-formation.html) in the *Amazon EMR Management Guide*\.

  Amazon EMR with Lake Formation is currently available in 16 AWS Regions: US East \(Ohio and N\. Virginia\), US West \(N\. California and Oregon\), Asia Pacific \(Mumbai, Seoul, Singapore, Sydney, and Tokyo\), Canada \(Central\), Europe \(Frankfurt, Ireland, London, Paris, and Stockholm\), South America \(São Paulo\)\.

**Known Issues**
+ Known issue in clusters with multiple master nodes and Kerberos authentication

  If you run clusters with multiple master nodes and Kerberos authentication in EMR releases 5\.20\.0 and later, you may encounter problems with cluster operations such as scale down or step submission, after the cluster has been running for some time\. The time period depends on the Kerberos ticket validity period that you defined\. The scale\-down problem impacts both automatic scale\-down and explicit scale down requests that you submitted\. Additional cluster operations can also be impacted\. 

  Workaround:
  + SSH as `hadoop` user to the lead master node of the EMR cluster with multiple master nodes\.
  +  Run the following command to renew Kerberos ticket for `hadoop` user\. 

    ```
    kinit -kt <keytab_file> <principal>
    ```

    Typically, the keytab file is located at `/etc/hadoop.keytab` and the principal is in the form of `hadoop/<hostname>@<REALM>`\.
**Note**  
This workaround will be effective for the time period the Kerberos ticket is valid\. This duration is 10 hours by default, but can configured by your Kerberos settings\. You must re\-run the above command once the Kerberos ticket expires\.