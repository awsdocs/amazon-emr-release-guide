# Hadoop and Spark Metrics in Ganglia<a name="Hadoopmetrics_Ganglia"></a>

 Ganglia reports Hadoop metrics for each instance\. The various types of metrics are prefixed by category: distributed file system \(dfs\.\*\), Java virtual machine \(jvm\.\*\), MapReduce \(mapred\.\*\), and remote procedure calls \(rpc\.\*\)\. 

YARN\-based Ganglia metrics such as Spark and Hadoop are not available for EMR release versions 4\.4\.0 and 4\.5\.0\. Use a later version to use these metrics\.

Ganglia metrics for Spark generally have prefixes for YARN application ID and Spark DAGScheduler\. So prefixes follow this form: 
+ DAGScheduler\.\*
+ application\_xxxxxxxxxx\_xxxx\.driver\.\*
+ application\_xxxxxxxxxx\_xxxx\.executor\.\*