# Use the EMRFS S3\-optimized committer<a name="emr-spark-s3-optimized-committer"></a>

The EMRFS S3\-optimized committer is an alternative [OutputCommitter](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/OutputCommitter.html) implementation that is optimized for writing files to Amazon S3 when using EMRFS\. The committer is available with Amazon EMR release version 5\.19\.0 and later, and is enabled by default with Amazon EMR 5\.20\.0 and later\. The committer is used for Spark jobs that use Spark SQL, DataFrames, or Datasets\. Starting with Amazon EMR 6\.4\.0, this committer can be used for all common formats including parquet, ORC, and text\-based formats \(including CSV and JSON\)\. For release versions prior to Amazon EMR 6\.4\.0, only the Parquet format is supported\. There are circumstances under which the committer is not used\. For more information, see [Requirements for the EMRFS S3\-optimized committer](emr-spark-committer-reqs.md)\.

The EMRFS S3\-optimized committer has the following benefits:
+ Improves application performance by avoiding list and rename operations done in Amazon S3 during job and task commit phases\. 
+ Avoids issues that can occur with Amazon S3 eventual consistency during job and task commit phases, and helps improve job correctness under task failure conditions\.

**Topics**
+ [Requirements for the EMRFS S3\-optimized committer](emr-spark-committer-reqs.md)
+ [The EMRFS S3\-optimized committer and multipart uploads](emr-spark-committer-multipart.md)
+ [Job tuning considerations](emr-spark-committer-tuning.md)
+ [Enable the EMRFS S3\-optimized committer for Amazon EMR 5\.19\.0](emr-spark-committer-enable.md)