# Considerations and Limitations for Using Hudi on Amazon EMR<a name="emr-hudi-considerations"></a>
+ **Record key field cannot be null or empty** – The field that you specify as the record key field cannot have `null` or empty values\.
+ **Schema updated by default on upsert and insert** – Hudi provides an interface, `HoodieRecordPayload` that determines how the input DataFrame and existing Hudi dataset are merged to produce a new, updated dataset\. Hudi provides a default implementation of this class, `OverwriteWithLatestAvroPayload`, that overwrites existing records and updates the schema as specified in the input DataFrame\. To customize this logic for implementing merge and partial updates, you can provide an implementation of the `HoodieRecordPayload` interface using the `DataSourceWriteOptions.PAYLOAD_CLASS_OPT_KEY` parameter\.
+ **Deletion requires schema** – When deleting, you must specify the record key, the partition key, and the pre\-combine key fields\. Other columns can be made `null` or empty, but the full schema is required\.
+ **MoR table limitations** – MoR tables do not support savepointing\. You can query MoR tables using the read\-optimized view or the real\-time view \(`tablename_rt`\) from Spark SQL, Presto, or Hive\. Using the read\-optimized view only exposes base file data, and does not expose a merged view of base and log data\.
+ **Hive**
  + For registering tables in the Hive metastore, Hudi expects the Hive Thrift server to be running at the default port `10000`\. If you override this port with a custom port, pass the `HIVE_URL_OPT_KEY` option as shown in the following example\.

    ```
    .option(DataSourceWriteOptions.HIVE_URL_OPT_KEY, "jdbc:hive2://localhost:override-port-number
    ```
  + The `timestamp` data type in Spark is registerd as `long` data type in Hive, and not as Hive's `timestamp` type\.
+ **Presto**
  + Presto does not support reading MoR real time tables in Hudi versions below 0\.6\.0\. 
  + Presto only supports snapshot queries\.
  + For Presto to correctly interpret Hudi dataset columns, set the `hive.parquet_use_column_names` value to `true`\.
    + To set the value for a session, in the Presto shell, run the following command:

      ```
      set session hive.parquet_use_column_names=true
      ```
    + To set the value at the cluster level, use the `presto-connector-hive` configuration classification to set `hive.parquet.use_column_names` to `true`, as shown in the following example\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

      ```
      [
        {
          "Classification": "presto-connector-hive",
          "Properties": {
            "hive.parquet.use-column-names": "true"
          }
        }
      ]
      ```
+ **HBase Index**
  + The HBase version used to *build* Hudi might be different from what is listed in the EMR Release Guide\. To pull in the correct dependencies for your Spark session, run the following command\.

    ```
    spark-shell \
    --jars /usr/lib/spark/external/lib/spark-avro.jar,/usr/lib/hudi/cli/lib/*.jar \
    --conf "spark.serializer=org.apache.spark.serializer.KryoSerializer" \
    --conf "spark.sql.hive.convertMetastoreParquet=false"
    ```