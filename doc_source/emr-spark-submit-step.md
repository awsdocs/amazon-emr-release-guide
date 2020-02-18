# Adding a Spark Step<a name="emr-spark-submit-step"></a>

You can use Amazon EMR steps to submit work to the Spark framework installed on an EMR cluster\. For more information, see [Steps](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-overview.html#emr-overview-data-processing) in the Amazon EMR Management Guide\. In the console and CLI, you do this using a Spark application step, which runs the `spark-submit` script as a step on your behalf\. With the API, you use a step to invoke `spark-submit` using `command-runner.jar`\.

For more information about submitting applications to Spark, see the [Submitting Applications](https://spark.apache.org/docs/latest/submitting-applications.html) topic in the Apache Spark documentation\.

**To submit a Spark step using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the **Cluster List**, choose the name of your cluster\.

1. Scroll to the **Steps** section and expand it, then choose **Add step**\.

1. In the **Add Step** dialog box:
   + For **Step type**, choose **Spark application**\.
   + For **Name**, accept the default name \(Spark application\) or type a new name\.
   + For **Deploy mode**, choose **Client** or **Cluster** mode\. Client mode launches the driver program on the cluster's master instance, while cluster mode launches your driver program on the cluster\. For client mode, the driver's log output appears in the step logs, while for cluster mode, the driver's log output appears in the logs for the first YARN container\. For more information, see [Cluster Mode Overview](https://spark.apache.org/docs/latest/cluster-overview.html) in the Apache Spark documentation\.
   + Specify the desired **Spark\-submit options**\. For more information about `spark-submit` options, see [Launching Applications with spark\-submit](https://spark.apache.org/docs/latest/submitting-applications.html#launching-applications-with-spark-submit)\.
   + For **Application location**, specify the local or S3 URI path of the application\.
   + For **Arguments**, leave the field blank\.
   + For **Action on failure**, accept the default option \(**Continue**\)\.

1. Choose **Add**\. The step appears in the console with a status of Pending\. 

1. The status of the step changes from **Pending** to **Running** to **Completed** as the step runs\. To update the status, choose the **Refresh** icon above the **Actions** column\. 

1. The results of the step are located in the Amazon EMR console Cluster Details page next to your step under **Log Files** if you have logging configured\. You can optionally find step information in the log bucket you configured when you launched the cluster\. 

**To submit work to Spark using the AWS CLI**

Submit a step when you create the cluster or use the `aws emr add-steps` subcommand in an existing cluster\. 

1. Use `create-cluster` as shown in the following example\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

   ```
   aws emr create-cluster --name "Add Spark Step Cluster" --release-label emr-5.29.0 --applications Name=Spark \
   --ec2-attributes KeyName=myKey --instance-type m5.xlarge --instance-count 3 \
   --steps Type=Spark,Name="Spark Program",ActionOnFailure=CONTINUE,Args=[--class,org.apache.spark.examples.SparkPi,/usr/lib/spark/examples/jars/spark-examples.jar,10] --use-default-roles
   ```

   As an alternative, you can use `command-runner.jar` as shown in the following example\.

   ```
   aws emr create-cluster --name "Add Spark Step Cluster" --release-label emr-5.29.0 \
   --applications Name=Spark --ec2-attributes KeyName=myKey --instance-type m5.xlarge --instance-count 3 \
   --steps Type=CUSTOM_JAR,Name="Spark Program",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[spark-example,SparkPi,10] --use-default-roles
   ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

1. Alternatively, add steps to a cluster already running\. Use `add-steps`\.

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF --steps Type=Spark,Name="Spark Program",ActionOnFailure=CONTINUE,Args=[--class,org.apache.spark.examples.SparkPi,/usr/lib/spark/examples/jars/spark-examples.jar,10]
   ```

   As an alternative, you can use `command-runner.jar` as shown in the following example\.

   ```
   aws emr add-steps --cluster-id j-2AXXXXXXGAPLF --steps Type=CUSTOM_JAR,Name="Spark Program",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[spark-example,SparkPi,10]
   ```

**To submit work to Spark using the SDK for Java**
+ 

  ```
  AWSCredentials credentials = new BasicAWSCredentials(accessKey, secretKey);
  AmazonElasticMapReduce emr = new AmazonElasticMapReduceClient(credentials);
   
  StepFactory stepFactory = new StepFactory();
  AmazonElasticMapReduceClient emr = new AmazonElasticMapReduceClient(credentials);
  AddJobFlowStepsRequest req = new AddJobFlowStepsRequest();
  req.withJobFlowId("j-1K48XXXXXXHCB");
  
  List<StepConfig> stepConfigs = new ArrayList<StepConfig>();
  		
  HadoopJarStepConfig sparkStepConf = new HadoopJarStepConfig()
  			.withJar("command-runner.jar")
  			.withArgs("spark-submit","--executor-memory","1g","--class","org.apache.spark.examples.SparkPi","/usr/lib/spark/examples/jars/spark-examples.jar","10");			
  		
  StepConfig sparkStep = new StepConfig()
  			.withName("Spark Step")
  			.withActionOnFailure("CONTINUE")
  			.withHadoopJarStep(sparkStepConf);
  
  stepConfigs.add(sparkStep);
  req.withSteps(stepConfigs);
  AddJobFlowStepsResult result = emr.addJobFlowSteps(req);
  ```

View the results of the step by examining the logs for the step\. You can do this in the AWS Management Console if you have enabled logging by choosing **Steps**, selecting your step, and then, for **Log files**, choosing either `stdout` or `stderr`\. To see the logs available, choose **View Logs**\.

## Overriding Spark Default Configuration Settings<a name="dynamic-configuration"></a>

You may want to override Spark default configuration values on a per\-application basis\. You can do this when you submit applications using a step, which essentially passes options to `spark-submit`\. For example, you may wish to change the memory allocated to an executor process by changing `spark.executor.memory`\. You would supply the `--executor-memory` switch with an argument like the following:

```
spark-submit --executor-memory 1g --class org.apache.spark.examples.SparkPi /usr/lib/spark/examples/jars/spark-examples.jar 10
```

Similarly, you can tune `--executor-cores` and `--driver-memory`\. In a step, you would provide the following arguments to the step:

```
spark-submit --executor-cores 2 --driver-memory 1g --class org.apache.spark.examples.SparkPi /usr/lib/spark/examples/jars/spark-examples.jar 10
```

You can also tune settings that may not have a built\-in switch using the `--conf` option\. For more information about other settings that are tunable, see the [Dynamically Loading Spark Properties](https://spark.apache.org/docs/latest/configuration.html#dynamically-loading-spark-properties) topic in the Apache Spark documentation\.
