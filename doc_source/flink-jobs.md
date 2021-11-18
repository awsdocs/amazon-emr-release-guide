# Working with Flink jobs in Amazon EMR<a name="flink-jobs"></a>

There are several ways to interact with Flink on Amazon EMR: through the console, the Flink interface found on the ResourceManager Tracking UI, and at the command line\. All of these allow you to submit a JAR file to a Flink application\. Once submitted, a JAR files become a job managed by the Flink JobManager, which is located on the YARN node that hosts the Flink session Application Master daemon\.

You can run a Flink application as a YARN job on a long\-running cluster or on a transient cluster\. On a long\-running cluster, you can submit multiple Flink jobs to one Flink cluster running on Amazon EMR\. If you run a Flink job on a transient cluster, your Amazon EMR cluster exists only for the time it takes to run the Flink application, so you are only charged for the resources and time used\. You can submit a Flink job using the Amazon EMR `AddSteps` API operation, as a step argument to the `RunJobFlow` operation, and through the AWS CLI `add-steps` or `create-cluster` commands\.

## Start a Flink YARN application as a step on a long\-running cluster<a name="flink-add-step"></a>

To start a Flink application that multiple clients can submit work to through YARN API operations, you need to either create a cluster or add a Flink application an existing cluster\. For instructions on how to create a new cluster, see [Creating a cluster with Flink](flink-create-cluster.md)\. To start a YARN session on an existing cluster, use the following steps from the console, AWS CLI, or Java SDK\.

**Note**  
The `flink-yarn-session` command was added in Amazon EMR version 5\.5\.0 as a wrapper for the `yarn-session.sh` script to simplify execution\. If you use an earlier version of Amazon EMR, substitute `bash -c "/usr/lib/flink/bin/yarn-session.sh -d"` for **Arguments** in the console or `Args`\. in the AWS CLI command\.

**To submit a Flink job on an existing cluster using the console**

Submit the Flink session using the `flink-yarn-session` command in an existing cluster\.

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the cluster list, select the cluster you previously launched\.

1. In the cluster details page, choose **Steps**, **Add Step**\.

1. Enter parameters using the guidelines that follow and then choose **Add**\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/flink-jobs.html)

**To submit a Flink job on an existing cluster using the AWS CLI**
+ To add a Flink job to a long\-running cluster within EMR, use the `add-steps` command:

  ```
  aws emr add-steps --cluster-id j-XXXXXXXX --steps Type=CUSTOM_JAR,Name=CustomJAR,ActionOnFailure=CONTINUE,Jar=s3://mybucket/mytest.jar,Args=arg1,arg2,arg3 Type=CUSTOM_JAR,Name=CustomJAR,ActionOnFailure=CONTINUE,Jar=s3://mybucket/mytest.jar,MainClass=mymainclass,Args=flink-yarn-session -d
  ```

## Submit work to an existing Flink application on a long\-running cluster<a name="flink-submit-work"></a>

If you already have an existing Flink application on a long\-running cluster, you can specify the cluster's Flink application ID in order to submit work to it\. To obtain the application ID, run `yarn application -list` on the AWS CLI or through the [YarnClient](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/yarn/client/api/YarnClient.html) API operation:

```
$ yarn application -list
16/09/07 19:32:13 INFO client.RMProxy: Connecting to ResourceManager at ip-10-181-83-19.ec2.internal/10.181.83.19:8032
Total number of applications (application-types: [] and states: [SUBMITTED, ACCEPTED, RUNNING]):1
Application-Id    Application-Name    Application-Type    User    Queue    State    Final-State    Progress    Tracking-URL
application_1473169569237_0002    Flink session with 14 TaskManagers (detached)	        Apache Flink	    hadoop	   default	           RUNNING	         UNDEFINED	           100%	http://ip-10-136-154-194.ec2.internal:33089
```

The application ID for this Flink session is `application_1473169569237_0002`, which you can use to submit work to the application using the AWS CLI or an SDK\.

**Example SDK for Java**  

```
List<StepConfig> stepConfigs = new ArrayList<StepConfig>();
  
HadoopJarStepConfig flinkWordCountConf = new HadoopJarStepConfig()
    .withJar("command-runner.jar")
    .withArgs("flink", "run", "-m", "yarn-cluster", "-yid", "application_1473169569237_0002", "-yn", "2", "/usr/lib/flink/examples/streaming/WordCount.jar", 
      "--input", "s3://myBucket/pg11.txt", "--output", "s3://myBucket/alice2/");
  
StepConfig flinkRunWordCount = new StepConfig()
  .withName("Flink add a wordcount step")
  .withActionOnFailure("CONTINUE")
  .withHadoopJarStep(flinkWordCountConf);
  
stepConfigs.add(flinkRunWordCount); 
  
AddJobFlowStepsResult res = emr.addJobFlowSteps(new AddJobFlowStepsRequest()
   .withJobFlowId("myClusterId")
   .withSteps(stepConfigs));
```

**Example AWS CLI**  

```
aws emr add-steps --cluster-id myClusterId \
--steps Type=CUSTOM_JAR,Name=Flink_Submit_To_Long_Running,Jar=command-runner.jar,\
Args="flink","run","-m","yarn-cluster","-yid","application_1473169569237_0002",\
"/usr/lib/flink/examples/streaming/WordCount.jar",\
"--input","s3://myBucket/pg11.txt","--output","s3://myBucket/alice2/" \
--region myRegion
```

## Submit a transient Flink job<a name="flink-transient-job"></a>

The following examples launch a transient cluster that runs a Flink job and then terminates on completion\.

**Example SDK for Java**  

```
import java.util.ArrayList;
import java.util.List;
import com.amazonaws.AmazonClientException;
import com.amazonaws.auth.AWSCredentials;
import com.amazonaws.auth.AWSStaticCredentialsProvider;
import com.amazonaws.auth.profile.ProfileCredentialsProvider;
import com.amazonaws.services.elasticmapreduce.AmazonElasticMapReduce;
import com.amazonaws.services.elasticmapreduce.AmazonElasticMapReduceClientBuilder;
import com.amazonaws.services.elasticmapreduce.model.*;

public class Main_test {

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
        
		List<StepConfig> stepConfigs = new ArrayList<StepConfig>();
	    HadoopJarStepConfig flinkWordCountConf = new HadoopJarStepConfig()
	      .withJar("command-runner.jar")
	      .withArgs("bash","-c", "flink", "run", "-m", "yarn-cluster", "-yn", "2", "/usr/lib/flink/examples/streaming/WordCount.jar", "--input", "s3://path/to/input-file.txt", "--output", "s3://path/to/output/");
	    
	    StepConfig flinkRunWordCountStep = new StepConfig()
	      .withName("Flink add a wordcount step and terminate")
	      .withActionOnFailure("CONTINUE")
	      .withHadoopJarStep(flinkWordCountConf);
	    
	    stepConfigs.add(flinkRunWordCountStep); 
	    
	    Application flink = new Application().withName("Flink");
	    
	    RunJobFlowRequest request = new RunJobFlowRequest()
	      .withName("flink-transient")
	      .withReleaseLabel("emr-5.20.0")
	      .withApplications(flink)
	      .withServiceRole("EMR_DefaultRole")
	      .withJobFlowRole("EMR_EC2_DefaultRole")
	      .withLogUri("s3://path/to/my/logfiles")
	      .withInstances(new JobFlowInstancesConfig()
	          .withEc2KeyName("myEc2Key")
	          .withEc2SubnetId("subnet-12ab3c45")
	          .withInstanceCount(3)
	          .withKeepJobFlowAliveWhenNoSteps(false)
	          .withMasterInstanceType("m4.large")
	          .withSlaveInstanceType("m4.large"))
	      .withSteps(stepConfigs);
	    
	    RunJobFlowResult result = emr.runJobFlow(request);  
		System.out.println("The cluster ID is " + result.toString());

	}

}
```

**Example AWS CLI**  
Use the `create-cluster` subcommand to create a transient cluster that terminates when the Flink job completes:  

```
aws emr create-cluster --release-label emr-5.2.1 \
--name "Flink_Transient" \
--applications Name=Flink \
--configurations file://./configurations.json \
--region us-east-1 \
--log-uri s3://myLogUri \
--auto-terminate
--instance-type m5.xlarge \
--instance-count 2 \
--service-role EMR_DefaultRole \ 
--ec2-attributes KeyName=YourKeyName,InstanceProfile=EMR_EC2_DefaultRole \
--steps Type=CUSTOM_JAR,Jar=command-runner.jar,Name=Flink_Long_Running_Session,\
Args="bash","-c","\"flink run -m yarn-cluster /usr/lib/flink/examples/streaming/WordCount.jar
--input s3://myBucket/pg11.txt --output s3://myBucket/alice/""
```