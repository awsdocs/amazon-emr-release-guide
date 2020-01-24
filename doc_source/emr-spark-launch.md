# Create a Cluster With Spark<a name="emr-spark-launch"></a>

The following procedure creates a cluster with [Spark](https://aws.amazon.com/big-data/what-is-spark/) installed using **Quick Options** in the EMR console\. Use **Advanced Options** to further customize your cluster setup, and use Step execution mode to programmatically install applications and then execute custom applications that you submit as steps\. With either of these advanced options, you can choose to use AWS Glue as your Spark SQL metastore\. See [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md) for more information\.

**To launch a cluster with Spark installed**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster** to use **Quick Create**\.

1.  For **Software Configuration**, choose **Amazon Release Version *emr\-5\.29\.0*** or later\.

1.  For **Select Applications**, choose either **All Applications** or **Spark**\.

1.  Select other options as necessary and then choose **Create cluster**\.
**Note**  
To configure Spark when you are creating the cluster, see [Configure Spark](emr-spark-configure.md)\.

**To launch a cluster with Spark installed using the AWS CLI**
+ Create the cluster with the following command:

  ```
  aws emr create-cluster --name "Spark cluster" --release-label emr-5.29.0 --applications Name=Spark \
  --ec2-attributes KeyName=myKey --instance-type m5.xlarge --instance-count 3 --use-default-roles
  ```

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

**To launch a cluster with Spark installed using the SDK for Java**

Specify Spark as an application with `SupportedProductConfig` used in `RunJobFlowRequest`\.
+ The following example shows how to create a cluster with Spark using Java\.

  ```
  import com.amazonaws.AmazonClientException;
  import com.amazonaws.auth.AWSCredentials;
  import com.amazonaws.auth.AWSStaticCredentialsProvider;
  import com.amazonaws.auth.profile.ProfileCredentialsProvider;
  import com.amazonaws.services.elasticmapreduce.AmazonElasticMapReduce;
  import com.amazonaws.services.elasticmapreduce.AmazonElasticMapReduceClientBuilder;
  import com.amazonaws.services.elasticmapreduce.model.*;
  import com.amazonaws.services.elasticmapreduce.util.StepFactory;
  
  public class Main {
  
  	public static void main(String[] args) {
  		AWSCredentials credentials_profile = null;		
  		try {
  			credentials_profile = new ProfileCredentialsProvider("default").getCredentials();
          } catch (Exception e) {
              throw new AmazonClientException(
                      "Cannot load credentials from .aws/credentials file. " +
                      "Make sure that the credentials file exists and the profile name is specified within it.",
                      e);
          }
          
          AmazonElasticMapReduce emr = AmazonElasticMapReduceClientBuilder.standard()
  			.withCredentials(new AWSStaticCredentialsProvider(credentials_profile))
  			.withRegion(Regions.US_WEST_1)
  			.build();
          
          // create a step to enable debugging in the AWS Management Console
  		StepFactory stepFactory = new StepFactory(); 
  		StepConfig enabledebugging = new StepConfig()
     			.withName("Enable debugging")
     			.withActionOnFailure("TERMINATE_JOB_FLOW")
     			.withHadoopJarStep(stepFactory.newEnableDebuggingStep());
          
          Application spark = new Application().withName("Spark");
  
          RunJobFlowRequest request = new RunJobFlowRequest()
              .withName("Spark Cluster")
              .withReleaseLabel("emr-5.20.0")
              .withSteps(enabledebugging)
              .withApplications(spark)
              .withLogUri("s3://path/to/my/logs/")
  	       	.withServiceRole("EMR_DefaultRole") 
  	       	.withJobFlowRole("EMR_EC2_DefaultRole") 
              .withInstances(new JobFlowInstancesConfig()
                  .withEc2SubnetId("subnet-12ab3c45")
                  .withEc2KeyName("myEc2Key")
                  .withInstanceCount(3)
                  .withKeepJobFlowAliveWhenNoSteps(true)
                  .withMasterInstanceType("m4.large")
                  .withSlaveInstanceType("m4.large")
              );			
          RunJobFlowResult result = emr.runJobFlow(request);  
  	    System.out.println("The cluster ID is " + result.toString());
  	}
  }
  ```