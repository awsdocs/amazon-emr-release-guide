# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.20\.0 Tab](emr-release-5x.md#emr-5200-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.20\.0 \(Latest\)<a name="emr-5200-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.20\.0\. Changes are relative to 5\.19\.0\.

Initial release date: December 18, 2018

Last updated date: January 22, 2019

**Upgrades**
+ Flink 1\.6\.2
+ HBase 1\.4\.8
+ Hive 2\.3\.4
+ Hue 4\.3\.0
+ MXNet 1\.3\.1
+ Presto 0\.214
+ Spark 2\.4\.0
+ TensorFlow 1\.12\.0
+ Tez 0\.9\.1
+ AWS SDK for Java 1\.11\.461

**New Features**
+ \(January 22, 2019\) Kerberos in Amazon EMR has been improved to support authenticating principals from an external KDC\. This centralizes principal management because multiple clusters can share a single, external KDC\. In addition, the external KDC can have a cross\-realm trust with an Active Directory domain\. This allows all clusters to authenticate principals from Active Directory\. For more information, see [Use Kerberos Authentication](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ Default Amazon Linux AMI for Amazon EMR
  + Python3 package was upgraded from python 3\.4 to 3\.6\.
+ The EMRFS S3\-optimized committer 
  + The EMRFS S3\-optimized committer is now enabled by default, which improves write performance\. For more information, see [Using the EMRFS S3\-optimized Committer](emr-spark-s3-optimized-committer.md)\.
+ Hive
  + Backported [HIVE\-16686](https://issues.apache.org/jira/browse/HIVE-16686)\.
+ Glue with Spark and Hive
  + In EMR 5\.20\.0 or later, parallel partition pruning is enabled automatically for Spark and Hive when AWS Glue Data Catalog is used as the metastore\. This change significantly reduces query planning time by executing multiple requests in parallel to retrieve partitions\. The total number of segments that can be executed concurrently range between 1 and 10\. The default value is 5, which is a recommended setting\. You can change it by specifying the property `aws.glue.partition.num.segments` in `hive-site` configuration classification\. If throttling occurs, you can turn off the feature by changing the value to 1\. For more information, see [AWS Glue Segment Structure](http://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-catalog-partitions.html#aws-glue-api-catalog-partitions-Segment)\.