# Work with a Hudi Dataset<a name="emr-hudi-work-with-dataset"></a>

Hudi supports inserting, updating, and deleting data in Hudi datasets through Spark\. For more information, see [Writing Hudi Tables](https://hudi.apache.org/docs/writing_data.html) in Apache Hudi documentation\.

The following examples demonstrate how to launch the interactive Spark shell, use Spark submit, or use Amazon EMR Notebooks to work with Hudi on Amazon EMR\. You can also use the Hudi DeltaStreamer utility or other tools to write to a dataset\. Throughout this section, the examples demonstrate working with datasets using the Spark shell while connected to the master node using SSH as the default `hadoop` user\.

**Note**  
Hudi 0\.6\.0 includes the spark\-avro package as a dependency under a different name\. You don't have to include the `spark-avro.jar` in your configuration when you use EMR 5\.31\.0 and later\.

------
#### [ spark\-shell ]

**To open the Spark shell on the master node**

1. Connect to the master node using SSH\. For more information, see [Connect to the Master Node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. Enter the following command to launch the Spark shell\. To use the PySpark shell, replace *spark\-shell* with *pyspark*\.

   ```
   spark-shell \
   --conf "spark.serializer=org.apache.spark.serializer.KryoSerializer" \
   --conf "spark.sql.hive.convertMetastoreParquet=false" \
   --jars /usr/lib/hudi/hudi-spark-bundle.jar,/usr/lib/spark/external/lib/spark-avro.jar
   ```

------
#### [ spark\-submit ]

To submit a Spark application that uses Hudi, make sure to pass the following parameters to spark\-submit\.

```
spark-submit \
--conf "spark.serializer=org.apache.spark.serializer.KryoSerializer"\
--conf "spark.sql.hive.convertMetastoreParquet=false" \
--jars /usr/lib/hudi/hudi-spark-bundle.jar,/usr/lib/spark/external/lib/spark-avro.jar
```

------
#### [ Amazon EMR Notebooks ]

To use Hudi with Amazon EMR Notebooks, you must first copy the Hudi jar files from the local file system to HDFS on the master node of the notebook cluster\. You then use the notebook editor to configure your EMR notebook to use Hudi\.

**To use Hudi with Amazon EMR Notebooks**

1. Create and launch a cluster for Amazon EMR Notebooks\. For more information, see [Creating Amazon EMR Clusters for Notebooks](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-cluster.html) in the *Amazon EMR Management Guide*\.

1. Connect to the master node of the cluster using SSH and then copy the jar files from the local filesystem to HDFS as shown in the following examples\. In the example, we create a directory in HDFS for clarity of file management\. You can choose your own destination in HDFS, if desired\.

   ```
   hdfs dfs -mkdir -p /apps/hudi/lib
   ```

   ```
   hdfs dfs -copyFromLocal /usr/lib/hudi/hudi-spark-bundle.jar /apps/hudi/lib/hudi-spark-bundle.jar
   ```

   ```
   hdfs dfs -copyFromLocal /usr/lib/spark/external/lib/spark-avro.jar /apps/hudi/lib/spark-avro.jar
   ```

1. Open the notebook editor, enter the code from the following example, and run it\.

   ```
   %%configure
   { "conf": {
               "spark.jars":"hdfs:///apps/hudi/lib/hudi-spark-bundle.jar,hdfs:///apps/hudi/lib/spark-avro.jar",
               "spark.serializer":"org.apache.spark.serializer.KryoSerializer",
               "spark.sql.hive.convertMetastoreParquet":"false"
             }}
   ```

------

## Initialize a Spark Session for Hudi<a name="emr-hudi-initialize-session"></a>

When using Scala, make sure you import the following classes in your Spark session\. This needs to be done once per Spark session\.

```
import org.apache.spark.sql.SaveMode
import org.apache.spark.sql.functions._
import org.apache.hudi.DataSourceWriteOptions
import org.apache.hudi.config.HoodieWriteConfig
import org.apache.hudi.hive.MultiPartKeysValueExtractor
```

## Write to a Hudi Dataset<a name="emr-hudi-dataframe"></a>

The following example shows how to create a DataFrame and write it as a Hudi dataset\.

**Note**  
To paste code samples into the Spark shell, type **:paste** at the prompt, paste the example, and then press **CTRL** \+ **D**\.

Each time you write a DataFrame to a Hudi dataset, you must specify `DataSourceWriteOptions`\. Many of these options are likely to be identical between write operations\. The following example specifies common options using the `hudiOptions` variable, which subsequent examples use\.

------
#### [ Scala ]

```
// Create a DataFrame
val inputDF = Seq(
 ("100", "2015-01-01", "2015-01-01T13:51:39.340396Z"),
 ("101", "2015-01-01", "2015-01-01T12:14:58.597216Z"),
 ("102", "2015-01-01", "2015-01-01T13:51:40.417052Z"),
 ("103", "2015-01-01", "2015-01-01T13:51:40.519832Z"),
 ("104", "2015-01-02", "2015-01-01T12:15:00.512679Z"),
 ("105", "2015-01-02", "2015-01-01T13:51:42.248818Z")
 ).toDF("id", "creation_date", "last_update_time")

//Specify common DataSourceWriteOptions in the single hudiOptions variable 
val hudiOptions = Map[String,String](
  HoodieWriteConfig.TABLE_NAME -> "my_hudi_table",
  DataSourceWriteOptions.TABLE_TYPE_OPT_KEY -> "COPY_ON_WRITE", 
  DataSourceWriteOptions.RECORDKEY_FIELD_OPT_KEY -> "id",
  DataSourceWriteOptions.PARTITIONPATH_FIELD_OPT_KEY -> "creation_date",
  DataSourceWriteOptions.PRECOMBINE_FIELD_OPT_KEY -> "last_update_time",
  DataSourceWriteOptions.HIVE_SYNC_ENABLED_OPT_KEY -> "true",
  DataSourceWriteOptions.HIVE_TABLE_OPT_KEY -> "my_hudi_table",
  DataSourceWriteOptions.HIVE_PARTITION_FIELDS_OPT_KEY -> "creation_date",
  DataSourceWriteOptions.HIVE_PARTITION_EXTRACTOR_CLASS_OPT_KEY -> classOf[MultiPartKeysValueExtractor].getName
)

// Write the DataFrame as a Hudi dataset
inputDF.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.INSERT_OPERATION_OPT_VAL)
  .options(hudiOptions)
  .mode(SaveMode.Overwrite)
  .save("s3://DOC-EXAMPLE-BUCKET/myhudidataset/")
```

------
#### [ PySpark ]

```
# Create a DataFrame
inputDF = spark.createDataFrame(
    [
        ("100", "2015-01-01", "2015-01-01T13:51:39.340396Z"),
        ("101", "2015-01-01", "2015-01-01T12:14:58.597216Z"),
        ("102", "2015-01-01", "2015-01-01T13:51:40.417052Z"),
        ("103", "2015-01-01", "2015-01-01T13:51:40.519832Z"),
        ("104", "2015-01-02", "2015-01-01T12:15:00.512679Z"),
        ("105", "2015-01-02", "2015-01-01T13:51:42.248818Z"),
    ],
    ["id", "creation_date", "last_update_time"]
)

# Specify common DataSourceWriteOptions in the single hudiOptions variable
hudiOptions = {
'hoodie.table.name': 'my_hudi_table',
'hoodie.datasource.write.recordkey.field': 'id',
'hoodie.datasource.write.partitionpath.field': 'creation_date',
'hoodie.datasource.write.precombine.field': 'last_update_time',
'hoodie.datasource.hive_sync.enable': 'true',
'hoodie.datasource.hive_sync.table': 'my_hudi_table',
'hoodie.datasource.hive_sync.partition_fields': 'creation_date',
'hoodie.datasource.hive_sync.partition_extractor_class': 'org.apache.hudi.hive.MultiPartKeysValueExtractor'
}

# Write a DataFrame as a Hudi dataset
inputDF.write
.format('org.apache.hudi')
.option('hoodie.datasource.write.operation', 'insert')
.options(**hudiOptions)
.mode('overwrite')
.save('s3://DOC-EXAMPLE-BUCKET/myhudidataset/')
```

------

**Note**  
You might see "hoodie" instead of Hudi in code examples and notifications\. The Hudi codebase widely uses the old "hoodie" spelling\.


**DataSourceWriteOptions Reference for Hudi**  

| Option | Description | 
| --- | --- | 
|  TABLE\_NAME  |  The table name under which to register the dataset\.  | 
|  TABLE\_TYPE\_OPT\_KEY  |  Optional\. Specifies whether the dataset is created as `"COPY_ON_WRITE"` or `"MERGE_ON_READ"`\. The default is `"COPY_ON_WRITE"`\.  | 
|  RECORDKEY\_FIELD\_OPT\_KEY  |  The record key field whose value will be used as the `recordKey` component of `HoodieKey`\. Actual value will be obtained by invoking `.toString()` on the field value\. Nested fields can be specified using the dot notation, for example, `a.b.c`\.   | 
|  PARTITIONPATH\_FIELD\_OPT\_KEY  |  The partition path field whose value will be used as the `partitionPath` component of `HoodieKey`\. The actual value will be obtained by invoking `.toString()` on the field value\.  | 
|  PRECOMBINE\_FIELD\_OPT\_KEY  |  The field used in pre\-combining before actual write\. When two records have the same key value, Hudi picks the one with the largest value for the precombine field as determined by `Object.compareTo(..)`\.  | 

The following options are required only to register the Hudi dataset table in your metastore\. If you do not register your Hudi dataset as a table in the Hive metastore, these options are not required\.


**DataSourceWriteOptions Reference for Hive**  

| Option | Description | 
| --- | --- | 
|  HIVE\_DATABASE\_OPT\_KEY  |  The Hive database to sync to\. The default is `"default"`\.  | 
|  HIVE\_PARTITION\_EXTRACTOR\_CLASS\_OPT\_KEY  |  The class used to extract partition field values into Hive partition columns\.   | 
|  HIVE\_PARTITION\_FIELDS\_OPT\_KEY  |  The field in the dataset to use for determining Hive partition columns\.  | 
|  HIVE\_SYNC\_ENABLED\_OPT\_KEY  |  When set to `"true"`, registers the dataset with the Apache Hive metastore\. The default is `"false"`\.  | 
|  HIVE\_TABLE\_OPT\_KEY  |  Required\. The name of the table in Hive to sync to\. For example, `"my_hudi_table_cow"`\.  | 
|  HIVE\_USER\_OPT\_KEY  |  Optional\. The Hive user name to use when syncing\. For example, `"hadoop"`\.  | 
|  HIVE\_PASS\_OPT\_KEY  |  Optional\. The Hive password for the user specified by `HIVE_USER_OPT_KEY`\.  | 
|  HIVE\_URL\_OPT\_KEY  |  The Hive metastore URL\.  | 

## Upsert Data<a name="emr-hudi-upsert-to-datasets"></a>

The following example demonstrates how to upsert data by writing a DataFrame\. Unlike the previous insert example, the `OPERATION_OPT_KEY` value is set to `UPSERT_OPERATION_OPT_VAL`\. In addition, `.mode(SaveMode.Append)` is specified to indicate that the record should be appended\.

------
#### [ Scala ]

```
// Create a new DataFrame from the first row of inputDF with a different creation_date value
val updateDF = inputDF.limit(1).withColumn("creation_date", lit("new_value"))

updateDF.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.UPSERT_OPERATION_OPT_VAL)
  .options(hudiOptions)
  .mode(SaveMode.Append)
  .save("s3://DOC-EXAMPLE-BUCKET/myhudidataset/")
```

------
#### [ PySpark ]

```
# Create a new DataFrame from the first row of inputDF with a different creation_date value
updateDF = inputDF.limit(1).withColumn('creation_date', lit('new_value'))

updateDF.write
.format('org.apache.hudi')
.option('hoodie.datasource.write.operation', 'upsert')
.options(**hudiOptions)
.mode('append')
.save('s3://DOC-EXAMPLE-BUCKET/myhudidataset/')
```

------

## Delete a Record<a name="emr-hudi-delete-from-datasets"></a>

To hard delete a record, you can upsert an empty payload\. In this case, the `PAYLOAD_CLASS_OPT_KEY` option specifies the `EmptyHoodieRecordPayload` class\. The example uses the same DataFrame, `updateDF`, used in the upsert example to specify the same record\.

------
#### [ Scala ]

```
updateDF.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.UPSERT_OPERATION_OPT_VAL)
  .option(DataSourceWriteOptions.PAYLOAD_CLASS_OPT_KEY, "org.apache.hudi.common.model.EmptyHoodieRecordPayload")
  .mode(SaveMode.Append)
  .save("s3://DOC-EXAMPLE-BUCKET/myhudidataset/")
```

------
#### [ PySpark ]

```
updateDF.write
.format('org.apache.hudi')
.option('hoodie.datasource.write.operation', 'upsert')
.option('hoodie.datasource.write.payload.class', 'org.apache.hudi.common.model.EmptyHoodieRecordPayload')
.options(**hudiOptions)
.mode('append')
.save('s3://DOC-EXAMPLE-BUCKET/myhudidataset/')
```

------

You can also hard delete data by setting `OPERATION_OPT_KEY `to `DELETE_OPERATION_OPT_VAL` to remove all records in the dataset you submit\. For instructions on performing soft deletes, and for more information about deleting data stored in Hudi tables, see [Deletes](https://hudi.apache.org/docs/writing_data.html#deletes) in the Apache Hudi documentation\.

## Read from a Hudi Dataset<a name="emr-hudi-read-dataset"></a>

To retrieve data at the present point in time, Hudi performs snapshot queries by default\. Following is an example of querying the dataset written to S3 in [Write to a Hudi Dataset](#emr-hudi-dataframe)\. Replace *s3://mybucket/myhudidataset* with your table path, and add wildcard asterisks for each partition level, *plus one additional asterisk*\. In this example, there is one partition level, so we've added two wildcard symbols\.

------
#### [ Scala ]

```
val snapshotQueryDF = spark.read
.format("org.apache.hudi")
.load("s3://DOC-EXAMPLE-BUCKET/myhudidataset" + "/*/*")

snapshotQueryDF.show()
```

------
#### [ PySpark  ]

```
snapshotQueryDF = spark.read
    .format('org.apache.hudi')
    .load('s3://DOC-EXAMPLE-BUCKET/myhudidataset' + '/*/*')
    
snapshotQueryDF.show()
```

------

### Incremental Queries<a name="emr-hudi-incremental-query"></a>

You can also perform incremental queries with Hudi to get a stream of records that have changed since a given commit timestamp\. To do so, set the `QUERY_TYPE_OPT_KEY` field to `QUERY_TYPE_INCREMENTAL_OPT_VAL`\. Then, add a value for `BEGIN_INSTANTTIME_OPT_KEY` to obtain all records written since the specified time\. Incremental queries are typically ten times more efficient than their batch counterparts since they only process changed records\.

When you perform incremental queries, use the root \(base\) table path without the wildcard asterisks used for Snapshot queries\.

**Note**  
Presto does not support incremental queries\.

------
#### [ Scala ]

```
val incQueryDF = spark.read
     .format("org.apache.hudi")
     .option(DataSourceReadOptions.QUERY_TYPE_OPT_KEY, DataSourceReadOptions.QUERY_TYPE_INCREMENTAL_OPT_VAL)
     .option(DataSourceReadOptions.BEGIN_INSTANTTIME_OPT_KEY, <beginInstantTime>)
     .load("s3://DOC-EXAMPLE-BUCKET/myhudidataset" );
     
incQueryDF.show()
```

------
#### [ PySpark ]

```
readOptions = {
  'hoodie.datasource.query.type': 'incremental',
  'hoodie.datasource.read.begin.instanttime': <beginInstantTime>,
}

incQueryDF = spark.read
    .format('org.apache.hudi')
    .options(**readOptions)
    .load('s3://DOC-EXAMPLE-BUCKET/myhudidataset')
    
incQueryDF.show()
```

------

For more information about reading from Hudi datasets, see [Querying Hudi Tables](https://hudi.apache.org/docs/querying_data.html) in the Apache Hudi documentation\.