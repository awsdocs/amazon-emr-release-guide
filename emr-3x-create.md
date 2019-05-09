# Creating a Cluster With Earlier AMI Versions of Amazon EMR<a name="emr-3x-create"></a>

Amazon EMR 2\.x and 3\.x releases are referenced by AMI version\. With Amazon EMR release 4\.0\.0 and later, releases are referenced by release version, using a release label such as `emr-5.11.0`\. This change is most apparent when you create a cluster using the AWS CLI or programmatically\.

When you use the AWS CLI to create a cluster using an AMI release version, use the `--ami-version` option, for example, `--ami-version 3.11.0`\. Many options, features, and applications introduced in Amazon EMR 4\.0\.0 and later are not available when you specify an `--ami-version`\. For more information, see [create\-cluster](https://docs.aws.amazon.com/cli/latest/reference/emr/create-cluster.html) in the *AWS CLI Command Reference*\. 

The following example AWS CLI command launches a cluster using an AMI version\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.11.0 \
--applications Name=Hue Name=Hive Name=Pig \
--use-default-roles --ec2-attributes KeyName=myKey \
--instance-groups InstanceGroupType=MASTER,InstanceCount=1,\
InstanceType=m3.xlarge InstanceGroupType=CORE,InstanceCount=2,\
InstanceType=m3.xlarge --bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hadoop,\
Name="Configuring infinite JVM reuse",Args=["-m","mapred.job.reuse.jvm.num.tasks=-1"]
```

Programmatically, all Amazon EMR release versions use the `RunJobFlowRequest` action in the EMR API to create clusters\. The following example Java code creates a cluster using AMI release version 3\.11\.0\.

```
RunJobFlowRequest request = new RunJobFlowRequest()
			.withName("AmiVersion Cluster")
			.withAmiVersion("3.11.0")
			.withInstances(new JobFlowInstancesConfig()
				.withEc2KeyName("myKeyPair")
				.withInstanceCount(1)
				.withKeepJobFlowAliveWhenNoSteps(true)
				.withMasterInstanceType("m3.xlarge")
				.withSlaveInstanceType("m3.xlarge");
```

The following `RunJobFlowRequest` call uses a release label instead:

```
RunJobFlowRequest request = new RunJobFlowRequest()
			.withName("ReleaseLabel Cluster")
			.withReleaseLabel("emr-5.23.0")
			.withInstances(new JobFlowInstancesConfig()
				.withEc2KeyName("myKeyPair")
				.withInstanceCount(1)
				.withKeepJobFlowAliveWhenNoSteps(true)
				.withMasterInstanceType("m3.xlarge")
				.withSlaveInstanceType("m3.xlarge");
```

## Configuring Cluster Size<a name="emr-3x-cluster-size"></a>

When your cluster runs, Hadoop determines the number of mapper and reducer tasks needed to process the data\. Larger clusters should have more tasks for better resource use and shorter processing time\. Typically, an EMR cluster remains the same size during the entire cluster; you set the number of tasks when you create the cluster\. When you resize a running cluster, you can vary the processing during the cluster execution\. Therefore, instead of using a fixed number of tasks, you can vary the number of tasks during the life of the cluster\. There are two configuration options to help set the ideal number of tasks:
+ `mapred.map.tasksperslot`
+ `mapred.reduce.tasksperslot`

You can set both options in the `mapred-conf.xml` file\. When you submit a job to the cluster, the job client checks the current total number of map and reduce slots available clusterwide\. The job client then uses the following equations to set the number of tasks: 
+ `mapred.map.tasks` =` mapred.map.tasksperslot` \* map slots in cluster
+ `mapred.reduce.tasks` = `mapred.reduce.tasksperslot` \* reduce slots in cluster

The job client only reads the `tasksperslot` parameter if the number of tasks is not configured\. You can override the number of tasks at any time, either for all clusters via a bootstrap action or individually per job by adding a step to change the configuration\. 

Amazon EMR withstands task node failures and continues cluster execution even if a task node becomes unavailable\. Amazon EMR automatically provisions additional task nodes to replace those that fail\. 

You can have a different number of task nodes for each cluster step\. You can also add a step to a running cluster to modify the number of task nodes\. Because all steps are guaranteed to run sequentially by default, you can specify the number of running task nodes for any step\. 