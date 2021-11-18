# Improve Spark performance with Amazon S3<a name="emr-spark-s3-performance"></a>

Amazon EMR offers features to help optimize performance when using Spark to query, read and write data saved in Amazon S3\.

[S3 Select](https://aws.amazon.com/blogs/aws/s3-glacier-select/) can improve query performance for CSV and JSON files in some applications by "pushing down" processing to Amazon S3\.

The EMRFS S3\-optimized committer is an alternative to the [OutputCommitter](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/OutputCommitter.html) class, which uses the multipart uploads feature of EMRFS to improve performance when writing Parquet files to Amazon S3 using Spark SQL, DataFrames, and Datasets\.

**Topics**
+ [Use S3 Select with Spark to improve query performance](emr-spark-s3select.md)
+ [Use the EMRFS S3\-optimized committer](emr-spark-s3-optimized-committer.md)
+ [Retry Amazon S3 requests with EMRFS](emr-spark-emrfs-retry.md)