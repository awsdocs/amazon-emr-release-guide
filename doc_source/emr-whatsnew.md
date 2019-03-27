# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.22\.0 Tab](emr-release-5x.md#emr-5220-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.22\.0 \(Latest\)<a name="emr-5220-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.22\.0\. Changes are relative to 5\.21\.0\.

Initial release date: March 20, 2019

**Upgrades**
+ Flink 1\.7\.1
+ HBase 1\.4\.9
+ Oozie 5\.1\.0
+ Phoenix 4\.14\.1
+ Zeppelin 0\.8\.1
+ Connectors and drivers:
  + DynamoDB Connector 4\.8\.0
  + MariaDB Connector 2\.2\.6
  + Amazon Redshift JDBC Driver 1\.2\.20\.1043

**New Features**
+ Modified the default EBS configuration for EC2 instance types with EBS\-only storage\. When you create a cluster using Amazon EMR release version 5\.22\.0 and later, the default amount of EBS storage increases based on the size of the instance\. In addition, we split increased storage across multiple volumes, giving increased IOPS performance\. If you want to use a different EBS instance storage configuration, you can specify it when you create an EMR cluster or add nodes to an existing cluster\. For more information about the amount of storage and number of volumes allocated by default for each instance type, see [Default EBS Storage for Instances](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-storage.html#emr-plan-storage-ebs-storage-default) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Introduced a new configuration property for Spark on YARN, `spark.yarn.executor.memoryOverheadFactor`\. The value of this property is a scale factor that sets the value of memory overhead to a percentage of executor memory, with a minimum of 384 MB\. If memory overhead is set explicitly using `spark.yarn.executor.memoryOverhead`, this property has no effect\. The default value is `0.1875`, representing 18\.75%\. This default for Amazon EMR leaves more space in YARN containers for executor memory overhead than the 10% default set internally by Spark\. The Amazon EMR default of 18\.75% empirically showed fewer memory\-related failures in TPC\-DS benchmarks\.
  + Backported [SPARK\-26316](https://issues.apache.org/jira/browse/SPARK-26316) to improve performance\.