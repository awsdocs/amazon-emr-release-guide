# Using the EMRFS S3\-optimized Committer<a name="emr-spark-s3-optimized-committer"></a>

The EMRFS S3\-optimized committer is an alternative [OutputCommitter](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/mapreduce/OutputCommitter.html) implementation that is optimized for writing files to an Amazon S3 location when using EMRFS\. The committer is available with Amazon EMR release version 5\.19\.0 and later, and is enabled by default with Amazon EMR 5\.20\.0 and later\. The EMRFS S3\-optimized committer is used for Spark jobs that use Spark SQL, DataFrames, or Datasets to write Parquet files\. The EMRFS S3\-optimized committer has the following benefits:
+ Improves application performance by avoiding list and rename operations done in Amazon S3 during job and task commit phases\. 
+ Lets you safely enable the speculative execution of idempotent tasks in Spark jobs to help reduce the performance impact of task stragglers\.
+ Avoids issues that can occur with Amazon S3 eventual consistency during job and task commit phases, and helps improve job correctness under task failure conditions\.

The committer does not take effect when writing to HDFS, using the S3A file system, using an output format other than Parquet \(such as ORC or text\), or when using MapReduce or Spark's RDD API\.

The EMRFS S3\-optimized committer is used for Hive metastore Parquet tables as long as Spark's built\-in Parquet support is used\. This is enabled by default in Spark \(`spark.sql.hive.convertMetastoreParquet` set to `true`\)\. For more information, see [Hive metastore Parquet table conversion](https://spark.apache.org/docs/latest/sql-data-sources-parquet.html#hive-metastore-parquet-table-conversion) in the Apache Spark SQL, DataFrames and Datasets Guide\. A known limitation is that Spark's built\-in Parquet support is not used with partitioned Hive tables\. Because of this, the EMRFS S3\-optimized committer is not used for such tables\.

## The EMRFS S3\-optimized Committer and Multipart Uploads<a name="emr-spark-committer-multipart"></a>

To use the EMRFS S3\-optimized committer, multipart uploads must be enabled in Amazon EMR\. Multipart uploads are enabled by default\. You can re\-enable it if required\. For more information, see [Configure Multipart Upload for Amazon S3](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-upload-s3.html#Config_Multipart) in the *Amazon EMR Management Guide*\. 

The EMRFS S3\-optimized committer uses the transaction\-like characteristics of multipart uploads to ensure files written by task attempts only appear in the job's output location upon task commit\. By using multipart uploads in this way, the committer improves task commit performance over the default FileOutputCommitter algorithm version 2\. When using the EMRFS S3\-optimized committer, there are some key differences from traditional multipart upload behavior to consider:
+ Multipart uploads are always performed regardless of the file size\. This differs from the default behavior of EMRFS, where the `fs.s3n.multipart.uploads.split.size` property controls the file size at which multipart uploads are triggered\.
+ Multipart uploads are left in an incomplete state for a longer period of time until the task commits or aborts\. This differs from the default behavior of EMRFS where a multipart upload completes when a task finishes writing a given file\.

Because of these differences, if a Spark Executor JVM crashes or is killed while tasks are running and writing data to Amazon S3, incomplete multipart uploads are more likely to be left behind\. For this reason, when you use the EMRFS S3\-optimized committer, be sure to follow the best practices for managing failed multipart uploads\. For more information, see [Best Practices](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-upload-s3.html#emr-bucket-bestpractices) for working with Amazon S3 buckets in the *Amazon EMR Management Guide*\.

## Job Tuning Considerations<a name="emr-spark-committer-tuning"></a>

The EMRFS S3\-optimized committer consumes a small amount of memory for each file written by a task attempt until the task gets committed or aborted\. In most jobs, the amount of memory consumed is negligible\. For jobs that have long\-running tasks that write a large number of files, the memory that the committer consumes may be noticeable and require adjustments to the memory allocated for Spark executors\. You can tune executor memory using the `spark.executor.memory` property\. As a guideline, a single task writing 100,000 files would typically require an additional 100MB of memory\. For more information, see [Application Properties](https://spark.apache.org/docs/latest/configuration.html#application-properties) in the Apache Spark Configuration documentation\.

## Enabling the EMRFS S3\-optimized Committer for Amazon EMR 5\.19\.0<a name="emr-spark-committer-enable"></a>

With Amazon EMR 5\.20\.0 and later, the EMRFS S3\-optimized committer is enabled by default\. The `spark.sql.parquet.fs.optimized.committer.optimization-enabled` property is a boolean that enables and disables the committer\. You can set this property to `true` when you create a cluster or from within Spark if you are using Amazon EMR 5\.19\.0\. You can disable the committer by setting the property to `false` in the same way\.

### Enabling the EMRFS S3\-optimized Committer when Creating a Cluster Using Amazon EMR 5\.19\.0<a name="w3ab1c48c35c13c15b5"></a>

Use the `spark-defaults` configuration classification to set the `spark.sql.parquet.fs.optimized.committer.optimization-enabled` property to `true`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

### Enabling the EMRFS S3\-optimized Committer from Spark Using Amazon EMR 5\.19\.0<a name="w3ab1c48c35c13c15b7"></a>

You can set `spark.sql.parquet.fs.optimized.committer.optimization-enabled` to `true` by hard\-coding it in a `SparkConf`, passing it as a `--conf` parameter in the Spark shell or `spark-submit` and `spark-sql` tools, or in `conf/spark-defaults.conf`\. For more information, see [Spark Configuration](https://spark.apache.org/docs/latest/configuration.html) in Apache Spark documentation\.

The following example shows how to enable the committer while running a spark\-sql command\.

```
spark-sql \
  --conf spark.sql.parquet.fs.optimized.committer.optimization-enabled=true \
  -e "INSERT OVERWRITE TABLE target_table SELECT * FROM source_table;"
```