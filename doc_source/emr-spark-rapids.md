# Using the Nvidia Spark\-RAPIDS Accelerator for Spark<a name="emr-spark-rapids"></a>

With Amazon EMR release version 6\.2\.0 and later, you can use Nvidia's [RAPIDS](https://nvidia.github.io/spark-rapids/) Accelerator for Apache Spark plugin to accelerate Spark using EC2 graphics processing unit \(GPU\) instance types\. Rapids Accelerator will GPU\-accelerate your Apache Spark 3\.0 data science pipelines without code changes and speed up data processing and model training, while substantially lowering infrastructure costs\. 

The following sections guide you through configuring your EMR cluster to use the Spark\-RAPIDS Plugin for Spark\.

## Choose instance types<a name="emr-spark-rapids-instancetypes"></a>

To use the Nvidia Spark\-RAPIDS plugin for Spark, the core and task instance groups must use EC2 GPU instance types that meet the [Hardware requirements](https://nvidia.github.io/spark-rapids/) of Spark\-RAPIDS\. To view a complete list of EMR supported GPU instance types, please see [Supported instance types](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-supported-instance-types.html) in the *Amazon EMR Management Guide*\. Instance type for the master instance group can be either GPU or non\-GPU types, but ARM instance types aren't supported\.

## Set up application configurations for your cluster<a name="emr-spark-rapids-appconfig"></a>

**1\. Enable Amazon EMR to install the plugins on your new cluster**

To install plugins, supply the following configuration when creating your cluster:

```
{
	"Classification":"spark",
	"Properties":{
		"enableSparkRapids":"true"
	}
}
```

**2\. Configure YARN to use GPU**

For details on using GPU on YARN, see [Using GPU on YARN](https://hadoop.apache.org/docs/r3.2.1/hadoop-yarn/hadoop-yarn-site/UsingGpus.html) in Apache Hadoop documentation\. Here's a sample configuration:

```
{
	"Classification":"yarn-site",
	"Properties":{
		"yarn.nodemanager.resource-plugins":"yarn.io/gpu",
		"yarn.resource-types":"yarn.io/gpu",
		"yarn.nodemanager.resource-plugins.gpu.allowed-gpu-devices":"auto",
		"yarn.nodemanager.resource-plugins.gpu.path-to-discovery-executables":"/usr/bin",
		"yarn.nodemanager.linux-container-executor.cgroups.mount":"true",
		"yarn.nodemanager.linux-container-executor.cgroups.mount-path":"/sys/fs/cgroup",
		"yarn.nodemanager.linux-container-executor.cgroups.hierarchy":"yarn",
		"yarn.nodemanager.container-executor.class":"org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor"
	}
},
{
	"Classification":"container-executor",
	"Properties":{
		
	},
	"Configurations":[
		{
			"Classification":"gpu",
			"Properties":{
				"module.enabled":"true"
			}
		},
		{
			"Classification":"cgroups",
			"Properties":{
				"root":"/sys/fs/cgroup",
				"yarn-hierarchy":"yarn"
			}
		}
	]
}
```

**3\. Configure Spark to use RAPIDS**

Here are the required configurations to enable Spark to use RAPIDS plugin:

```
{
	"Classification":"spark-defaults",
	"Properties":{
		"spark.plugins":"com.nvidia.spark.SQLPlugin",
		"spark.sql.sources.useV1SourceList":"",
		"spark.executor.resource.gpu.discoveryScript":"/usr/lib/spark/scripts/gpu/getGpusResources.sh",
		"spark.executor.extraLibraryPath":"/usr/local/cuda/targets/x86_64-linux/lib:/usr/local/cuda/extras/CUPTI/lib64:/usr/local/cuda/compat/lib:/usr/local/cuda/lib:/usr/local/cuda/lib64:/usr/lib/hadoop/lib/native:/usr/lib/hadoop-lzo/lib/native:/docker/usr/lib/hadoop/lib/native:/docker/usr/lib/hadoop-lzo/lib/native"
	}
}
```

[XGBoost4J\-Spark library](https://xgboost.readthedocs.io/en/latest/jvm/xgboost4j_spark_tutorial.html) in XGBoost documentation is also available when the Spark RAPIDS plugin is enabled on your cluster\. You can use the following configuration to integrate XGBoost with you Spark job:

```
{
	"Classification":"spark-defaults",
	"Properties":{
		"spark.submit.pyFiles":"/usr/lib/spark/jars/xgboost4j-spark_3.0-1.0.0-0.2.0.jar"
	}
}
```

For additional Spark configurations that you can use to tune a GPU\-accelerated EMR cluster, please refer to the [Rapids Accelerator for Apache Spark tuning guide](https://nvidia.github.io/spark-rapids/docs/tuning-guide.html) in Nvidia\.github\.io documentation\.

**4\. Configure YARN Capacity Scheduler**

`DominantResourceCalculator` must be configured to enable GPU scheduling and isolation\. For more information, please refer to [Using GPU on YARN](https://hadoop.apache.org/docs/r3.2.1/hadoop-yarn/hadoop-yarn-site/UsingGpus.html) in Apache Hadoop documentation\.

```
{
	"Classification":"capacity-scheduler",
	"Properties":{
		"yarn.scheduler.capacity.resource-calculator":"org.apache.hadoop.yarn.util.resource.DominantResourceCalculator"
	}
}
```

**5\. Create a JSON File to Include All Your Configurations**

You can create a JSON file that contains your configuration for using the RAPIDS plugin for your Spark cluster\. You supply the file later when launching your cluster\.

The file can be stored locally or on S3\. For more information of how to supply application configurations for your clusters, see [Configure applications](emr-configure-apps.md)\.

The following is a sample file named `my-configurations.json`\. You can use it as a template to start building your own configurations\.

```
[
	{
		"Classification":"spark",
		"Properties":{
			"enableSparkRapids":"true"
		}
	},
	{
		"Classification":"yarn-site",
		"Properties":{
			"yarn.nodemanager.resource-plugins":"yarn.io/gpu",
			"yarn.resource-types":"yarn.io/gpu",
			"yarn.nodemanager.resource-plugins.gpu.allowed-gpu-devices":"auto",
			"yarn.nodemanager.resource-plugins.gpu.path-to-discovery-executables":"/usr/bin",
			"yarn.nodemanager.linux-container-executor.cgroups.mount":"true",
			"yarn.nodemanager.linux-container-executor.cgroups.mount-path":"/sys/fs/cgroup",
			"yarn.nodemanager.linux-container-executor.cgroups.hierarchy":"yarn",
			"yarn.nodemanager.container-executor.class":"org.apache.hadoop.yarn.server.nodemanager.LinuxContainerExecutor"
		}
	},
	{
		"Classification":"container-executor",
		"Properties":{
			
		},
		"Configurations":[
			{
				"Classification":"gpu",
				"Properties":{
					"module.enabled":"true"
				}
			},
			{
				"Classification":"cgroups",
				"Properties":{
					"root":"/sys/fs/cgroup",
					"yarn-hierarchy":"yarn"
				}
			}
		]
	},
	{
		"Classification":"spark-defaults",
		"Properties":{
			"spark.plugins":"com.nvidia.spark.SQLPlugin",
			"spark.sql.sources.useV1SourceList":"",
			"spark.executor.resource.gpu.discoveryScript":"/usr/lib/spark/scripts/gpu/getGpusResources.sh",
			"spark.executor.extraLibraryPath":"/usr/local/cuda/targets/x86_64-linux/lib:/usr/local/cuda/extras/CUPTI/lib64:/usr/local/cuda/compat/lib:/usr/local/cuda/lib:/usr/local/cuda/lib64:/usr/lib/hadoop/lib/native:/usr/lib/hadoop-lzo/lib/native:/docker/usr/lib/hadoop/lib/native:/docker/usr/lib/hadoop-lzo/lib/native",
			"spark.submit.pyFiles":"/usr/lib/spark/jars/xgboost4j-spark_3.0-1.0.0-0.2.0.jar",
			"spark.rapids.sql.concurrentGpuTasks":"1",
			"spark.executor.resource.gpu.amount":"1",
			"spark.executor.cores":"2",
			"spark.task.cpus ":"1",
			"spark.task.resource.gpu.amount":"0.5",
			"spark.rapids.memory.pinnedPool.size":"0",
			"spark.executor.memoryOverhead":"2G",
			"spark.locality.wait":"0s",
			"spark.sql.shuffle.partitions":"200",
			"spark.sql.files.maxPartitionBytes":"512m"
		}
	},
	{
		"Classification":"capacity-scheduler",
		"Properties":{
			"yarn.scheduler.capacity.resource-calculator":"org.apache.hadoop.yarn.util.resource.DominantResourceCalculator"
		}
	}
]
```

## Add a bootstrap action for your cluster<a name="emr-spark-rapids-bootstrap"></a>

In order to use YARN on GPU, you need to open cgroups permissions to YARN on your cluster, which can be done using an EMR bootstrap action script\.

For more information on how to supply bootstrap action scripts when creating your cluster, see [Bootstrap action basics](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html#bootstrapUses) in the *Amazon EMR Management Guide*\.

Here's an example script named `my-bootstap-action.json`:

```
#!/bin/bash
 
set -ex
 
sudo chmod a+rwx -R /sys/fs/cgroup/cpu,cpuacct
sudo chmod a+rwx -R /sys/fs/cgroup/devices
```

## Launch your cluster<a name="emr-spark-rapids-launchcluster"></a>

The last step is to launch your cluster with the cluster configurations mentioned above\. Here's an example command to launch a cluster via EMR CLI:

```
 aws emr create-cluster \
--release-label emr-6.2.0 \
--applications Name=Hadoop Name=Spark \
--service-role EMR_DefaultRole \
--ec2-attributes KeyName=my-key-pair,InstanceProfile=EMR_EC2_DefaultRole \
--instance-groups InstanceGroupType=MASTER,InstanceCount=1,InstanceType=m4.4xlarge \                 
                  InstanceGroupType=CORE,InstanceCount=1,InstanceType=g4dn.2xlarge \    
                  InstanceGroupType=TASK,InstanceCount=1,InstanceType=g4dn.2xlarge \
--configurations file:///my-configurations.json \
--bootstrap-actions Name='My Spark Rapids Bootstrap action',Path=s3://my-bucket/my-bootstrap-action.sh
```