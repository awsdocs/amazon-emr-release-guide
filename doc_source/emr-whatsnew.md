# What's new?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR 6\.x series and 5\.x series\. These release notes are also available on the [Release 6\.5\.0 Tab](emr-650-release.md) and [Release 5\.34\.0 Tab](emr-5340-release.md), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR what's new history](emr-whatsnew-history.md)\.

**Note**  
Twenty\-five previous Amazon EMR release versions now use AWS Signature Version 4 to authenticate requests to Amazon S3\. The use of AWS Signature version 2 is being phased out and new S3 buckets created after June 24, 2020 will not support Signature Version 2 signed requests\. Existing buckets will continue to support Signature Version 2\. We recommend migrating to an Amazon EMR release that supports Signature Version 4 so you can continue accessing new S3 buckets and avoid any potential interruption to your workloads\.  
The following EMR releases are now available that supports Signature Version 4: emr\-4\.7\.4, emr\-4\.8\.5, emr\-4\.9\.6, emr\-4\.10\.1, emr\-5\.1\.1, emr\-5\.2\.3, emr\-5\.3\.2, emr\-5\.4\.1, emr\-5\.5\.4, emr\-5\.6\.1, emr\-5\.7\.1, emr\-5\.8\.3, emr\-5\.9\.1, emr\-5\.10\.1, emr\-5\.11\.4, emr\-5\.12\.3, emr\-5\.13\.1, emr\-5\.14\.2, emr\-5\.15\.1, emr\-5\.16\.1, emr\-5\.17\.2, emr\-5\.18\.1, emr\-5\.19\.1, emr\-5\.20\.1, and emr\-5\.21\.2\. EMR version 5\.22\.0 and later already support Signature Version 4\.  
You do not need to change your application code to use Signature Version 4 if you are using Amazon EMR applications, such as Apache Spark, Apache Hive, Presto, etc\. If you are using custom applications, which are not included with Amazon EMR, you may need to update your code to use Signature Version 4\. For more information about what updates may be required, see [Moving from Signature Version 2 to Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html#UsingAWSSDK-move-to-Sig4)\.

## Release 6\.5\.0 \(latest version of Amazon EMR 6\.x series\)<a name="emr-650-whatsnew"></a>

New Amazon EMR release versions are made available in different Regions over a period of several days, beginning with the first Region on the initial release date\. The latest release version may not be available in your Region during this period\.

The following release notes include information for Amazon EMR release version 6\.5\.0\. Changes are relative to 6\.4\.0\.

Initial release date: January 20, 2022

**New Features**
+ Support for Apache Iceberg open table format for huge analytic datasets\.
+ Support for ranger\-trino\-plugin 2\.0\.1\-amzn\-1
+ Support for toree 0\.5\.0

**Changes, Enhancements, and Resolved Issues**
+ Amazon EMR 6\.5 release version now supports Apache Iceberg 0\.12\.0, and provides runtime improvements with Amazon EMR Runtime for Apache Spark, Amazon EMR Runtime for Presto, and Amazon EMR Runtime for Apache Hive\.
+ [Apache Iceberg](https://iceberg.apache.org/) is an open table format for large data sets in Amazon S3 and provides fast query performance over large tables, atomic commits, concurrent writes, and SQL\-compatible table evolution\. With EMR 6\.5, you can use Apache Spark 3\.1\.2 with the Iceberg table format\.
+ Apache Hudi 0\.9 adds Spark SQL DDL and DML support\. This allows you to create, upsert Hudi tables using just SQL statements\. Apache Hudi 0\.9 also includes query side and writer side performance improvements\.
+ Amazon EMR Runtime for Apache Hive improves Apache Hive performance on Amazon S3 by removing rename operations during staging operations, and improves performance for metastore check \(MSCK\) commands used for repairing tables\.

**Known Issues**
+ Hbase bundle clusters in high availability \(HA\) fail to provision with the default volume size and instance type\. The workaround for this issue is to increase the root volume size\.

## Release 5\.34\.0 \(latest version of Amazon EMR 5\.x series\)<a name="emr-5340-whatsnew"></a>

New Amazon EMR release versions are made available in different Regions over a period of several days, beginning with the first Region on the initial release date\. The latest release version may not be available in your Region during this period\.