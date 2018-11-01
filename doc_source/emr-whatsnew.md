# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.18\.0 Tab](emr-release-5x.md#emr-5180-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.18\.0 \(Latest\)<a name="emr-5180-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.18\.0\. Changes are relative to 5\.17\.0\.

Initial release date: October 24, 2018

**Upgrades**
+ Flink 1\.6\.0
+ HBase 1\.4\.7
+ Presto 0\.210
+ Spark 2\.3\.2
+ Zeppelin 0\.8\.0

**New Features**
+ Beginning with Amazon EMR 5\.18\.0, you can use the Amazon EMR artifact repository to build your job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions\. For more information, see [Checking Dependencies Using the Amazon EMR Artifact Repository](emr-artifact-repository.md)\.

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Added support for S3 Select\. For more information, see [Using S3 Select with Hive to Improve Performance](emr-hive-s3select.md)\.
+ Presto
  + Added support for [S3 Select](aws.amazon.comblogs/aws/s3-glacier-select/) Pushdown\. For more information, see [Using S3 Select Pushdown with Presto to Improve Performance](emr-presto-s3select.md)\.
+ Spark
  + The default log4j configuration for Spark has been changed to roll container logs hourly for Spark streaming jobs\. This helps prevent the deletion of logs for long\-running Spark streaming jobs\.