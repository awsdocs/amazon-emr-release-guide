# Create a cluster with Iceberg installed<a name="emr-iceberg-create-cluster"></a>

You can create a cluster using the AWS Management Console, the AWS CLI, or the Amazon EMR API\.

To use Iceberg on Amazon EMR, create a cluster with the following classification:

```
[{
    "Classification":"iceberg-defaults",
    "Properties":{"iceberg.enabled":"true"}
}]
```

Alternatively, you can create an EMR cluster including the Spark application and include the file `/usr/share/aws/iceberg/lib/iceberg-spark3-runtime.jar` as a JAR dependency in a Spark job\.

**Working with an Iceberg dataset**

The notebook can initialize a Spark session and write to an Iceberg Table \(in append mode\)\.

**Initialize a Spark session for Iceberg **

spark\-shell:

```
spark-shell \
--conf "spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions"\
--conf "spark.sql.catalog.spark_catalog=org.apache.iceberg.spark.SparkSessionCatalog" \
--conf "spark.sql.catalog.spark_catalog.type=hive" \
--conf "spark.sql.catalog.spark_catalog.warehouse=s3://>bucket</>prefix</"
```

spark\-submit:

```
spark-submit \
--conf "spark.sql.extensions=org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions"\
--conf "spark.sql.catalog.spark_catalog=org.apache.iceberg.spark.SparkSessionCatalog" \
--conf "spark.sql.catalog.spark_catalog.type=hive" \
--conf "spark.sql.catalog.spark_catalog.warehouse=s3://<bucket>/<prefix>/"
```

EMR Studio Notebooks:

```
%%configure -f
{
"conf":{
    "spark.sql.extensions":"org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions",
    "spark.sql.catalog.spark_catalog":"org.apache.iceberg.spark.SparkSessionCatalog",
    "spark.sql.catalog.spark_catalog.type":"hive",
    "spark.sql.catalog.dev":"org.apache.iceberg.spark.SparkCatalog",
    "spark.sql.catalog.dev.type":"hadoop",
    "spark.sql.catalog.dev.warehouse":"s3://<bucket>/<prefix>/"
    }
}
```

**Write to an Iceberg table**

PySpark:

```
## Create a DataFrame
data = spark.createDataFrame([
 ("100", "2015-01-01", "2015-01-01T13:51:39.340396Z"),
 ("101", "2015-01-01", "2015-01-01T12:14:58.597216Z"),
 ("102", "2015-01-01", "2015-01-01T13:51:40.417052Z"),
 ("103", "2015-01-01", "2015-01-01T13:51:40.519832Z")
],["id", "creation_date", "last_update_time"])

## Write a DataFrame as a Iceberg dataset to the S3 location
spark.sql("""CREATE TABLE IF NOT EXISTS dev.db.iceberg_table (id string, 
                                       creation_date string,
                                       last_update_time string)
USING iceberg
location  's3://<bucket>/<prefix>/dev_db_iceberg_table'""")

data.writeTo("dev.db.iceberg_table").append()
```

Scala:

```
import org.apache.spark.sql.SaveMode
import org.apache.spark.sql.functions._

// Create a DataFrame
val data = Seq(
("100", "2015-01-01", "2015-01-01T13:51:39.340396Z"),
("101", "2015-01-01", "2015-01-01T12:14:58.597216Z"),
("102", "2015-01-01", "2015-01-01T13:51:40.417052Z"),
("103", "2015-01-01", "2015-01-01T13:51:40.519832Z")
).toDF("id", "creation_date", "last_update_time")

// Write a DataFrame as a Iceberg dataset to the S3 location
spark.sql("""CREATE TABLE IF NOT EXISTS dev.db.iceberg_table (id string,
creation_date string,
last_update_time string)
USING iceberg
location 's3://<bucket>/<prefix>/dev_db_iceberg_table'""")

data.writeTo("dev.db.iceberg_table").append()
```

**Read from an Iceberg table**

PySpark:

```
df = spark.read.format("iceberg").load("dev.db.iceberg_table")
df.show()
```

Scala:

```
val df = spark.read.format("iceberg").load("dev.db.iceberg_table")
df.show()
```

Spark SQL:

```
SELECT * from dev.db.iceberg_table LIMIT 10
```