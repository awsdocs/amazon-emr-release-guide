# How Iceberg works<a name="emr-iceberg-how-it-works"></a>

Iceberg tracks individual data files in a table instead of directories\. This allows writers to create data files in\-place and only adds files to the table in an explicit commit\. The table state is maintained in metadata files\. All changes to the table state create a new metadata file and atomically replaces the older metadata\. The table metadata file tracks the table schema, partitioning config, other properties, and the snapshots of the table contents\. 

Each snapshot is a complete set of data files in the table at a point in time\. Snapshots are listed in the metadata file, but the files in a snapshot are stored in separate manifest files\. The atomic transitions from one table metadata file to the next provide snapshot isolation\. Readers use the snapshot that was current when they loaded the table metadata and are not affected by changes until they refresh and pick up a new metadata location\. Data files in snapshots are stored in one or more manifest files that contain a row for each data file in the table, its partition data, and its metrics\. A snapshot is the union of all files in its manifests\. Manifest files can also be shared between snapshots to avoid rewriting metadata that is slow\-changing\.

**Iceberg snapshot diagram**

![\[Diagram of two snapshots. Each snapshot has its own manifest list, which stores metadata about multiple reusable manifests. Each manifest refers to one or multiple data files.\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/Iceberg-snapshot-diagram.png)

Iceberg offers the following features:
+ Supports ACID transactions and time travel in your S3 data lake\.
+ Commit retries are inexpensive due to reliance on [optimistic concurrency](https://iceberg.apache.org/#reliability/#concurrent-write-operations)\.
+ File level conflict resolution resulting in high concurrency\.
+ Min\-max statistics per column in metadata allows skipping of files significantly boosting performance of highly selective queries\.
+ Implicit partitioning and partition evolution: Partition values derived from columns using logical transforms removing the need to add extra predicates to queries, as well as evolve partitions as needed\.
+ [Schema evolution](https://iceberg.apache.org/#evolution/#schema-evolution) and enforcement\.
+ Iceberg tables act as idempotent sinks and replayable sources enabling streaming and batch support with exactly\-once pipelines\. Idempotent sinks track write operations that have succeeded in the past, so the sink can re\-request data in case of a failure and drop data if it has been sent multiple times\.
+ Viewable history and lineage: table evolution, operations history, and stats for each commit\.
+ Easy migration from existing dataset with choice of data format \(Parquet, ORC, Avro\) and analytics engine \(Spark, Trino, PrestoDB, Flink, Hive\)\.