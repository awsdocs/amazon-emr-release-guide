# Amazon EMR What's New History<a name="emr-whatsnew-history"></a>

Release notes for earlier Amazon EMR release versions are available below\. For most recent release notes, see [](emr-whatsnew.md#emr-5120-whatsnew)\. For comprehensive release information for each release, see [Amazon EMR 5\.x Release Versions](emr-release-5x.md) and [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

## Release 5\.11\.1 \(Latest\)<a name="emr-5111-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.11\.1 release\. Changes are relative to the Amazon EMR 5\.11\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-5111-enhancements"></a>

+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

### Known Issues<a name="emr-5111-known-issues"></a>

+ MXNet does not include OpenCV libraries\.

+ Hive 2\.3\.2 sets `hive.compute.stats.using.query=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.stats.using.query=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.stats.using.query=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.11\.0<a name="emr-5110-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.11\.0 release\. Changes are relative to the Amazon EMR 5\.10\.0 release\.

### Upgrades<a name="emr-5110-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.

+ Hive 2\.3\.2

+ Spark 2\.2\.1

+ SDK for Java 1\.11\.238

### New Features<a name="emr-5110-new-features"></a>

+ **Spark**

  + Added `spark.decommissioning.timeout.threshold` setting, which improves Spark decommissioning behavior when using Spot instances\. For more information, see [Configuring Node Decommissioning Behavior](emr-spark-configure.md#spark-decommissioning)\.

  + Added the `aws-sagemaker-spark-sdk` component to Spark, which installs Amazon SageMaker Spark and associated dependencies for Spark integration with [Amazon SageMaker](https://aws.amazon.com/sagemaker/)\. You can use Amazon SageMaker Spark to construct Spark machine learning \(ML\) pipelines using Amazon SageMaker stages\. For more information, see the [SageMaker Spark Readme](https://github.com/aws/sagemaker-spark/blob/master/README.md) on GitHub and [Using Apache Spark with Amazon SageMaker](http://docs.aws.amazon.com/sagemaker/latest/dg/apache-spark.html) in the *Amazon SageMaker Developer Guide*\.

### Known Issues<a name="emr-5110-known-issues"></a>

+ MXNet does not include OpenCV libraries\.

+ Hive 2\.3\.2 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.10\.0<a name="emr-5100-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.10\.0 release\. Changes are relative to the Amazon EMR 5\.9\.0 release\.

### Upgrades<a name="emr-5100-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.

+ AWS SDK for Java 1\.11\.221

+ Hive 2\.3\.1

+ Presto 0\.187

### New Features<a name="emr-5100-new-features"></a>

+ Added support for Kerberos authentication\. For more information, see [Use Kerberos Authentication](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html) in the *Amazon EMR Management Guide*

+ Added support for EMRFS authorization\. For more information, see [Use EMRFS Authorization for Data in Amazon S3](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-authz.html) in the *Amazon EMR Management Guide*

+ Added support for GPU\-based P2 and P3 instance types\. For more information, see [Amazon EC2 P2 Instances](https://aws.amazon.com/ec2/instance-types/p2/) and [Amazon EC2 P3 Instances](https://aws.amazon.com/ec2/instance-types/p3/)\. NVIDIA driver 384\.81 and CUDA driver 9\.0\.176 are installed on these instance types by default\.

+ Added support for [Apache MXNet](emr-mxnet.md)\.

### Changes, Enhancements, and Resolved Issues<a name="emr-5100-enhancements"></a>

+ Presto

  + Added support for using the AWS Glue Data Catalog as the default Hive metastore\. For more information, see [Using Presto with the AWS Glue Data Catalog](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-presto.html#emr-presto-glue)\.

  + Added support for [geospatial functions](https://prestodb.io/docs/current/functions/geospatial.html)\.

  + Added [spill to disk](https://prestodb.io/docs/current/admin/spill.html) support for joins\.

  + Added support for the [Redshift connector](https://prestodb.io/docs/current/connector/redshift.html)\.

+ Spark

  + Backported [SPARK\-20640](https://issues.apache.org/jira/browse/SPARK-20640), which makes the rpc timeout and the retries for shuffle registration values configurable using `spark.shuffle.registration.timeout` and `spark.shuffle.registration.maxAttempts` properties\.

  + Backported [SPARK\-21549](https://issues.apache.org/jira/browse/SPARK-21549), which corrects an error that occurs when writing custom OutputFormat to non\-HDFS locations\.

+ Backported [Hadoop\-13270](https://issues.apache.org/jira/browse/HADOOP-13270)

+ The Numpy, Scipy, and Matplotlib libraries have been removed from the base Amazon EMR AMI\. If these libraries are required for your application, they are available in the application repository, so you can use a bootstrap action to install them on all nodes using `yum install`\.

+ The Amazon EMR base AMI no longer has application RPM packages included, so the RPM packages are no longer present on cluster nodes\. Custom AMIs and the Amazon EMR base AMI now reference the RPM package repository in Amazon S3\.

+ Because of the introduction of per\-second billing in Amazon EC2, the default **Scale down behavior** is now **Terminate at task completion** rather than **Terminate at instance hour**\. For more information, see [Configure Cluster Scale\-Down](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scaledown-behavior.html)\.

### Known Issues<a name="emr-5100-known-issues"></a>

+ MXNet does not include OpenCV libraries\.

+ Hive 2\.3\.1 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.9\.0<a name="emr-590-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.9\.0 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Release date: October 5, 2017

Latest feature update: October 12, 2017

### Upgrades<a name="emr-590-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.

+ AWS SDK for Java version 1\.11\.183

+ Flink 1\.3\.2

+ Hue 4\.0\.1

+ Pig 0\.17\.0

+ Presto 0\.184

### New Features<a name="emr-590-new-features"></a>

+ Added Livy support \(version 0\.4\.0\-incubating\)\. For more information, see [Apache Livy](emr-livy.md)\.

+ Added support for Hue Notebook for Spark\.

+ Added support for i3\-series Amazon EC2 instances \(October 12, 2017\)\.

### Changes, Enhancements, and Resolved Issues<a name="emr-590-enhancements"></a>

+ Spark

  + Added a new set of features that help ensure Spark handles node termination because of a manual resize or an automatic scaling policy request more gracefully\. For more information, see [Configuring Node Decommissioning Behavior](emr-spark-configure.md#spark-decommissioning)\.

  + SSL is used instead of 3DES for in\-transit encryption for the block transfer service, which enhances performance when using Amazon EC2 instance types with AES\-NI\.

  + Backported [SPARK\-21494](https://issues.apache.org/jira/browse/SPARK-21494)\.

+ Zeppelin

  + Backported [ZEPPELIN\-2377](https://issues.apache.org/jira/browse/ZEPPELIN-2377)\.

+ HBase

  + Added patch [HBASE\-18533](https://issues.apache.org/jira/browse/HBASE-18533), which allows additional values for HBase BucketCache configuration using the `hbase-site` configuration classification\.

+ Hue

  + Added AWS Glue Data Catalog support for the Hive query editor in Hue\.

  + By default, superusers in Hue can access all files that Amazon EMR IAM roles are allowed to access\. Newly created users do not automatically have permissions to access the Amazon S3 filebrowser and must have the `filebrowser.s3_access` permissions enabled for their group\.

+ Resolved an issue that caused underlying JSON data created using AWS Glue Data Catalog to be inaccessible\.

### Known Issues<a name="emr-590-known-issues"></a>

+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.

+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.8\.1<a name="emr-581-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.8\.1 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-581-enhancements"></a>

+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 5\.8\.0<a name="emr-580-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.8\.0 release\. Changes are relative to the Amazon EMR 5\.7\.0 release\.

Initial release date: August 10, 2017

Latest feature update: September 25, 2017

### Upgrades<a name="emr-580-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions:

+ AWS SDK 1\.11\.160

+ Flink 1\.3\.1

+ Hive 2\.3\.0\. For more information, see [Release Notes](https://issues.apache.org/jira/secure/ConfigureReleaseNote.jspa?projectId=12310843&version=12340269) on the Apache Hive site\.

+ Spark 2\.2\.0\. For more information, see [Release Notes](https://spark.apache.org/releases/spark-release-2-2-0.html) on the Apache Spark site\.

### New Features<a name="emr-580-new-features"></a>

+ Added support for viewing application history \(September 25, 2017\)\. For more information, see [Viewing Application History](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.

### Changes, Enhancements, and Resolved Issues<a name="emr-580-enhancements"></a>

+ **Integration with AWS Glue Data Catalog**

  + Added ability for Hive and Spark SQL to use AWS Glue Data Catalog as the Hive metadata store\. For more information, see [Using the AWS Glue Data Catalog as the Metastore for Hive](emr-hive-metastore-glue.md) and [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md)\.

+ Added **Application history** to cluster details, which allows you to view historical data for YARN applications and additional details for Spark applications\. For more information, see [View Application History](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.

+ **Oozie**

  + Backported [OOZIE\-2748](https://issues.apache.org/jira/browse/OOZIE-2748)\.

+ **Hue**

  + Backported [HUE\-5859](https://issues.cloudera.org/browse/HUE-5859)

+ **HBase**

  + Added patch to expose the HBase master server start time through Java Management Extensions \(JMX\) using `getMasterInitializedTime`\.

  + Added patch that improves cluster start time\.

### Known Issues<a name="emr-580-known-issues"></a>

+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.

+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

+ **Spark**—When using Spark, there is a file handler leak issue with the apppusher daemon, which can appear for a long\-running Spark job after several hours or days\. To fix the issue, connect to the master node and type `sudo /etc/init.d/apppusher stop`\. This stops that apppusher daemon, which Amazon EMR will restart automatically\.

+ **Application history**

  + Historical data for dead Spark executors is not available\.

  + Application history is not available for clusters that use a security configuration to enable in\-flight encryption\.

## Release 5\.7\.0<a name="w3ab1c11c11c17"></a>

The following release notes include information for the Amazon EMR 5\.7\.0 release\. Changes are relative to the Amazon EMR 5\.6\.0 release\.

Release date: July 13, 2017

### Upgrades<a name="w3ab1c11c11c17b6"></a>

+ Flink 1\.3\.0

+ Phoenix 4\.11\.0

+ Zeppelin 0\.7\.2

### New Features<a name="w3ab1c11c11c17b8"></a>

+ Added the ability to specify a custom Amazon Linux AMI when you create a cluster\. For more information, see [Using a Custom AMI](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html)\.

### Changes, Enhancements, and Resolved Issues<a name="w3ab1c11c11c17c10"></a>

+ **HBase**

  + Added capability to configure HBase read\-replica clusters\. See [Using a Read\-Replica Cluster\.](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-read-replica)

  + Multiple bug fixes and enhancements

+ **Presto**—added ability to configure `node.properties`\.

+ **YARN**—added ability to configure `container-log4j.properties`

+ **Sqoop**—backported [SQOOP\-2880](https://issues.apache.org/jira/browse/SQOOP-2880), which introduces an argument that allows you to set the Sqoop temporary directory\.

## Release 5\.6\.0<a name="w3ab1c11c11c19"></a>

The following release notes include information for the Amazon EMR 5\.6\.0 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Release date: June 5, 2017

### Upgrades<a name="w3ab1c11c11c19b6"></a>

+ Flink 1\.2\.1

+ HBase 1\.3\.1

+ Mahout 0\.13\.0\. This is the first version of Mahout to support Spark 2\.x in Amazon EMR version 5\.0 and later\.

+ Spark 2\.1\.1

### Changes, Enhancements, and Resolved Issues<a name="w3ab1c11c11c19b8"></a>

+ **Presto**

  + Added the ability to enable SSL/TLS secured communication between Presto nodes by enabling in\-transit encryption using a security configuration\. For more information, see [In\-transit Data Encryption](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption-options.html#emr-encryption-intransit)\.

  + Backported [Presto 7661](https://github.com/prestodb/presto/pull/7661/commits), which adds the `VERBOSE` option to the `EXPLAIN ANALYZE` statement to report more detailed, low level statistics about a query plan\.

## Release 5\.5\.1<a name="emr-551-whatsnew"></a>

The following release notes include information for the Amazon EMR 5\.5\.1 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-551-enhancements"></a>

+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 5\.5\.0<a name="w3ab1c11c11c23"></a>

The following release notes include information for the Amazon EMR 5\.5\.0 release\. Changes are relative to the Amazon EMR 5\.4\.0 release\.

Release date: April 26, 2017

### Upgrades<a name="w3ab1c11c11c23b6"></a>

+ Hue 3\.12

+ Presto 0\.170

+ Zeppelin 0\.7\.1

+ ZooKeeper 3\.4\.10

### Changes, Enhancements, and Resolved Issues<a name="w3ab1c11c11c23b8"></a>

+ **Spark**

  + Backported Spark Patch [\(SPARK\-20115\) Fix DAGScheduler to recompute all the lost shuffle blocks when external shuffle service is unavailable](https://issues.apache.org/jira/browse/SPARK-20115) to version 2\.1\.0 of Spark, which is included in this release\.

+ **Flink**

  + Flink is now built with Scala 2\.11\. If you use the Scala API and libraries, we recommend that you use Scala 2\.11 in your projects\.

  + Addressed an issue where `HADOOP_CONF_DIR` and `YARN_CONF_DIR` defaults were not properly set, so `start-scala-shell.sh` failed to work\. Also added the ability to set these values using `env.hadoop.conf.dir` and `env.yarn.conf.dir` in `/etc/flink/conf/flink-conf.yaml` or the `flink-conf` configuration classification\.

  + Introduced a new EMR\-specific command, `flink-scala-shell` as a wrapper for `start-scala-shell.sh`\. We recommend using this command instead of `start-scala-shell`\. The new command simplifies execution\. For example, `flink-scala-shell -n 2` starts a Flink Scala shell with a task parallelism of 2\.

  + Introduced a new EMR\-specific command, `flink-yarn-session` as a wrapper for `yarn-session.sh`\. We recommend using this command instead of `yarn-session`\. The new command simplifies execution\. For example, `flink-yarn-session -n 2 -d` starts a long\-running Flink session in a detached state with two task managers\. 

  + Addressed [\(FLINK\-6125\) Commons httpclient is not shaded anymore in Flink 1\.2](https://issues.apache.org/jira/browse/FLINK-6125)\.

+ **Presto**

  + Added support for LDAP authentication\. Using LDAP with Presto on Amazon EMR requires that you enable HTTPS access for the Presto coordinator \(`http-server.https.enabled=true` in `config.properties`\)\. For configuration details, see [LDAP Authentication](https://prestodb.io/docs/current/security/ldap.html) in Presto documentation\.

  + Added support for `SHOW GRANTS`\.

+ **Amazon EMR Base Linux AMI**

  + Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [Amazon Linux AMI 2017\.03 Release Notes](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.

  + Removed Python 2\.6 from the Amazon EMR base Linux image\. Python 2\.7 and 3\.4 are installed by default\. You can install Python 2\.6 manually if necessary\.

## Release 5\.4\.0<a name="w3ab1c11c11c25"></a>

The following release notes include information for the Amazon EMR 5\.4\.0 release\. Changes are relative to the Amazon EMR 5\.3\.0 release\.

Release date: March 08, 2017

### Upgrades<a name="w3ab1c11c11c25b6"></a>

The following upgrades are available in this release:

+ Upgraded to Flink 1\.2\.0

+ Upgraded to Hbase 1\.3\.0

+ Upgraded to Phoenix 4\.9\.0
**Note**  
If you upgrade from an earlier version of Amazon EMR to Amazon EMR version 5\.4\.0 or later and use secondary indexing, upgrade local indexes as described in the [Apache Phoenix documentation](https://phoenix.apache.org/secondary_indexing.html#Upgrading_Local_Indexes_created_before_4.8.0)\. Amazon EMR removes the required configurations from the `hbase-site` classification, but indexes need to be repopulated\. Online and offline upgrade of indexes are supported\. Online upgrades are the default, which means indexes are repopulated while initializing from Phoenix clients of version 4\.8\.0 or greater\. To specify offline upgrades, set the `phoenix.client.localIndexUpgrade` configuration to false in the `phoenix-site` classification, and then SSH to the master node to run `psql [zookeeper] -1`\.

+ Upgraded to Presto 0\.166

+ Upgraded to Zeppelin 0\.7\.0

### Changes and Enhancements<a name="w3ab1c11c11c25b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.4\.0:

+ Added support for r4 instances\. See [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)\.

## Release 5\.3\.0<a name="w3ab1c11c11c27"></a>

The following release notes include information for the Amazon EMR 5\.3\.0 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: January 26, 2017

### Upgrades<a name="w3ab1c11c11c27b6"></a>

The following upgrades are available in this release:

+ Upgraded to Hive 2\.1\.1

+ Upgraded to Hue 3\.11\.0

+ Upgraded to Spark 2\.1\.0

+ Upgraded to Oozie 4\.3\.0

+ Upgraded to Flink 1\.1\.4

### Changes and Enhancements<a name="w3ab1c11c11c27b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.3\.0:

+ Added a patch to Hue that allows you to use the `interpreters_shown_on_wheel` setting to configure what interpreters to show first on the Notebook selection wheel, regardless of their ordering in the `hue.ini` file\.

+ Added the `hive-parquet-logging` configuration classification, which you can use to configure values in Hive's `parquet-logging.properties` file\.

## Release 5\.2\.2<a name="w3ab1c11c11c29"></a>

The following release notes include information for the Amazon EMR 5\.2\.2 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: May 2, 2017

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c29b6"></a>

+ Backported [SPARK\-194459](https://issues.apache.org/jira/browse/SPARK-19459), which addresses an issue where reading from an ORC table with char/varchar columns can fail\.

## Release 5\.2\.1<a name="w3ab1c11c11c31"></a>

The following release notes include information for the Amazon EMR 5\.2\.1 release\. Changes are relative to the Amazon EMR 5\.2\.0 release\.

Release date: December 29, 2016

### Upgrades<a name="w3ab1c11c11c31b6"></a>

The following upgrades are available in this release:

+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\. 

+ Upgraded to Zookeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

### Changes and Enhancements<a name="w3ab1c11c11c31b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.2\.1:

+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.

+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

+ The location of Flink and YARN configuration paths are now set by default in `/etc/default/flink` that you don't need to set the environment variables `FLINK_CONF_DIR` and `HADOOP_CONF_DIR` when running the `flink` or `yarn-session.sh` driver scripts to launch Flink jobs\.

+ Added support for FlinkKinesisConsumer class\.

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c31c10"></a>

+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.

+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

## Release 5\.2\.0<a name="w3ab1c11c11c33"></a>

The following release notes include information for the Amazon EMR 5\.2\.0 release\. Changes are relative to the Amazon EMR 5\.1\.0 release\.

Release date: November 21, 2016

### Changes and enhancements<a name="w3ab1c11c11c33b6"></a>

The following changes and enhancements are available in this release:

+ Added Amazon S3 storage mode for HBase\.

+  Enables you to specify an Amazon S3 location for the HBase rootdir\. For more information, see [HBase on Amazon S3](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html)\.

### Upgrades<a name="w3ab1c11c11c33b8"></a>

The following upgrades are available in this release:

+ Upgraded to Spark 2\.0\.2

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c33c10"></a>

+ Fixed an issue with /mnt being constrained to 2 TB on EBS\-only instance types\.

+ Fixed an issue with instance\-controller and logpusher logs being output to their corresponding \.out files instead of to their normal log4j\-configured \.log files, which rotate hourly\. The \.out files don't rotate, so this would eventually fill up the /emr partition\. This issue only affects hardware virtual machine \(HVM\) instance types\.

## Release 5\.1\.0<a name="w3ab1c11c11c35"></a>

The following release notes include information for the Amazon EMR 5\.1\.0 release\. Changes are relative to the Amazon EMR 5\.0\.0 release\.

Release date: November 03, 2016

### Changes and enhancements<a name="w3ab1c11c11c35b6"></a>

The following changes and enhancements are available in this release:

+ Added support for Flink 1\.1\.3\.

+ Presto has been added as an option in the notebook section of Hue\.

### Upgrades<a name="w3ab1c11c11c35b8"></a>

The following upgrades are available in this release:

+ Upgraded to HBase 1\.2\.3

+ Upgraded to Zeppelin 0\.6\.2

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c35c10"></a>

+ Fixed an issue with Tez queries on Amazon S3 with ORC files did not perform as well as earlier Amazon EMR 4\.x versions\.

## Release 5\.0\.3<a name="w3ab1c11c11c37"></a>

The following release notes include information for the Amazon EMR 5\.0\.3 release\. Changes are relative to the Amazon EMR 5\.0\.0 release\.

Release date: October 24, 2016

### Upgrades<a name="w3ab1c11c11c37b6"></a>

The following upgrades are available in this release:

+ Upgraded to Hadoop 2\.7\.3

+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.

+ Upgraded to Spark 2\.0\.1

+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

## Release 5\.0\.0<a name="w3ab1c11c11c39"></a>

 Release date: July 27, 2016

### Upgrades<a name="w3ab1c11c11c39b4"></a>

The following upgrades are available in this release:

+ Upgraded to Hive 2\.1

+ Upgraded to Presto 0\.150

+ Upgraded to Spark 2\.0

+ Upgraded to Hue 3\.10\.0

+ Upgraded to Pig 0\.16\.0

+ Upgraded to Tez 0\.8\.4

+ Upgraded to Zeppelin 0\.6\.1

### Changes and Enhancements<a name="w3ab1c11c11c39b6"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.0\.0 or greater:

+ Amazon EMR supports the latest open\-source versions of Hive \(version 2\.1\) and Pig \(version 0\.16\.0\)\. If you have used Hive or Pig on Amazon EMR in the past, this may affect some use cases\. For more information, see [Hive](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive.html) and [Pig](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-pig.html)\.

+ The default execution engine for Hive and Pig is now Tez\. To change this, you would edit the appropriate values in the `hive-site` and `pig-properties` configuration classifications, respectively\.

+ An enhanced step debugging feature was added, which allows you to see the root cause of step failures if the service can determine the cause\. For more information, see [ Enhanced Step Debugging](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-enhanced-step-debugging.html) in the Amazon EMR Management Guide\.

+ Applications that previously ended with "\-Sandbox" no longer have that suffix\. This may break your automation, for example, if you are using scripts to launch clusters with these applications\. The following table shows application names in Amazon EMR 4\.7\.2 versus Amazon EMR 5\.0\.0\.   
**Application name changes**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew-history.html)

+ Spark is now compiled for Scala 2\.11\.

+ Java 8 is now the default JVM\. All applications run using the Java 8 runtime\. There are no changes to any application’s byte code target\. Most applications continue to target Java 7\.

+ Zeppelin now includes authentication features\. For more information, see [Zeppelin](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-zeppelin.html)\.

+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

## Release 4\.9\.3<a name="emr-493-whatsnew"></a>

The following release notes include information for the Amazon EMR 4\.9\.3 release\. Changes are relative to the Amazon EMR 4\.9\.2 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-493-enhancements"></a>

+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 4\.9\.2<a name="w3ab1c11c11c43"></a>

The following release notes include information for the Amazon EMR 4\.9\.2 release\. Changes are relative to the Amazon EMR 4\.9\.1 release\.

Release date: July 13, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

## Release 4\.9\.1<a name="w3ab1c11c11c45"></a>

The following release notes include information for the Amazon EMR 4\.9\.1 release\. Changes are relative to the Amazon EMR 4\.8\.4 release\.

Release date: April 10, 2017

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c45b6"></a>

+ Backports of [HIVE\-9976](https://issues.apache.org/jira/browse/HIVE-9976) and [HIVE\-10106](https://issues.apache.org/jira/browse/HIVE-10106)

+ Fixed an issue in YARN where a large number of nodes \(greater than 2,000\) and containers \(greater than 5,000\) would cause an out of memory error, for example: `"Exception in thread 'main' java.lang.OutOfMemoryError"`\.

### Changes and Enhancements<a name="w3ab1c11c11c45b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.9\.1:

+ Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.

+ Removed Python 2\.6 from the Amazon EMR base Linux image\. You can install Python 2\.6 manually if necessary\.

## Release 4\.8\.4<a name="w3ab1c11c11c47"></a>

The following release notes include information for the Amazon EMR 4\.8\.4 release\. Changes are relative to the Amazon EMR 4\.8\.3 release\.

Release date: Feb 7, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

## Release 4\.8\.3<a name="w3ab1c11c11c49"></a>

The following release notes include information for the Amazon EMR 4\.8\.3 release\. Changes are relative to the Amazon EMR 4\.8\.2 release\.

Release date: December 29, 2016

### Upgrades<a name="w3ab1c11c11c49b6"></a>

The following upgrades are available in this release:

+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\.

+ Upgraded to Spark 1\.6\.3\. For more information, see [Spark Release Notes](http://spark.apache.org/releases/spark-release-1-6-3.html) in the Apache Spark documentation\.

+ Upgraded to ZooKeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

### Changes and Enhancements<a name="w3ab1c11c11c49b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.8\.3:

+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.

+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c49c10"></a>

+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.

+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

## Release 4\.8\.2<a name="w3ab1c11c11c51"></a>

The following release notes include information for the Amazon EMR 4\.8\.2 release\. Changes are relative to the Amazon EMR 4\.8\.0 release\.

Release date: October 24, 2016

### Upgrades<a name="w3ab1c11c11c51b6"></a>

The following upgrades are available in this release:

+ Upgraded to Hadoop 2\.7\.3

+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.

+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

## Release 4\.8\.0<a name="w3ab1c11c11c53"></a>

Release date: September 7, 2016

### Upgrades<a name="w3ab1c11c11c53b4"></a>

The following upgrades are available in this release:

+ Upgraded to HBase 1\.2\.2

+ Upgraded to Presto\-Sandbox 0\.151

+ Upgraded to Tez 0\.8\.4

+ Upgraded to Zeppelin\-Sandbox 0\.6\.1

### Changes and Enhancements<a name="w3ab1c11c11c53b6"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.8\.0:

+ Fixed an issue in YARN where the ApplicationMaster would attempt to clean up containers that no longer exist because their instances have been terminated\.

+ Corrected the hive\-server2 URL for Hive2 actions in the Oozie examples\.

+ Added support for additional Presto catalogs\.

+ Backported patches: [HIVE\-8948](https://issues.apache.org/jira/browse/HIVE-8948), [HIVE\-12679](https://issues.apache.org/jira/browse/HIVE-12679), [HIVE\-13405](https://issues.apache.org/jira/browse/HIVE-13405), [PHOENIX\-3116](https://issues.apache.org/jira/browse/PHOENIX-3116), [HADOOP\-12689](https://issues.apache.org/jira/browse/HADOOP-12689)

+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

## Release 4\.7\.2<a name="w3ab1c11c11c55"></a>

The following release notes include information for Amazon EMR 4\.7\.2\.

Release date: July 15, 2016

### Features<a name="w3ab1c11c11c55b6"></a>

The following features are available in this release:

+ Upgraded to Mahout 0\.12\.2

+ Upgraded to Presto 0\.148

+ Upgraded to Spark 1\.6\.2

+ You can now create an AWSCredentialsProvider for use with EMRFS using a URI as a parameter\. For more information, see [Create an AWSCredentialsProvider for EMRFS](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-plan-credentialsprovider.html)\.

+ EMRFS now allows users to configure a custom DynamoDB endpoint for their Consistent View metadata using the `fs.s3.consistent.dynamodb.endpoint` property in `emrfs-site.xml`\.

+ Added a script in `/usr/bin` called `spark-example`, which wraps `/usr/lib/spark/spark/bin/run-example` so you can run examples directly\. For instance, to run the SparkPi example that comes with the Spark distribution, you can run `spark-example SparkPi 100` from the command line or using `command-runner.jar` as a step in the API\.

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c55b8"></a>

+ Fixed an issue where Oozie had the `spark-assembly.jar` was not in the correct location when Spark was also installed, which resulted in failure to launch Spark applications with Oozie\.

+ Fixed an issue with Spark Log4j\-based logging in YARN containers\.

## Release 4\.7\.1<a name="w3ab1c11c11c57"></a>

Release date: June 10, 2016

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c57b4"></a>

+ Fixed an issue that extended the startup time of clusters launched in a VPC with private subnets\. The bug only impacted clusters launched with the Amazon EMR 4\.7\.0 release\. 

+ Fixed an issue that improperly handled listing of files in Amazon EMR for clusters launched with the Amazon EMR 4\.7\.0 release\.

## Release 4\.7\.0<a name="w3ab1c11c11c59"></a>

**Important**  
Amazon EMR 4\.7\.0 is deprecated\. Use Amazon EMR 4\.7\.1 or later instead\.

Release date: June 2, 2016

### Features<a name="w3ab1c11c11c59b6"></a>

The following features are available in this release:

+ Added Apache Phoenix 4\.7\.0

+ Added Apache Tez 0\.8\.3

+ Upgraded to HBase 1\.2\.1

+ Upgraded to Mahout 0\.12\.0

+ Upgraded to Presto 0\.147

+ Upgraded the AWS SDK for Java to 1\.10\.75

+ The final flag was removed from the `mapreduce.cluster.local.dir` property in `mapred-site.xml` to allow users to run Pig in local mode\.

### Amazon Redshift JDBC Drivers Available on Cluster<a name="w3ab1c11c11c59b8"></a>

Amazon Redshift JDBC drivers are now included at `/usr/share/aws/redshift/jdbc`\. `/usr/share/aws/redshift/jdbc/RedshiftJDBC41.jar` is the JDBC 4\.1\-compatible Amazon Redshift driver and `/usr/share/aws/redshift/jdbc/RedshiftJDBC4.jar` is the JDBC 4\.0\-compatible Amazon Redshift driver\. For more information, see [Configure a JDBC Connection](http://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html) in the *Amazon Redshift Cluster Management Guide*\.

### Java 8<a name="w3ab1c11c11c59c10"></a>

Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c59c12"></a>

+ Fixed a kernel issue that significantly affected performance on Throughput Optimized HDD \(st1\) EBS volumes for Amazon EMR in emr\-4\.6\.0\.

+ Fixed an issue where a cluster would fail if any HDFS encryption zone were specified without choosing Hadoop as an application\.

+ Changed the default HDFS write policy from `RoundRobin` to `AvailableSpaceVolumeChoosingPolicy`\. Some volumes were not properly utilized with the RoundRobin configuration, which resulted in failed core nodes and an unreliable HDFS\.

+ Fixed an issue with the EMRFS CLI, which would cause an exception when creating the default DynamoDB metadata table for consistent views\.

+ Fixed a deadlock issue in EMRFS that potentially occurred during multipart rename and copy operations\.

+ Fixed an issue with EMRFS that caused the CopyPart size default to be 5 MB\. The default is now properly set at 128 MB\.

+ Fixed an issue with the Zeppelin upstart configuration that potentially prevented you from stopping the service\.

+ Fixed an issue with Spark and Zeppelin, which prevented you from using the `s3a://` URI scheme because `/usr/lib/hadoop/hadoop-aws.jar` was not properly loaded in their respective classpath\.

+ Backported [HUE\-2484](https://issues.cloudera.org/browse/HUE-2484)\.

+ Backported a [commit](https://github.com/cloudera/hue/commit/c3c89f085e7a29c9fac7de016d881142d90af3eb) from Hue 3\.9\.0 \(no JIRA exists\) to fix an issue with the HBase browser sample\. 

+ Backported [HIVE\-9073](https://issues.apache.org/jira/browse/HIVE-9073)\.

## Release 4\.6\.0<a name="w3ab1c11c11c61"></a>

Release date: April 21, 2016

### Features<a name="w3ab1c11c11c61b4"></a>

The following features are available in this release:

+ Added HBase 1\.2\.0

+ Added Zookeeper\-Sandbox 3\.4\.8 

+ Upgraded to Presto\-Sandbox 0\.143

+ Amazon EMR releases are now based on Amazon Linux 2016\.03\.0\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/)\.

### Issue Affecting Throughput Optimized HDD \(st1\) EBS Volume Types<a name="w3ab1c11c11c61b6"></a>

An issue in the Linux kernel versions 4\.2 and above significantly affects performance on Throughput Optimized HDD \(st1\) EBS volumes for EMR\. This release \(emr\-4\.6\.0\) uses kernel version 4\.4\.5 and hence is impacted\. Therefore, we recommend not using emr\-4\.6\.0 if you want to use st1 EBS volumes\. You can use emr\-4\.5\.0 or prior Amazon EMR releases with st1 without impact\. In addition, we provide the fix with future releases\.

### Python Defaults<a name="w3ab1c11c11c61b8"></a>

Python 3\.4 is now installed by default, but Python 2\.7 remains the system default\. You may configure Python 3\.4 as the system default using either a bootstrap action; you can use the configuration API to set PYSPARK\_PYTHON export to `/usr/bin/python3.4` in the `spark-env` classification to affect the Python version used by PySpark\.

### Java 8<a name="w3ab1c11c11c61c10"></a>

Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c61c12"></a>

+ Fixed an issue where application provisioning would sometimes randomly fail due to a generated password\.

+ Previously, `mysqld` was installed on all nodes\. Now, it is only installed on the master instance and only if the chosen application includes `mysql-server` as a component\. Currently, the following applications include the `mysql-server` component: HCatalog, Hive, Hue, Presto\-Sandbox, and Sqoop\-Sandbox\.

+ Changed `yarn.scheduler.maximum-allocation-vcores` to 80 from the default of 32, which fixes an issue introduced in emr\-4\.4\.0 that mainly occurs with Spark while using the `maximizeResourceAllocation` option in a cluster whose core instance type is one of a few large instance types that have the YARN vcores set higher than 32; namely c4\.8xlarge, cc2\.8xlarge, hs1\.8xlarge, i2\.8xlarge, m2\.4xlarge, r3\.8xlarge, d2\.8xlarge, or m4\.10xlarge were affected by this issue\.

+ s3\-dist\-cp now uses EMRFS for all Amazon S3 nominations and no longer stages to a temporary HDFS directory\.

+ Fixed an issue with exception handling for client\-side encryption multipart uploads\.

+ Added an option to allow users to change the Amazon S3 storage class\. By default this setting is `STANDARD`\. The `emrfs-site` configuration classification setting is `fs.s3.storageClass` and the possible values are `STANDARD`, `STANDARD_IA`, and `REDUCED_REDUNDANCY`\. For more information about storage classes, see [Storage Classes](http://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html) in the Amazon Simple Storage Service Developer Guide\. 

## Release 4\.5\.0<a name="w3ab1c11c11c63"></a>

Release date: April 4, 2016

### Features<a name="w3ab1c11c11c63b4"></a>

The following features are available in this release:

+ Upgraded to Spark 1\.6\.1

+ Upgraded to Hadoop 2\.7\.2

+ Upgraded to Presto 0\.140

+ Added AWS KMS support for Amazon S3 server\-side encryption\.

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c63b6"></a>

+ Fixed an issue where MySQL and Apache servers would not start after a node was rebooted\. 

+ Fixed an issue where IMPORT did not work correctly with non\-partitioned tables stored in Amazon S3

+ Fixed an issue with Presto where it requires the staging directory to be `/mnt/tmp` rather than `/tmp` when writing to Hive tables\.

## Release 4\.4\.0<a name="w3ab1c11c11c65"></a>

Release date: March 14, 2016

### Features<a name="w3ab1c11c11c65b4"></a>

The following features are available in this release:

+ Added HCatalog 1\.0\.0

+ Added Sqoop\-Sandbox 1\.4\.6

+ Upgraded to Presto 0\.136

+ Upgraded to Zeppelin 0\.5\.6

+ Upgraded to Mahout 0\.11\.1

+ Enabled `dynamicResourceAllocation` by default\.

+ Added a table of all configuration classifications for the release\. For more information, see the Configuration Classifications table in [Configuring Applications](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.

### Known Issues Resolved from Previous Releases<a name="w3ab1c11c11c65b6"></a>

+ Fixed an issue where the `maximizeResourceAllocation` setting would not reserve enough memory for YARN ApplicationMaster daemons\.

+ Fixed an issue encountered with a custom DNS\. If any entries in `resolve.conf` precede the custom entries provided, then the custom entries are not resolvable\. This behavior was affected by clusters in a VPC where the default VPC name server is inserted as the top entry in `resolve.conf`\.

+ Fixed an issue where the default Python moved to version 2\.7 and boto was not installed for that version\.

+ Fixed an issue where YARN containers and Spark applications would generate a unique Ganglia round robin database \(rrd\) file, which resulted in the first disk attached to the instance filling up\. Because of this fix, YARN container level metrics have been disabled and Spark application level metrics have been disabled\.

+ Fixed an issue in log pusher where it would delete all empty log folders\. The effect was that the Hive CLI was not able to log because log pusher was removing the empty `user` folder under `/var/log/hive`\.

+ Fixed an issue affecting Hive imports, which affected partitioning and resulted in an error during import\.

+ Fixed an issue where EMRFS and s3\-dist\-cp did not properly handle bucket names that contain periods\.

+ Changed a behavior in EMRFS so that in versioning\-enabled buckets the `_$folder$` marker file is not continuously created, which may contribute to improved performance for versioning\-enabled buckets\.

+ Changed the behavior in EMRFS such that it does not use instruction files except for cases where client\-side encryption is enabled\. If you want to delete instruction files while using client\-side encryption, you can set the emrfs\-site\.xml property, `fs.s3.cse.cryptoStorageMode.deleteInstructionFiles.enabled`, to true\. 

+ Changed YARN log aggregation to retain logs at the aggregation destination for two days\. The default destination is your cluster's HDFS storage\. If you want to change this duration, change the value of `yarn.log-aggregation.retain-seconds` using the `yarn-site` configuration classification when you create your cluster\. As always, you can save your application logs to Amazon S3 using the `log-uri` parameter when you create your cluster\.

### Patches Applied<a name="w3ab1c11c11c65b8"></a>

The following patches from open source projects were included in this release:

+ [HIVE\-9655](https://issues.apache.org/jira/browse/HIVE-9655)

+ [HIVE\-9183](https://issues.apache.org/jira/browse/HIVE-9183)

+ [HADOOP\-12810](https://issues.apache.org/jira/browse/HADOOP-12810)

## Release 4\.3\.0<a name="w3ab1c11c11c67"></a>

Release date: January 19, 2016

### Features<a name="w3ab1c11c11c67b4"></a>

The following features are available in this release:

+ Upgraded to Hadoop 2\.7\.1

+ Upgraded to Spark 1\.6\.0

+ Upgraded Ganglia to 3\.7\.2 

+ Upgraded Presto to 0\.130

Amazon EMR made some changes to `spark.dynamicAllocation.enabled` when it is set to true; it is false by default\. When set to true, this affects the defaults set by the `maximizeResourceAllocation` setting:

+ If `spark.dynamicAllocation.enabled` is set to true, `spark.executor.instances` is not set by `maximizeResourceAllocation`\.

+ The `spark.driver.memory` setting is now configured based on the instance types in the cluster in a similar way to how `spark.executors.memory` is set\. However, because the Spark driver application may run on either the master or one of the core instances \(for example, in YARN client and cluster modes, respectively\), the `spark.driver.memory` setting is set based on the instance type of the smaller instance type between these two instance groups\.

+ The `spark.default.parallelism` setting is now set at twice the number of CPU cores available for YARN containers\. In previous releases, this was half that value\.

+ The calculations for the memory overhead reserved for Spark YARN processes was adjusted to be more accurate, resulting in a small increase in the total amount of memory available to Spark \(that is, `spark.executor.memory`\)\.

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c67b6"></a>

+ YARN log aggregation is now enabled by default\.

+ Fixed an issue where logs would not be pushed to a cluster's Amazon S3 logs bucket when YARN log aggregation was enabled\.

+ YARN container sizes now have a new minimum of 32 across all node types\.

+ Fixed an issue with Ganglia that caused excessive disk I/O on the master node in large clusters\.

+ Fixed an issue that prevented applications logs from being pushed to Amazon S3 when a cluster is shutting down\.

+ Fixed an issue in EMRFS CLI that caused certain commands to fail\.

+ Fixed an issue with Zeppelin that prevented dependencies from being loaded in the underlying SparkContext\.

+ Fixed an issue that resulted from issuing a resize attempting to add instances\. 

+ Fixed an issue in Hive where CREATE TABLE AS SELECT makes excessive list calls to Amazon S3\. 

+ Fixed an issue where large clusters would not provision properly when Hue, Oozie, and Ganglia are installed\.

+ Fixed an issue in s3\-dist\-cp where it would return a zero exit code even if it failed with an error\.

### Patches Applied<a name="w3ab1c11c11c67b8"></a>

The following patches from open source projects were included in this release:

+ [OOZIE\-2402](https://issues.apache.org/jira/browse/OOZIE-2402)

+ [HIVE\-12502](https://issues.apache.org/jira/browse/HIVE-12502)

+ [HIVE\-10631](https://issues.apache.org/jira/browse/HIVE-10631)

+ [HIVE\-12213](https://issues.apache.org/jira/browse/HIVE-12213)

+ [HIVE\-10559](https://issues.apache.org/jira/browse/HIVE-10559)

+ [HIVE\-12715](https://issues.apache.org/jira/browse/HIVE-12715)

+ [HIVE\-10685](https://issues.apache.org/jira/browse/HIVE-10685)

## Release 4\.2\.0<a name="w3ab1c11c11c69"></a>

Release date: November 18, 2015

### Features<a name="w3ab1c11c11c69b4"></a>

The following features are available in this release:

+ Added Ganglia support

+ Upgraded to Spark 1\.5\.2

+ Upgraded to Presto 0\.125

+ Upgraded Oozie to 4\.2\.0

+ Upgraded Zeppelin to 0\.5\.5

+ Upgraded the AWS SDK for Java to 1\.10\.27

### Known Issues Resolved from the Previous Releases<a name="w3ab1c11c11c69b6"></a>

+ Fixed an issue with the EMRFS CLI where it did not use the default metadata table name\.

+ Fixed an issue encountered when using ORC\-backed tables in Amazon S3\.

+ Fixed an issue encountered with a Python version mismatch in the Spark configuration\.

+ Fixed an issue when a YARN node status fails to report because of DNS issues for clusters in a VPC\.

+ Fixed an issue encountered when YARN decommissioned nodes, resulting in hanged applications or the inability to schedule new applications\.

+ Fixed an issue encountered when clusters terminated with status TIMED\_OUT\_STARTING\.

+ Fixed an issue encountered when including the EMRFS Scala dependency in other builds\. The Scala dependency has been removed\.