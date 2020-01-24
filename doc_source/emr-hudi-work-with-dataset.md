# Working With a Hudi Dataset<a name="emr-hudi-work-with-dataset"></a>

Hudi supports currently supports inserting, updating, and deleting data in Hudi datasets through Spark\. For more information, see [Writing Hudi Datasets](https://hudi.apache.org/writing_data.html) in Apache Hudi documentation\.

The following examples demonstrate how to launch the interactive Spark shell, use Spark submit, and use Amazon EMR Notebooks to work with Hudi on Amazon EMR\. You can also use the Hudi DeltaStreamer utility or other tools to write to a dataset\. Throughout this section, the examples demonstrate working with datasets using the Spark shell while connected to the master node using SSH as the default `hadoop` user\.

------
#### [ Spark Shell ]

**To open the Spark shell on the master node**

1. Connect to the master node using SSH\. For more information, see [Connect to the Master Node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. Enter the following command to launch the Spark shell\.

   ```
   spark-shell --conf "spark.serializer=org.apache.spark.serializer.KryoSerializer" --conf "spark.sql.hive.convertMetastoreParquet=false"
   --jars /usr/lib/hudi/hudi-spark-bundle.jar,/usr/lib/spark/external/lib/spark-avro.jar
   ```

------
#### [ spark\-submit ]

To submit a Spark application that uses Hudi, make sure to pass the following parameters to spark\-submit\.

```
spark-submit --conf "spark.serializer=org.apache.spark.serializer.KryoSerializer" --conf "spark.sql.hive.convertMetastoreParquet=false"
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

## Initializing a Spark Session for Hudi<a name="emr-hudi-initialize-session"></a>

In the Spark session, import the following classes\. This needs to be done once per Spark session\.

```
import org.apache.spark.sql.SaveMode
import org.apache.spark.sql.functions._
import org.apache.hudi.DataSourceWriteOptions
import org.apache.hudi.config.HoodieWriteConfig
import org.apache.hudi.hive.MultiPartKeysValueExtractor
```

## Writing to a Hudi Dataset<a name="emr-hudi-dataframe"></a>

The following example shows how to write a Spark DataFrame as a Hudi dataset\.

**Note**  
To paste code samples into the Spark shell, type **:paste** at the prompt, paste the example, and then press **CTRL** \+ **D**\.

Each time you write a DataFrame to a Hudi dataset, you must specify `DataSourceWriteOptions`\. Many of these options are likely to be identical between write operations\. The following example specifies common options using the `hudiOptions` variable, which subsequent examples use\.

```
// Read data from S3 and create a DataFrame with Partition and Record Key
val inputDF = spark.read.format("parquet").load("s3://mybucket/mydata/parquet/")

//Specify common DataSourceWriteOptions in the single hudiOptions variable 
val hudiOptions = Map[String,String](
  HoodieWriteConfig.TABLE_NAME → "my_hudi_table",
  DataSourceWriteOptions.STORAGE_TYPE_OPT_KEY -> "COPY_ON_WRITE", 
  DataSourceWriteOptions.RECORDKEY_FIELD_OPT_KEY -> "dataframe_column_name1",
  DataSourceWriteOptions.PARTITIONPATH_FIELD_OPT_KEY ->"dataframe_column_name2",
  DataSourceWriteOptions.PRECOMBINE_FIELD_OPT_KEY -> "dataframe_column_name3"
  DataSourceWriteOptions.HIVE_SYNC_ENABLED_OPT_KEY → "true",
  DataSourceWriteOptions.HIVE_TABLE_OPT_KEY → "my_hudi_table",
  DataSourceWriteOptions.HIVE_PARTITION_FIELDS_OPT_KEY → "dataframe_column_name2",
  DataSourceWriteOptions.HIVE_PARTITION_EXTRACTOR_CLASS_OPT_KEY → classOf[MultiPartKeysValueExtractor].getName
)

// Write a DataFrame as a Hudi dataset
inputDF.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.INSERT_OPERATION_OPT_VAL)
  .options(hudiOptions)
  .mode(SaveMode.Overwrite)
  .save("s3://mybucket/myhudidataset/")
```

**Note**  
The `STORAGE_TYPE_OPT_KEY` option establishes the type of dataset as CoW in the example\. CoW is the default, so this option is not required; we included it for clarity\.


**DataSourceWriteOptions Reference for Hudi**  

| Option | Description | 
| --- | --- | 
|  PARTITIONPATH\_FIELD\_OPT\_KEY  |  The partition path field whose value will be used as the `partitionPath` component of `HoodieKey`\. The actual value will be obtained by invoking `.toString()` on the field value\.  | 
|  PRECOMBINE\_FIELD\_OPT\_KEY  |  The field used in pre\-combining before actual write\. When two records have the same key value, Hudi picks the one with the largest value for the precombine field as determined by `Object.compareTo(..)`\.  | 
|  RECORDKEY\_FIELD\_OPT\_KEY  |  The record key field whose value will be used as the `recordKey` component of `HoodieKey`\. Actual value will be obtained by invoking `.toString()` on the field value\. Nested fields can be specified using the dot notation, for example, `a.b.c`\.   | 
|  STORAGE\_TYPE\_OPT\_KEY  |  Optional\. Specifies whether the dataset is created as `"COPY_ON_WRITE"` or `"MERGE_ON_READ"`\. The default is `"COPY_ON_WRITE"`\.  | 
|  TABLE\_NAME  |  The table name under which to register the dataset\.  | 

The following options are required only to register the Hudi dataset table in your metastore\. If you do not register your Hudi dataset as a table in the Hive metastore, these options are not required\.


**DataSourceWriteOptions Reference for Hive**  

| Option | Description | 
| --- | --- | 
|  HIVE\_ASSUME\_DATE\_PARTITION\_OPT\_KEY  |  Valid values are `"true"` or `"false"`\. Default is `"false"`\. When set to `"true"`, Hudi assumes that partitioning is `yyyy/mm/dd`\.  | 
|  HIVE\_DATABASE\_OPT\_KEY  |  The Hive database to sync to\. The default is `"default"`\.  | 
|  HIVE\_PARTITION\_EXTRACTOR\_CLASS\_OPT\_KEY  |  The class used to extract partition field values into Hive partition columns\.   | 
|  HIVE\_PARTITION\_FIELDS\_OPT\_KEY  |  The field in the dataset to use for determining Hive partition columns\.  | 
|  HIVE\_SYNC\_ENABLED\_OPT\_KEY  |  When set to `"true"`, registers the dataset with the Apache Hive metastore\. The default is `"false"`\.  | 
|  HIVE\_TABLE\_OPT\_KEY  |  Required\. The name of the table in Hive to sync to\. For example, `"my_hudi_table_cow"`\.  | 
|  HIVE\_USER\_OPT\_KEY  |  Optional\. The Hive user name to use when syncing\. For example, `"hadoop"`\.  | 
|  HIVE\_PASS\_OPT\_KEY  |  Optional\. The Hive password for the user specified by `HIVE_USER_OPT_KEY`\.  | 
|  HIVE\_URL\_OPT\_KEY  |  The Hive metastore URL\.  | 

## Upserting Data<a name="emr-hudi-upsert-to-datasets"></a>

The following example demonstrates how to write a DataFrame to perform upserts\. Unlike the insert example, the `OPERATION_OPT_KEY` value is set to `UPSERT_OPERATION_OPT_VAL`\. In addition, `.mode(SaveMode.Append)` is specified to indicate that the record should be appended\.

```
inputDF4.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.UPSERT_OPERATION_OPT_VAL)
  .options(hudiOptions)
  .mode(SaveMode.Append)
  .save("s3://mybucket/myhudidataset/")
```

## Deleting a Record by Upserting an Empty Payload<a name="emr-hudi-delete-from-datasets"></a>

To delete the same record specified in the previous example, this example again uses an upsert operation\. In this case, the `PAYLOAD_CKLASS_OPT_KEY` option specifies the `EmptyHoodieRecordPayload` class\. The example uses the same DataFrame, `inputDF4`, used in the upsert example so that the same record is specified\.

```
inputDF4.write
  .format("org.apache.hudi")
  .option(DataSourceWriteOptions.OPERATION_OPT_KEY, DataSourceWriteOptions.UPSERT_OPERATION_OPT_VAL)
  .option(DataSourceWriteOptions.PAYLOAD_CLASS_OPT_KEY, "org.apache.hudi.EmptyHoodieRecordPayload")
  .mode(SaveMode.Append)
  .save("s3://mybucket/myhudidataset/")
```