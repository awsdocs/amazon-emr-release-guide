# HBase on Amazon S3 \(Amazon S3 Storage Mode\)<a name="emr-hbase-s3"></a>

When you run HBase on Amazon EMR version 5\.2\.0 or later, you can enable HBase on Amazon S3, which offers the following advantages:
+ The HBase root directory is stored in Amazon S3, including HBase store files and table metadata\. This data is persistent outside of the cluster, available across Amazon EC2 Availability Zones, and you don't need to recover using snapshots or other methods\.
+ With store files in Amazon S3, you can size your Amazon EMR cluster for your compute requirements instead of data requirements, with 3x replication in HDFS\.
+ Using Amazon EMR version 5\.7\.0 or later, you can set up a read\-replica cluster, which allows you to maintain read\-only copies of data in Amazon S3\. You can access the data from the read\-replica cluster to perform read operations simultaneously, and in the event that the primary cluster becomes unavailable\.

The following illustration shows the HBase components relevant to HBase on Amazon S3\. 

![\[HBase on Amazon S3 architecture.\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/hbase_s3.png)

## Enabling HBase on Amazon S3<a name="emr-hbase-s3-enable"></a>

You can enable HBase on Amazon S3 using the Amazon EMR console, the AWS CLI, or the Amazon EMR API\. The configuration is an option during cluster creation\. When you use the console, you choose the setting using **Advanced options**\. When you use the AWS CLI, use the `--configurations ` option to provide a JSON configuration object\. Properties of the configuration object specify the storage mode and the root directory location in Amazon S3\. The Amazon S3 location that you specify should be in the same region as your Amazon EMR cluster\. Only one active cluster at a time can use the same HBase root directory in Amazon S3\. For console steps and a detailed create\-cluster example using the AWS CLI, see [Creating a Cluster with HBase](emr-hbase-create.md)\. An example configuration object is shown in the following JSON snippet\. 

**Important**  
We strongly recommend that you use EMRFS consistent view when you enable HBase on Amazon S3 for production workloads\. Not using consistent view may result in performance impacts for specific operations\. For more information about configuring consistent view, see [Consistent View](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-consistent-view.html) in the *Amazon EMR Management Guide*\.

```
{
  "Classification": "hbase-site",
  "Properties": {
    "hbase.rootdir": "s3://my-bucket/my-hbase-rootdir"}
},
{
  "Classification": "hbase",
  "Properties": {
  "hbase.emr.storageMode":"s3"
  }
}
```

## Using a Read\-Replica Cluster<a name="emr-hbase-s3-read-replica"></a>

After you set up a primary cluster using HBase on Amazon S3, you can create and configure a read\-replica cluster that provides read\-only access to the same data as the primary cluster\. This is useful when you need simultaneous access to query data or uninterrupted access if the primary cluster becomes unavailable\. The read\-replica feature is available with Amazon EMR version 5\.7\.0 and later\.

The primary cluster and the read\-replica cluster are set up the same way with one important difference\. Both point to the same `hbase.rootdir` location\. However, the `hbase` classification for the read\-replica cluster includes the `"hbase.emr.readreplica.enabled":"true"` property\.

For example, given the JSON classification for the primary cluster as shown earlier in the topic, the configuration for a read\-replica cluster is as follows:

```
{
  "Classification": "hbase-site",
  "Properties": {
    "hbase.rootdir": "s3://my-bucket/my-hbase-rootdir"}
},
{
  "Classification": "hbase",
  "Properties": {
  "hbase.emr.storageMode":"s3",
  "hbase.emr.readreplica.enabled":"true"
  }
}
```

### Synchronizing the Read Replica When You Add Data<a name="w40aac26c21c13c10"></a>

Because the read\-replica uses HBase StoreFiles and metadata that the primary cluster writes to Amazon S3, the read\-replica is only as current as the Amazon S3 data store\. The following guidance can help minimize the lag time between the primary cluster and the read\-replica when you write data\.
+ Bulk load data on the primary cluster whenever possible\. For more information, see [Bulk Loading](http://hbase.apache.org/0.94/book/arch.bulk.load.html) in Apache HBase documentation\.
+ A flush that writes store files to Amazon S3 should occur as soon as possible after data is added\. Either flush manually or tune flush settings to minimize lag time\.
+ If compactions might run automatically, run a manual compaction to avoid inconsistencies when compactions are triggered\.
+ On the read\-replica cluster, when any metadata has changed—for example, when HBase region split or compactions occur, or when tables are added or removed—run the `refresh_meta` command\.
+ On the read\-replica cluster, run the `refresh_hfiles` command when records are added to or changed in a table\.

![\[Synchronizing data with an HBase read-replica\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/hbase-read-replica.png)

## Operational Considerations<a name="emr-hbase-s3-performance"></a>

HBase region servers use BlockCache to store data reads in memory and BucketCache to store data reads on local disk\. In addition, region servers use MemStore to store data writes in\-memory, and use write\-ahead logs to store data writes in HDFS before the data is written to HBase StoreFiles in Amazon S3\. The read performance of your cluster relates to how often a record can be retrieved from the in\-memory or on\-disk caches\. A cache miss results in the record being read from the StoreFile in Amazon S3, which has significantly higher latency and higher standard deviation than reading from HDFS\. In addition, the maximum request rates for Amazon S3 are lower than what can be achieved from the local cache, so caching data may be important for read\-heavy workloads\. For more information about Amazon S3 performance, see [Performance Optimization](https://docs.aws.amazon.com/AmazonS3/latest/dev/PerformanceOptimization.html) in the *Amazon Simple Storage Service Developer Guide*\.

To improve performance, we recommend that you cache as much of your dataset as possible in EC2 instance storage\. Because the BucketCache uses the region server's EC2 instance storage, you can choose an EC2 instance type with a sufficient instance store and add Amazon EBS storage to accommodate the required cache size\. You can also increase the BucketCache size on attached instance stores and EBS volumes using the `hbase.bucketcache.size` property\. The default setting is 8,192 MB\.

For writes, the frequency of MemStore flushes and the number of StoreFiles present during minor and major compactions can contribute significantly to an increase in region server response times\. For optimal performance, consider increasing the size of the MemStore flush and HRegion block multiplier, which increases the elapsed time between major compactions, but also increases the lag in consistency if you use a read\-replica\. In some cases, you may get better performance using larger file block sizes \(but less than 5 GB\) to trigger Amazon S3 multipart upload functionality in EMRFS\. Amazon EMR's block size default 128 MB\. For more information, see [HDFS Configuration](emr-hdfs-config.md)\. We rarely see customers who exceed 1 GB block size while benchmarking performance with flushes and compactions\. Additionally, HBase compactions and region servers perform optimally when fewer StoreFiles need to be compacted\.

Tables can take a significant amount of time to drop on Amazon S3 because large directories need to be renamed\. Consider disabling tables instead of dropping\.

There is an HBase cleaner process that cleans up old WAL files and store files\. With Amazon EMR release version 5\.17\.0 and later, the cleaner is enabled globally, and the following configuration properties can be used to control cleaner behavior\.


| Configuration Property | Default Value | Description | 
| --- | --- | --- | 
|  `hbase.regionserver.hfilecleaner.large.thread.count`  |  1  |  The number of threads allocated to clean expired large HFiles\.  | 
|  `hbase.regionserver.hfilecleaner.small.thread.count`  |  1  |  The number of threads allocated to clean expired small HFiles\.  | 
|  `hbase.cleaner.scan.dir.concurrent.size`  |  Set to one quarter of all available cores\.  |  The number of threads to scan the oldWALs directories\.  | 
|  `hbase.oldwals.cleaner.thread.size`  |  2  |  The number of threads to clean the WALs under the oldWALs directory\.  | 

With Amazon EMR 5\.17\.0 and earlier, the cleaner operation can affect query performance when running heavy workloads, so we recommend that you enable the cleaner only during off\-peak times\. The cleaner has the following HBase shell commands:
+ `cleaner_enabled` queries whether the cleaner is enabled\.
+ `cleaner_run` manually runs the cleaner to remove files\.
+ `cleaner_switch` enables or disables the cleaner and returns the previous state of the cleaner\. For example, `cleaner-switch true` enables the cleaner\.

### Properties for HBase on Amazon S3 Performance Tuning<a name="emr-hbase-s3-properties"></a>

The following parameters can be adjusted to tune the performance of your workload when you use HBase on Amazon S3\.


| Configuration Property | Default Value | Description | 
| --- | --- | --- | 
|  `hbase.bucketcache.size`  |  8,192  |  The amount of disk space, in MB, reserved on region server Amazon EC2 instance stores and EBS volumes for BucketCache storage\. The setting applies to all region server instances\. Larger BucketCache sizes generally correspond to improved performance  | 
|  `hbase.hregion.memstore.flush.size`  |  134217728  |  The data limit, in bytes, at which a memstore flush to Amazon S3 is triggered\.  | 
|  `hbase.hregion.memstore.block.multiplier`  |  4  |  A multiplier that determines the MemStore upper limit at which updates are blocked\. If the MemStore exceeds `hbase.hregion.memstore.flush.size` multiplied by this value, updates are blocked\. MemStore flushes and compaction may happen to unblock updates\.  | 
|  `hbase.hstore.blockingStoreFiles`  |  10  |  The maximum number of StoreFiles that can exist in a store before updates are blocked\.  | 
|  `hbase.hregion.max.filesize`  |  10737418240  |  The maximum size of a region before the region is split\.  | 

### Shutting Down and Restoring a Cluster Without Data Loss<a name="emr-hbase-s3-shutdown"></a>

To shut down an Amazon EMR cluster without losing data that hasn't been written to Amazon S3, the MemStore cache needs to flush to Amazon S3 to write new store files\. To do this, you can run a shell script provided on the EMR cluster\. You can either add it as a step or run it directly using the on\-cluster CLI\. The script disables all HBase tables, which causes the MemStore in each region server to flush to Amazon S3\. If the script completes successfully, the data persists in Amazon S3 and the cluster can be terminated\. 

The following step configuration can be used when you add a step to the cluster\. For more information, see [Work with Steps Using the CLI and Console](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-work-with-steps.html) in the *Amazon EMR Management Guide*\.

```
Name="Disable all tables",Jar="command-runner.jar",Args=["/bin/bash","/usr/lib/hbase/bin/disable_all_tables.sh"]
```

Alternatively, you can run the following bash command directly\.

```
bash /usr/lib/hbase/bin/disable_all_tables.sh
```

To restart a cluster with the same HBase data, specify the same Amazon S3 location as the previous cluster either in the AWS Management Console or using the `hbase.rootdir` configuration property\.