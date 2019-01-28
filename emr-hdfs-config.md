# HDFS Configuration<a name="emr-hdfs-config"></a>

The following table describes the default Hadoop Distributed File System \(HDFS\) parameters and their settings\. You can change these values using the `hdfs-site` configuration classification\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


| Parameter | Definition | Default value | 
| --- | --- | --- | 
| dfs\.block\.size | The size of HDFS blocks\. When operating on data stored in HDFS, the split size is generally the size of an HDFS block\. Larger numbers provide less task granularity, but also put less strain on the cluster NameNode\. | 134217728 \(128 MB\) | 
| dfs\.replication | The number of copies of each block to store for durability\. For small clusters, set this to 2 because the cluster is small and easy to restart in case of data loss\. You can change the setting to 1, 2, or 3 as your needs dictate\. Amazon EMR automatically calculates the replication factor based on cluster size\. To overwrite the default value, use the hdfs\-site classification\. |  1 for clusters < four nodes 2 for clusters < ten nodes 3 for all other clusters  | 