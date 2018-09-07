# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.17\.0 Tab](emr-release-5x.md#emr-5170-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.17\.0 \(Latest\)<a name="emr-5170-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.17\.0\. Changes are relative to 5\.16\.0\.

Initial release date: August 30, 2018

**Upgrades**
+ Flink 1\.5\.2
+ HBase 1\.4\.6
+ Presto 0\.206

**New Features**
+ Added support for Tensorflow\. For more information, see [TensorFlow](emr-tensorflow.md)\.

**Changes, Enhancements, and Resolved Issues**
+ JupyterHub
  + Added support for notebook persistence in Amazon S3\. For more information, see [Configuring Persistence for Notebooks in Amazon S3](emr-jupyterhub-s3.md)\.
+ Spark
  + Added support for [S3 Select](aws.amazon.comblogs/aws/s3-glacier-select/)\. For more information, see [Using S3 Select with Spark to Improve Performance](emr-spark-s3select.md)\.

**Known Issues**
+ When you create a kerberized cluster with Livy installed, Livy fails with an error that simple authentication is not enabled\. Rebooting the Livy server resolves the issue\. As a workaround, add a step during cluster creation that runs `sudo restart livy-server` on the master node\.