# Enable the EMRFS S3\-optimized committer for Amazon EMR 5\.19\.0<a name="emr-spark-committer-enable"></a>

If you are using Amazon EMR 5\.19\.0 , you can manually set the `spark.sql.parquet.fs.optimized.committer.optimization-enabled` property to `true` when you create a cluster or from within Spark if you are using Amazon EMR\.

## Enabling the EMRFS S3\-optimized committer when creating a cluster<a name="w197aac53c47c13c17b5"></a>

Use the `spark-defaults` configuration classification to set the `spark.sql.parquet.fs.optimized.committer.optimization-enabled` property to `true`\. For more information, see [Configure applications](emr-configure-apps.md)\.

## Enabling the EMRFS S3\-optimized committer from Spark<a name="w197aac53c47c13c17b7"></a>

You can set `spark.sql.parquet.fs.optimized.committer.optimization-enabled` to `true` by hard\-coding it in a `SparkConf`, passing it as a `--conf` parameter in the Spark shell or `spark-submit` and `spark-sql` tools, or in `conf/spark-defaults.conf`\. For more information, see [Spark configuration](https://spark.apache.org/docs/latest/configuration.html) in Apache Spark documentation\.

The following example shows how to enable the committer while running a spark\-sql command\.

```
spark-sql \
  --conf spark.sql.parquet.fs.optimized.committer.optimization-enabled=true \
  -e "INSERT OVERWRITE TABLE target_table SELECT * FROM source_table;"
```