# Supplying a Configuration when Creating a Cluster<a name="emr-configure-apps-create-cluster"></a>

When you create a cluster, you can override the default configurations for applications\. To do so, use the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. 

## Supplying a Configuration in the Console when Creating a Cluster<a name="emr-configure-apps-create-cluster-console"></a>

To supply a configuration, navigate to the **Create cluster** page and choose **Edit software settings**\. You can then enter the configuration directly by using either JSON or a shorthand syntax demonstrated in shadow text in the console\. Otherwise, you can provide an Amazon S3 URI for a file with a JSON `Configurations` object\.

To supply a configuration for an instance group, navigate to the **Hardware Configuration** page\. Under the **Instance type** column in the **Node type** table, choose to edit the **Configurations** for applications for each instance group\. 

## Supplying a Configuration Using the AWS CLI when Creating a Cluster<a name="emr-configure-apps-create-cluster-cli"></a>

You can provide a configuration to create\-cluster by supplying a path to a JSON file stored locally or in Amazon S3\. The following example assumes that you are using default roles for Amazon EMR and the roles have been created\. If you need to create the roles, run `aws emr create-default-roles` first\.

```
aws emr create-cluster --use-default-roles --release-label emr-5.29.0 --instance-type m5.xlarge --instance-count 2 --applications Name=Hive --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
```

If your configuration is in your local directory, you can use the following:

```
aws emr create-cluster --use-default-roles --release-label emr-5.29.0 --applications Name=Hive \
--instance-type m5.xlarge --instance-count 3 --configurations file://./configurations.json
```

## Supplying a Configuration Using the Java SDK when Creating a Cluster<a name="emr-configure-apps-create-cluster-sdk"></a>

The following program excerpt shows how to supply a configuration using the AWS SDK for Java:

```
			Application hive = new Application().withName("Hive");

Map<String,String> hiveProperties = new HashMap<String,String>();
	hiveProperties.put("hive.join.emit.interval","1000");
	hiveProperties.put("hive.merge.mapfiles","true");
	    
Configuration myHiveConfig = new Configuration()
	.withClassification("hive-site")
	.withProperties(hiveProperties);

RunJobFlowRequest request = new RunJobFlowRequest()
	.withName("Create cluster with ReleaseLabel")
	.withReleaseLabel("emr-5.20.0")
	.withApplications(hive)
	.withConfigurations(myHiveConfig)
	.withServiceRole("EMR_DefaultRole")
	.withJobFlowRole("EMR_EC2_DefaultRole")
	.withInstances(new JobFlowInstancesConfig()
		.withEc2KeyName("myEc2Key")
		.withInstanceCount(3)
		.withKeepJobFlowAliveWhenNoSteps(true)
		.withMasterInstanceType("m4.large")
		.withSlaveInstanceType("m4.large")
	);
```