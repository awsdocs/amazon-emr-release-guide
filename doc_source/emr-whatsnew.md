# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.12\.0 Tab](emr-release-5x.md#emr-5120-release), along with the application versions, component versions, and available configuration classifications for this release\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.12\.0 \(Latest\)<a name="emr-5120-whatsnew"></a>

The following release notes include information for the Amazon EMR release version 5\.12\.0\. Changes are relative to 5\.11\.1\.

**Upgrades**

+ AWS SDK for Java 1\.11\.238 ⇒ 1\.11\.267\. For more information, see the [AWS SDK for Java Change Log](https://github.com/aws/aws-sdk-java/blob/master/CHANGELOG.md) on GitHub\.

+ Hadoop 2\.7\.3 ⇒ 2\.8\.3\. For more information, see [Apache Hadoop Releases](http://hadoop.apache.org/releases.html)\.

+ Flink 1\.3\.2 ⇒ 1\.4\.0\. For more information, see the [Apache Flink 1\.4\.0 Release Announcement](https://flink.apache.org/news/2017/12/12/release-1.4.0.html)\.

+ HBase 1\.3\.1 ⇒ 1\.4\.0\. For more information, see the [HBase Release Announcement](http://mail-archives.apache.org/mod_mbox/www-announce/201712.mbox/%3CCA+RK=_AU+tB=7SU1HRbeKVEd-sKA5WcJo3oa43vQ6PMB3L9pgQ@mail.gmail.com%3E)\.

+ Hue 4\.0\.1 ⇒ 4\.1\.0\. For more information, see the [Release Notes](http://cloudera.github.io/hue/latest/release-notes/release-notes-4.1.0.html)\.

+ MxNet 0\.12\.0 ⇒ 1\.0\.0\. For more information, see the [MXNet Change Log](https://github.com/apache/incubator-mxnet/releases/tag/1.0.0) on GitHub\.

+ Presto 0\.187 ⇒ 0\.188\. For more information, see the [Release Notes](https://prestodb.io/docs/current/release/release-0.188.html)\.

**Changes, Enhancements, and Resolved Issues**

+ **Hadoop**

  + The `yarn.resourcemanager.decommissioning.timeout` property has changed to `yarn.resourcemanager.nodemanager-graceful-decommission-timeout-secs`\. You can use this property to customize cluster scale\-down\. For more information, see [Cluster Scale\-Down](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scaledown-behavior.html) in the *Amazon EMR Management Guide*\.

  + The Hadoop CLI added the `-d` option to the `cp` \(copy\) command, which specifies direct copy\. You can use this to avoid creating an intermediary `.COPYING` file, which makes copying data between Amazon S3 faster\. For more information, see [HADOOP\-12384](https://issues.apache.org/jira/browse/HADOOP-12384)\.

+ **Pig**

  + Added the `pig-env` configuration classification, which simplifies the configuration of Pig environment properties\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

+ **Presto**

  + Added the `presto-connector-redshift` configuration classification, which you can use to configure values in the Presto `redshift.properties` configuration file\. For more information, see [Redshift Connector](https://prestodb.io/docs/current/connector/redshift.html) in Presto documentation, and [Configuring Applications](emr-configure-apps.md)\.

  + Presto support for EMRFS has been added and is the default configuration\. Earlier Amazon EMR release versions used PrestoS3FileSystem, which was the only option\. For more information, see [EMRFS and PrestoS3FileSystem Configuration](emr-presto-considerations.md#emr-presto-prestos3)\.

+ **Spark**

  + Backported [SPARK\-22036: BigDecimal multiplication sometimes returns null](https://issues.apache.org/jira/browse/SPARK-22036)\.

**Known Issues**

+ MXNet does not include OpenCV libraries\.

+ SparkR is not available for clusters created using a custom AMI because R is not installed by default on cluster nodes\.