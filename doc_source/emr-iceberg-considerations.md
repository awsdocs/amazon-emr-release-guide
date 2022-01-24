# Considerations and limitations for using Iceberg on Amazon EMR<a name="emr-iceberg-considerations"></a>
+ If you want to use Trino with Iceberg, EMR 6\.5 does not offer the [ Trino Iceberg Catalog](https://trino.io/docs/current/connector/iceberg.html#configuration) support for Iceberg natively\. Trino needs Iceberg v0\.11, so we recommend launching a different Amazon EMR cluster for Trino from the Spark cluster and including Iceberg v0\.11 on that cluster\. 
+ To use the AWS Glue Catalog as the Metastore for Iceberg tables, set the Spark configuration properties as below:

  ```
  spark-submit \
      --conf spark.sql.catalog.my_catalog=org.apache.iceberg.spark.SparkCatalog \
      --conf spark.sql.catalog.my_catalog.warehouse=s3://<bucket>/<prefix> \
      --conf spark.sql.catalog.my_catalog.catalog-impl=org.apache.iceberg.aws.glue.GlueCatalog \
      --conf spark.sql.catalog.my_catalog.io-impl=org.apache.iceberg.aws.s3.S3FileIO \
      --conf spark.sql.catalog.my_catalog.lock-impl=org.apache.iceberg.aws.glue.DynamoLockManager \
      --conf spark.sql.catalog.my_catalog.lock.table=myGlueLockTable
  ```