# Spark Application Specifics With Earlier AMI Versions of Amazon EMR<a name="emr-3x-spark"></a>

## Use Spark Interactively or in Batch Mode<a name="emr-3x-spark-interactive-batch"></a>

Amazon EMR enables you to run Spark applications in two modes: 
+ Interactive
+ Batch

When you launch a long\-running cluster using the console or the AWS CLI, you can connect using SSH into the master node as the Hadoop user and use the Spark shell to develop and run your Spark applications interactively\. Using Spark interactively enables you to prototype or test Spark applications more easily than in a batch environment\. After you successfully revise the Spark application in interactive mode, you can put that application JAR or Python program in the file system local to the master node of the cluster on Amazon S3\. You can then submit the application as a batch workflow\.

In batch mode, upload your Spark script to Amazon S3 or the local master node file system, and then submit the work to the cluster as a step\. Spark steps can be submitted to a long\-running cluster or a transient cluster\.

## Creating a Cluster with Spark Installed<a name="emr-3x-spark-install"></a>

**To launch a cluster with Spark installed using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**\.

1. For **Software Configuration**, choose the AMI release version that you require\.

1.  For **Applications to be installed**, choose **Spark** from the list, then choose **Configure and add**\.

1. Add arguments to change the Spark configuration as desired\. For more information, see [Configure Spark](#emr-3x-spark-configure)\. Choose **Add**\.

1.  Select other options as necessary and then choose **Create cluster**\.

The following example shows how to create a cluster with Spark using Java:

```
AmazonElasticMapReduceClient emr = new AmazonElasticMapReduceClient(credentials);
SupportedProductConfig sparkConfig = new SupportedProductConfig()
			.withName("Spark");

RunJobFlowRequest request = new RunJobFlowRequest()
			.withName("Spark Cluster")
			.withAmiVersion("3.11.0")
			.withNewSupportedProducts(sparkConfig)
			.withInstances(new JobFlowInstancesConfig()
				.withEc2KeyName("myKeyName")
				.withInstanceCount(1)
				.withKeepJobFlowAliveWhenNoSteps(true)
				.withMasterInstanceType("m3.xlarge")
				.withSlaveInstanceType("m3.xlarge")
			);			
RunJobFlowResult result = emr.runJobFlow(request);
```

## Configure Spark<a name="emr-3x-spark-configure"></a>

You configure Spark when you create a cluster by running the bootstrap action located at [awslabs/emr\-bootstrap\-actions/spark repository on Github](https://github.com/awslabs/emr-bootstrap-actions/tree/master/spark)\. For arguments that the bootstrap action accepts, see the [README](https://github.com/awslabs/emr-bootstrap-actions/blob/master/spark/README.md)in that repository\. The bootstrap action configures properties in the `$SPARK_CONF_DIR/spark-defaults.conf` file\. For more information about settings, see the Spark Configuration topic in Spark documentation\. You can replace "latest" in the following URL with the version number of Spark that you are installing, for example, `2.2.0` [http://spark.apache.org/docs/latest/configuration.html](http://spark.apache.org/docs/latest/configuration.html)\.

You can also configure Spark dynamically at the time of each application submission\. A setting to automatically maximize the resource allocation for an executor is available using the `spark` configuration file\. For more information, see [Overriding Spark Default Configuration Settings](#emr-3x-spark-dynamic-configuration)\.

### Changing Spark Default Settings<a name="emr-3x-spark-default-settings"></a>

The following example shows how to create a cluster with `spark.executor.memory` set to 2G using the AWS CLI\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Spark cluster" --ami-version 3.11.0 \
--applications Name=Spark, Args=[-d,spark.executor.memory=2G] --ec2-attributes KeyName=myKey \
--instance-type m3.xlarge --instance-count 3 --use-default-roles
```

### Submit Work to Spark<a name="emr-3x-spark-submit-work"></a>

To submit work to a cluster, use a step to run the `spark-submit` script on your EMR cluster\. Add the step using the `addJobFlowSteps` method in [AmazonElasticMapReduceClient](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/elasticmapreduce/AmazonElasticMapReduceClient.html):

```
AWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
AmazonElasticMapReduceClient emr = new AmazonElasticMapReduceClient(credentials);
StepFactory stepFactory = new StepFactory();
AddJobFlowStepsRequest req = new AddJobFlowStepsRequest();
req.withJobFlowId("j-1K48XXXXXXHCB");

List<StepConfig> stepConfigs = new ArrayList<StepConfig>();
		
StepConfig sparkStep = new StepConfig()
	.withName("Spark Step")
	.withActionOnFailure("CONTINUE")
	.withHadoopJarStep(stepFactory.newScriptRunnerStep("/home/hadoop/spark/bin/spark-submit","--class","org.apache.spark.examples.SparkPi","/home/hadoop/spark/lib/spark-examples-1.3.1-hadoop2.4.0.jar","10"));

stepConfigs.add(sparkStep);
req.withSteps(stepConfigs);
AddJobFlowStepsResult result = emr.addJobFlowSteps(req);
```

### Overriding Spark Default Configuration Settings<a name="emr-3x-spark-dynamic-configuration"></a>

You may want to override Spark default configuration values on a per\-application basis\. You can do this when you submit applications using a step, which essentially passes options to `spark-submit`\. For example, you may wish to change the memory allocated to an executor process by changing `spark.executor.memory`\. You can supply the `--executor-memory` switch with an argument like the following:

```
/home/hadoop/spark/bin/spark-submit --executor-memory 1g --class org.apache.spark.examples.SparkPi /home/hadoop/spark/lib/spark-examples*.jar 10
```

Similarly, you can tune `--executor-cores` and `--driver-memory`\. In a step, you would provide the following arguments to the step:

```
--executor-memory 1g --class org.apache.spark.examples.SparkPi /home/hadoop/spark/lib/spark-examples*.jar 10
```

You can also tune settings that may not have a built\-in switch using the `--conf` option\. For more information about other settings that are tunable, see the [Dynamically Loading Spark Properties](https://spark.apache.org/docs/latest/configuration.html#dynamically-loading-spark-properties) topic in the Apache Spark documentation\.