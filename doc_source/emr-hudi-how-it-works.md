# How Hudi Works<a name="emr-hudi-how-it-works"></a>

When using Hudi with Amazon EMR, you can write data to the dataset using the Spark Data Source API or the Hudi DeltaStreamer utility\. Hudi organizes a dataset into a partitioned directory structure under a `basepath` that is similar to a traditional Hive table\. The specifics of how the data is laid out as files in these directories depend on the dataset type that you choose\. You can choose either Copy on Write \(CoW\) or Merge on Read \(MoR\)\.

Regardless of the dataset type, each partition in a dataset is uniquely identified by its `partitionpath` relative to the `basepath`\. Within each partition, records are distributed into multiple data files\. For more information, see [File management](https://hudi.apache.org/docs/concepts.html#file-management) in the Apache Hudi documentation\.

Each action in Hudi has a corresponding commit, identified by a monotonically increasing timestamp known as an *Instant*\. Hudi keeps a series of all actions performed on the dataset as a timeline\. Hudi relies on the timeline to provide snapshot isolation between readers and writers, and to enable roll back to a previous point in time\. For more information about the actions that Hudi records and the state of actions, see [Timeline](https://hudi.apache.org/docs/concepts.html#timeline) in the Apache Hudi documentation\.

## Understanding Dataset Storage Types: Copy on Write vs\. Merge on Read<a name="emr-hudi-data-files"></a>

When you create a Hudi dataset, you specify that the dataset is either copy on write or merge on read\.
+ **Copy on Write \(CoW\)** – Data is stored in a columnar format \(Parquet\), and each update creates a new version of files during a write\. CoW is the default storage type\. 
+ **Merge on Read \(MoR\)** – Data is stored using a combination of columnar \(Parquet\) and row\-based \(Avro\) formats\. Updates are logged to row\-based *delta* files and are compacted as needed to create new versions of the columnar files\.

With CoW datasets, each time there is an update to a record, the file that contains the record is rewritten with the updated values\. With a MoR dataset, each time there is an update, Hudi writes only the row for the changed record\. MoR is better suited for write\- or change\-heavy workloads with fewer reads\. CoW is better suited for read\-heavy workloads on data that changes less frequently\.

Hudi provides three logical views for accessing the data:
+ **Read\-optimized view** – Provides the latest committed dataset from CoW tables and the latest compacted dataset from MoR tables\.
+ **Incremental view** – Provides a change stream between two actions out of a CoW dataset to feed downstream jobs and extract, transform, load \(ETL\) workflows\.
+ **Real\-time view** – Provides the latest committed data from a MoR table by merging the columnar and row\-based files inline\.

When you query the read\-optimized view, the query returns all compacted data but does not include the latest delta commits\. Querying this data provides good read performance but omits the freshest data\. When you query the real\-time view, Hudi merges the compacted data with the delta commits on read\. The freshest data is available to query, but the computational overhead of merging makes the query less performant\. The ability to query either compacted data or real\-time data allows you to choose between performance and flexibility when you query\.

For more information about the tradeoffs between storage types, see [Storage Types & Views](https://hudi.apache.org/docs/concepts.html#storage-types--views) in Apache Hudi documentation\.

Hudi creates two tables in the Hive metastore for MoR: a table with the name that you specified, which is a read\-optimized view, and a table with the same name appended with `_rt`, which is a real\-time view\. You can query both tables\.

## Registering a Hudi Dataset with Your Metastore<a name="emr-hudi-hive-metastore"></a>

When you register a Hudi table with the Hive metastore, you can query Hudi tables using Hive, Spark SQL or Presto as you would any other table\. In addition, you can integrate Hudi with AWS Glue by configuring Hive and Spark to use the AWS Glue Data Catalog as the metastore\. For MoR tables, Hudi registers the dataset as two tables in the Metastore: a table with the name that you specified, which is a read\-optimized view, and a table with the same name appended with `_rt`, which is a real\-time view\.

You register a Hudi table with the Hive metastore when you use Spark to create a Hudi dataset by setting the `HIVE_SYNC_ENABLED_OPT_KEY` option to `"true"` and providing other required properties\. For more information, see [Working With a Hudi Dataset](emr-hudi-work-with-dataset.md)\. In addition, you can use the hive\_sync\_tool command line utility to register a Hudi dataset as a table in your metastore, separately\. 