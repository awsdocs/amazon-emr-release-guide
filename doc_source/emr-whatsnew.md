# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.26\.0 Tab](emr-release-5x.md#emr-5260-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.26\.0 \(Latest\)<a name="emr-5260-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.26\.0\. Changes are relative to 5\.25\.0\.

Initial release date: Aug 8, 2019

Last updated date: Aug 19, 2019

**Upgrades**
+ AWS SDK for Java 1\.11\.595
+ HBase 1\.4\.10
+ Phoenix 4\.14\.2
+ Connectors and drivers:
  + DynamoDB Connector 4\.11\.0
  + MariaDB Connector 2\.4\.2
  + Amazon Redshift JDBC Driver 1\.2\.32\.1056

**New Features**
+ \(Beta\) With Amazon EMR 5\.26\.0, you can launch a cluster that integrates with Lake Formation\. This integration provides fine\-grained, column\-level access to databases and tables in the AWS Glue Data Catalog\. It also enables federated single sign\-on to EMR Notebooks or Apache Zeppelin from an enterprise identity system\. For more information, see [Integrating Amazon EMR with AWS Lake Formation \(Beta\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-lake-formation.html)\.
+ \(Aug 19, 2019\) Amazon EMR block public access is now available with all Amazon EMR releases that support security groups\. Block public access is an account\-wide setting applied to each AWS Region\. Block public access prevents a cluster from launching when any security group associated with the cluster has a rule that allows inbound traffic from IPv4 0\.0\.0\.0/0 or IPv6 ::/0 \(public access\) on a port, unless a port is specified as an exception\. Port 22 is an exception by default\. For more information, see [Using Amazon EMR Block Public Access](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-block-public-access.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ EMR Notebooks
  + With EMR 5\.26\.0 and later, EMR Notebooks supports notebook\-scoped Python libraries in addition to the default Python libraries\. You can install notebook\-scoped libraries from within the notebook editor without having to re\-create a cluster or re\-attach a notebook to a cluster\. Notebook\-scoped libraries are created in a Python virtual environment, so they apply only to the current notebook session\. This allows you to isolate notebook dependencies\. For more information, see [Using Notebook Scoped Libraries](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-scoped-libraries.html) in the *Amazon EMR Management Guide*\.
+ EMRFS
  + You can enable an ETag verification feature \(Beta\) by setting `fs.s3.consistent.metadata.etag.verification.enabled` to `true`\. With this feature, EMRFS uses Amazon S3 ETags to verify that objects being read are the latest available version\. This feature is helpful for read\-after\-update use cases in which files on Amazon S3 are overwritten while retaining the same name\. This ETag verification capability currently does not work with S3 Select\. For more information, see [Configure Consistent View](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emrfs-configure-consistent-view.html)\.
+ Spark
  + The following optimizations are now enabled by default: dynamic partition pruning, DISTINCT before INTERSECT, improvements in SQL plan statistics inference for JOIN followed by DISTINCT queries, flattening scalar subqueries, optimized join reorder, and bloom filter join\. For more information, see [Optimizing Spark Performance](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-performance.html)\.
  + Improved whole stage code generation for Sort Merge Join\.
  + Improved query fragment and subquery reuse\.
  + Improvements to pre\-allocate executors on Spark start up\.
  + Bloom filter joins are no longer applied when the smaller side of the join includes a broadcast hint\.
+ Tez
  + Resolved an issue with Tez\. Tez UI now works on an EMR cluster with multiple master nodes\.

**Known Issues**
+ The improved whole stage code generation capabilities for Sort Merge Join can increase memory pressure when enabled\. This optimization improves performance, but may result in job retries or failures if the `spark.yarn.executor.memoryOverheadFactor` is not tuned to provide enough memory\. To disable this feature, set `spark.sql.sortMergeJoinExec.extendedCodegen.enabled` to false\.