# Configure Spark<a name="emr-spark-configure"></a>

You can configure [Spark on Amazon EMR](https://aws.amazon.com/elasticmapreduce/details/spark/) using configuration classifications\. For more information about using configuration classifications, see [Configuring Applications](emr-configure-apps.md)\.

Configuration classifications for Spark on Amazon EMR include the following:
+ `spark`—Sets the `maximizeResourceAllocation` property to true or false\. When true, Amazon EMR automatically configures `spark-default` properties based on cluster hardware configuration\. For more information, see [Using maximizeResourceAllocation](#emr-spark-maximizeresourceallocation)\.
+ `spark-defaults`—Sets values in the `spark-defaults.conf` file\. For more information, see [Spark Configuration](https://spark.apache.org/docs/latest/configuration.html) in the Spark documentation\.
+ `spark-env`—Sets values in the `spark-env.sh` file\. For more information, see [Environment Variables](https://spark.apache.org/docs/latest/configuration.html#environment-variables) in the Spark documentation\.
+ `spark-hive-site`—Sets values in the `hive-site.xml` for Spark\.
+ `spark-log4j`—Sets values in the `log4j.properties` file\. For settings and more information, see the [log4j\.properties\.template](https://github.com/apache/spark/blob/master/conf/log4j.properties.template) file on Github\.
+ `spark-metrics`—Sets values in the `metrics.properties` file\. For settings and more information, see the [metrics\.properties\.template](https://github.com/apache/spark/blob/master/conf/metrics.properties.template) file on Github, and [Metrics](https://spark.apache.org/docs/latest/monitoring.html#metrics) in Spark documentation\.

## Spark Defaults Set By Amazon EMR<a name="spark-defaults"></a>

The following table shows how Amazon EMR sets default values in `spark-default` that affect applications\.


**Spark defaults set by Amazon EMR**  

| Setting | Description | Value | 
| --- | --- | --- | 
| spark\.executor\.memory | Amount of memory to use per executor process\. \(for example, 1g, 2g\) |  Setting is configured based on the core and task instance types in the cluster\.   | 
| spark\.executor\.cores | The number of cores to use on each executor\.  | Setting is configured based on the core and task instance types in the cluster\.  | 
| spark\.dynamicAllocation\.enabled | Whether to use dynamic resource allocation, which scales the number of executors registered with an application up and down based on the workload\. |  true \(emr\-4\.4\.0 or greater\)  Spark Shuffle Service is automatically configured by Amazon EMR\.   | 

## Using maximizeResourceAllocation<a name="emr-spark-maximizeresourceallocation"></a>

You can configure your executors to utilize the maximum resources possible on each node in a cluster by using the `spark` configuration classification to set `maximizeResourceAllocation` option to true\. This EMR\-specific option calculates the maximum compute and memory resources available for an executor on an instance in the core instance group\. It then sets the corresponding `spark-defaults` settings based on this information\.

```
[
  {
    "Classification": "spark",
    "Properties": {
      "maximizeResourceAllocation": "true"
    }
  }
]
```


**Settings configured in `spark-defaults` when `maximizeResourceAllocation `is enabled**  

| Setting | Description | Value | 
| --- | --- | --- | 
| spark\.default\.parallelism | Default number of partitions in RDDs returned by transformations like join, reduceByKey, and parallelize when not set by user\. |  2X number of CPU cores available to YARN containers\.  | 
| spark\.driver\.memory | Amount of memory to use for the driver process, i\.e\. where SparkContext is initialized\. \(for example, 1g, 2g\)\. |  Setting is configured based on the instance types in the cluster\. However, because the Spark driver application may run on either the master or one of the core instances \(for example, in YARN client and cluster modes, respectively\), this is set based on the smaller of the instance types in these two instance groups\.  | 
| spark\.executor\.memory | Amount of memory to use per executor process\. \(for example, 1g, 2g\) |  Setting is configured based on the core and task instance types in the cluster\.   | 
| spark\.executor\.cores | The number of cores to use on each executor\.  | Setting is configured based on the core and task instance types in the cluster\.  | 
| spark\.executor\.instances |  The number of executors\. |  Setting is configured based on the core and task instance types in the cluster\. Set unless `spark.dynamicAllocation.enabled` explicitly set to true at the same time\.  | 

## Enabling Dynamic Allocation of Executors<a name="spark-dynamic-allocation"></a>

Spark on YARN has the ability to scale the number of executors used for a Spark application dynamically\. Using Amazon EMR release version 4\.4\.0 and later, dynamic allocation is enabled by default\. For more information, see [Dynamic Resource Allocation](https://spark.apache.org/docs/1.6.1/job-scheduling.html#dynamic-resource-allocation) and the properties for [Dynamic Allocation](https://spark.apache.org/docs/latest/configuration.html#dynamic-allocation) in the Spark documentation\.

## Configuring Node Decommissioning Behavior<a name="spark-decommissioning"></a>

When using Amazon EMR release version 5\.9\.0 or later, Spark on Amazon EMR includes a set of features to help ensure that Spark handles node termination because of a manual resize or an automatic scaling policy request gracefully\. Amazon EMR implements a blacklisting mechanism in Spark that is built on top of YARN's decommissioning mechanism\. This mechanism helps ensure that no new tasks are scheduled on a node that is decommissioning, while at the same time allowing tasks that are already running to complete\. In addition, there are features to help recover Spark jobs faster if shuffle blocks are lost when a node terminates\. The recomputation process is triggered sooner and optimized to recompute faster with fewer stage retries, and jobs can be prevented from failing because of fetch failures that are caused by missing shuffle blocks\.

**Important**  
The `spark.decommissioning.timeout.threshold` setting was added in Amazon EMR release version 5\.11\.0 to improve Spark resiliency when you use Spot instances\. In earlier release versions, when a node uses a Spot instance, and the instance is terminated because of bid price, Spark may not be able to handle the termination gracefully\. Jobs may fail, and shuffle recomputations could take a significant amount of time\. For this reason, we recommend using release version 5\.11\.0 or later if you use Spot instances\.


**Spark Node Decommissioning Settings**  

| Setting | Description | Default Value | 
| --- | --- | --- | 
| `spark.blacklist.decommissioning.enabled` | When set to `true`, Spark blacklists nodes that are in the `decommissioning` state in YARN\. Spark does not schedule new tasks on executors running on that node\. Tasks already running are allowed to complete\. | `true` | 
| `spark.blacklist.decommissioning.timeout` | The amount of time that a node in the `decommissioning` state is blacklisted\. By default, this value is set to one hour, which is also the default for `yarn.resourcemanager.decommissioning.timeout`\. To ensure that a node is blacklisted for its entire decommissioning period, set this value equal to or greater than `yarn.resourcemanager.decommissioning.timeout`\. After the decommissioning timeout expires, the node transitions to a `decommissioned` state, and Amazon EMR can terminate the node's EC2 instance\. If any tasks are still running after the timeout expires, they are lost or killed and rescheduled on executors running on other nodes\. | `1h` | 
| `spark.decommissioning.timeout.threshold` | Available in Amazon EMR release version 5\.11\.0 or later\. Specified in seconds\. When a node transitions to the decommissioning state, if the host will decommission within a time period equal to or less than this value, Amazon EMR not only blacklists the node, but also cleans up the host state \(as specified by `spark.resourceManager.cleanupExpiredHost`\) without waiting for the node to transition to a decommissioned state\. This allows Spark to handle Spot instance terminations better because Spot instances decommission within a 20\-second timeout regardless of the value of `yarn.resourcemager.decommissioning.timeout`, which may not provide other nodes enough time to read shuffle files\. | `20s` | 
| `spark.resourceManager.cleanupExpiredHost` | When set to `true`, Spark unregisters all cached data and shuffle blocks that are stored in executors on nodes that are in the `decommissioned` state\. This speeds up the recovery process\. | `true` | 
| `spark.stage.attempt.ignoreOnDecommissionFetchFailure` | When set to `true`, helps prevent Spark from failing stages and eventually failing the job because of too many failed fetches from decommissioned nodes\. Failed fetches of shuffle blocks from a node in the `decommissioned` state will not count toward the maximum number of consecutive fetch failures\. | true | 

## Spark ThriftServer Environment Variable<a name="spark-thriftserver"></a>

Spark sets the Hive Thrift Server Port environment variable, `HIVE_SERVER2_THRIFT_PORT`, to 10001\.

## Changing Spark Default Settings<a name="spark-change-defaults"></a>

You change the defaults in `spark-defaults.conf` using the `spark-defaults` configuration classification or the `maximizeResourceAllocation` setting in the `spark` configuration classification\.

The following procedures show how to modify settings using the CLI or console\.

**To create a cluster with spark\.executor\.memory set to 2G using the CLI**
+ Create a cluster with Spark installed and `spark.executor.memory` set to 2G, using the following command, which references a file, `myConfig.json` stored in Amazon S3\.

  ```
  aws emr create-cluster --release-label emr-5.29.0 --applications Name=Spark \
  --instance-type m5.xlarge --instance-count 2 --service-role EMR_DefaultRole --ec2-attributes InstanceProfile=EMR_EC2_DefaultRole --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
      {
        "Classification": "spark-defaults",
        "Properties": {
          "spark.executor.memory": "2G"
        }
      }
    ]
  ```

**To create a cluster with spark\.executor\.memory set to 2G using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Choose **Spark**\. 

1. Under **Edit software settings**, leave **Enter configuration** selected and enter the following configuration:

   ```
   classification=spark-defaults,properties=[spark.executor.memory=2G]
   ```

1. Select other options, choose **** and then choose **Create cluster**\.

**To set maximizeResourceAllocation**
+ Create a cluster with Spark installed and `maximizeResourceAllocation` set to true using the AWS CLI, referencing a file, `myConfig.json`, stored in Amazon S3\.

  ```
  aws emr create-cluster --release-label emr-5.29.0 --applications Name=Spark \
  --instance-type m5.xlarge --instance-count 2 --service-role EMR_DefaultRole --ec2-attributes InstanceProfile=EMR_EC2_DefaultRole --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
    {
      "Classification": "spark",
      "Properties": {
        "maximizeResourceAllocation": "true"
      }
    }
  ]
  ```

**Note**  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.