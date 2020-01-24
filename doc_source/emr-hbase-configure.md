# Configure HBase<a name="emr-hbase-configure"></a>

Although the default settings should work for most applications, you have the flexibility to modify your HBase configuration settings\. To do this, use properties of HBase configuration classifications\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

The following example creates a cluster with an alternate HBase root directory based on a configuration file, `myConfig.json`, stored in Amazon S3\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --release-label emr-5.29.0 --applications Name=HBase \
--instance-type m5.xlarge --instance-count 3 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
```

The `myConfig.json` file specifies the `hbase.rootdir` property for the `hbase-site` configuration classification as shown in the following example\. Replace *ip\-XXX\-XX\-XX\-XXX\.ec2\.internal* with the internal DNS hostname of the cluster's master node\.

```
[
  {
    "Classification":"hbase-site",
    "Properties": {
       "hbase.rootdir": "hdfs://ip-XXX-XX-XX-XXX.ec2.internal:8020/user/myCustomHBaseDir"
    }
  }
]
```

**Note**  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

## Changes to Memory Allocation in YARN<a name="emr-hbase-configure-yarn"></a>

HBase is not running as a YARN application, thus it is necessary to recalculate the memory allocated to YARN and its applications, which results in a reduction in overall memory available to YARN if HBase is installed\. You should take this into account when planning to co\-locate YARN applications and HBase on the same clusters\. The instance types with less than 64 GB of memory have half the memory available to NodeManager, which is then allocated to the HBase RegionServer\. For instance types with memory greater than 64 GB, HBase RegionServer memory is capped at 32 GB\. As a general rule, YARN setting memory is some multiple of MapReduce reducer task memory\.

The tables in [Default Values for Task Configuration Settings](emr-hadoop-task-config.md#emr-hadoop-task-jvm) show changes to YARN settings based on the memory needed for HBase\.

## HBase Port Numbers<a name="emr-hbase-ports"></a>

Some port numbers chosen for HBase are different from the default\. The following are interfaces and ports for HBase on Amazon EMR\.


**HBase Ports**  

| Interface | Port | Protocol | 
| --- | --- | --- | 
| HMaster | 16000 | TCP | 
| HMaster UI | 16010 | HTTP | 
| RegionServer | 16020 | TCP | 
| RegionServer Info | 16030 | HTTP | 
| REST server | 8070 | HTTP | 
| REST UI | 8085 | HTTP | 
| Thrift server | 9090 | TCP | 
| Thrift server UI | 9095 | HTTP | 

**Important**  
The `kms-http-port` is 9700 and the `kms-admin-port` is 9701 in Amazon EMR release version 4\.6\.0 and later\.

## HBase Site Settings to Optimize<a name="emr-hbase-settings-optimize"></a>

You can set any or all of the HBase site settings to optimize the HBase cluster for your application's workload\. We recommend the following settings as a starting point in your investigation\.

### zookeeper\.session\.timeout<a name="emr-hbase-zookeeper.session.timeout"></a>

The default timeout is 40 seconds \(40000 ms\)\. If a region server crashes, this is how long it takes the master server to notice the absence of the region server and start recovery\. To help the master server recover faster, you can reduce this value to a shorter time period\. The following example uses 30 seconds, or 30000 ms: 

```
[
  {
    "Classification":"hbase-site",
    "Properties": {
       "zookeeper.session.timeout": "30000"
    }
  }
]
```

### hbase\.regionserver\.handler\.count<a name="emr-hbase-hbase.regionserver.handler.count"></a>

This defines the number of threads the region server keeps open to serve requests to tables\. The default of 10 is low, in order to prevent users from killing their region servers when using large write buffers with a high number of concurrent clients\. The rule of thumb is to keep this number low when the payload per request approaches the MB range \(big puts, scans using a large cache\) and high when the payload is small \(gets, small puts, ICVs, deletes\)\. The following example raises the number of open threads to 30: 

```
[
  {
    "Classification":"hbase-site",
    "Properties": {
       "hbase.regionserver.handler.count": "30"
    }
  }
]
```

### hbase\.hregion\.max\.filesize<a name="emr-hbase-hbase.hregion.max.filesize"></a>

This parameter governs the size, in bytes, of the individual regions\. By default, it is set to `1073741824`\. If you are writing a lot of data into your HBase cluster, and it's causing frequent splitting, you can increase this size to make individual regions bigger\. It reduces splitting but takes more time to load\-balance regions from one server to another\. 

```
[
  {
    "Classification":"hbase-site",
    "Properties": {
       "hbase.hregion.max.filesize": "1073741824"
    }
  }
]
```

### hbase\.hregion\.memstore\.flush\.size<a name="emr-hbase-hbase.hregion.memstore.flush.size"></a>

This parameter governs the maximum size of memstore, in bytes, before it is flushed to disk\. By default, it is `134217728`\. If your workload consists of short bursts of write operations, you might want to increase this limit so that all writes stay in memory during the burst and get flushed to disk later\. This can boost performance during bursts\. 

```
[
  {
    "Classification":"hbase-site",
    "Properties": {
       "hbase.hregion.memstore.flush.size": "134217728"
    }
  }
]
```