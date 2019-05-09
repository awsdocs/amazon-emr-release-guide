# Using the EMRFS S3\-optimized Committer<a name="emr-spark-s3-optimized-committer"></a>

The EMRFS S3\-optimized committer is an alternative [OutputCommitter](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/OutputCommitter.html) implementation that is optimized for writing files to Amazon S3 when using EMRFS\. The committer is available with Amazon EMR release version 5\.19\.0 and later, and is enabled by default with Amazon EMR 5\.20\.0 and later\. The committer is used for Spark jobs that use Spark SQL, DataFrames, or Datasets to write Parquet files\. There are circumstances under which the committer is not used\. For more information, see [Requirements for the EMRFS S3\-Optimized Committer](emr-spark-committer-reqs.md)\.

The EMRFS S3\-optimized committer has the following benefits:
+ Improves application performance by avoiding list and rename operations done in Amazon S3 during job and task commit phases\. 
+ Avoids issues that can occur with Amazon S3 eventual consistency during job and task commit phases, and helps improve job correctness under task failure conditions\.

**Topics**
+ [Requirements for the EMRFS S3\-Optimized Committer](emr-spark-committer-reqs.md)
+ [The EMRFS S3\-optimized Committer and Multipart Uploads](emr-spark-committer-multipart.md)
+ [Job Tuning Considerations](emr-spark-committer-tuning.md)
+ [Enabling the EMRFS S3\-optimized Committer for Amazon EMR 5\.19\.0](emr-spark-committer-enable.md)