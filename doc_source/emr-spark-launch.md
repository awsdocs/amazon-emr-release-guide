# Create a Cluster With Spark<a name="emr-spark-launch"></a>

The following procedure creates a cluster with [Spark](https://aws.amazon.com/big-data/what-is-spark/) installed using **Quick Options** in the EMR console\. Use **Advanced Options** to further customize your cluster setup, and use Step execution mode to programmatically install applications and then execute custom applications that you submit as steps\. With either of these advanced options, you can choose to use AWS Glue as your Spark SQL metastore\. See [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md) for more information\.

**To launch a cluster with Spark installed**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster** to use **Quick Create**\.

1.  For **Software Configuration**, choose **Amazon Release Version emr\-5\.15\.0** or later\.

1.  For **Select Applications**, choose either **All Applications** or **Spark**\.

1.  Select other options as necessary and then choose **Create cluster**\.
**Note**  
To configure Spark when you are creating the cluster, see [Configure Spark](emr-spark-configure.md)\.

**To launch a cluster with Spark installed using the AWS CLI**
+ Create the cluster with the following command:

  ```
  aws emr create-cluster --name "Spark cluster" --release-label emr-5.15.0 --applications Name=Spark \
  --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 --use-default-roles
  ```

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

**To launch a cluster with Spark installed using the SDK for Java**

Specify Spark as an application with `SupportedProductConfig` used in `RunJobFlowRequest`\.
+ The following example shows how to create a cluster with Spark using Java\.

  ```
  AmazonElasticMapReduceClient emr = new AmazonElasticMapReduceClient(credentials);
  
  Application sparkApp = new Application()
      .withName("Spark");
  Applications myApps = new Applications();
  myApps.add(sparkApp);
  
  RunJobFlowRequest request = new RunJobFlowRequest()
      .withName("Spark Cluster")
      .withApplications(myApps)
      .withReleaseLabel("emr-5.15.0")
      .withInstances(new JobFlowInstancesConfig()
      .withEc2KeyName("myKeyName")
      .withInstanceCount(1)
          .withKeepJobFlowAliveWhenNoSteps(true)
          .withMasterInstanceType("m4.large")
          .withSlaveInstanceType("m4.large")
      );			
  RunJobFlowResult result = emr.runJobFlow(request);
  ```