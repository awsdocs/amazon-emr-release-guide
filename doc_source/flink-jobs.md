# Working with Flink Jobs in Amazon EMR<a name="flink-jobs"></a>

There are several ways to interact with Flink on Amazon EMR: through Amazon EMR steps, the Flink interface found on the ResourceManager Tracking UI, and at the command line\. All of these also allow you to submit a JAR file of a Flink application to run\.

Additionally, you can run Flink applications as a long\-running YARN job or as a transient cluster\. In a long\-running job, you can submit multiple Flink applications to one Flink cluster running on Amazon EMR\. If you run Flink as a transient job, your Amazon EMR cluster exists only for the time it takes to run the Flink application, so you are only charged for the resources and time used\. In either case, you can submit a Flink job using the Amazon EMR `AddSteps` API operation, or as a step argument to the `RunJobFlow` operation or AWS CLI `create-cluster` command\.

## Start a Flink Long\-Running YARN Job as a Step<a name="flink-long-running-jobs"></a>

You may want to start a long\-running Flink job that multiple clients can submit to through YARN API operations\. You start a Flink YARN session and submit jobs to the Flink JobManager, which is located on the YARN node that hosts the Flink session Application Master daemon\. To start a YARN session, use the following steps from the console, AWS CLI, or Java SDK\.

**To submit a long\-running job using the console**

Submit the long\-running Flink session using the `flink-yarn-session` command in an existing cluster\.
**Note**  
The `flink-yarn-session` command was added in Amazon EMR version 5\.5\.0 as a wrapper for the `yarn-session.sh` script to simplify execution\. If you use an earlier version of Amazon EMR, substitute `bash -c "/usr/lib/flink/bin/yarn-session.sh -n 2 -d"` for **Argument** in the steps that follow\.

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the cluster list, select the cluster you previously launched\.

1. In the cluster details page, choose **Steps**, **Add Step**\.

1. Enter parameters using the guidelines that follow and then choose **Add**\.  
****    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/flink-jobs.html)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/flink-long-running.png)

**To submit a long\-running Flink job using the AWS CLI**
+ To launch a long\-running Flink cluster within EMR, use the `create-cluster` command:

  ```
  aws emr create-cluster --release-label emr-5.29.0 \
  --applications Name=Flink \
  --configurations file://./configurations.json \
  --region us-east-1 \
  --log-uri s3://myLogUri \
  --instance-type m5.xlarge \
  --instance-count 2 \
  --service-role EMR_DefaultRole \ 
  --ec2-attributes KeyName=MyKeyName,InstanceProfile=EMR_EC2_DefaultRole \
  --steps Type=CUSTOM_JAR,Jar=command-runner.jar,Name=Flink_Long_Running_Session,\
  Args=flink-yarn-session,-n,2,-d
  ```

## Submit Work to an Existing, Long\-Running Flink YARN Job<a name="flink-submit-work"></a>

You can submit work using a command\-line option but you can also use Flink’s native interface proxied through the YARN ResourceManager\. To submit through an EMR step using the Flink CLI, specify the long\-running Flink cluster’s YARN application ID\. To do this, run `yarn application –list` on the EMR command line or through the [YarnClient](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/yarn/client/api/YarnClient.html) API operation:

```
$ yarn application -list
16/09/07 19:32:13 INFO client.RMProxy: Connecting to ResourceManager at ip-10-181-83-19.ec2.internal/10.181.83.19:8032
Total number of applications (application-types: [] and states: [SUBMITTED, ACCEPTED, RUNNING]):1
Application-Id    Application-Name    Application-Type    User    Queue    State    Final-State    Progress    Tracking-URL
application_1473169569237_0002    Flink session with 14 TaskManagers (detached)	        Apache Flink	    hadoop	   default	           RUNNING	         UNDEFINED	           100%	http://ip-10-136-154-194.ec2.internal:33089
```

**Example SDK for Java**  

```
List<StepConfig> stepConfigs = new ArrayList<StepConfig>();
  
HadoopJarStepConfig flinkWordCountConf = new HadoopJarStepConfig()
    .withJar("command-runner.jar")
    .withArgs("flink", "run", "-m", "yarn-cluster", “-yid”, “application_1473169569237_0002”, "-yn", "2", "/usr/lib/flink/examples/streaming/WordCount.jar", 
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
Use the `add-steps` subcommand to submit new jobs to an existing Flink cluster:  

```
aws emr add-steps --cluster-id myClusterId \
--steps Type=CUSTOM_JAR,Name=Flink_Submit_To_Long_Running,Jar=command-runner.jar,\
Args="flink","run","-m","yarn-cluster","-yid","application_1473169569237_0002","-yn","2",\
"/usr/lib/flink/examples/streaming/WordCount.jar",\
"--input","s3://myBucket/pg11.txt","--output","s3://myBucket/alice2/" \
--region myRegion
```

## Submit a Transient Flink Job<a name="flink-transient-job"></a>

The following example launches the Flink WordCount example by adding a step to an existing cluster\. 

**Example Console**  
In the console details page for an existing cluster, add the step by choosing **Add Step** for the **Steps** field\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/flinkAddStep.png)

**Example SDK for Java**  
These examples illustrate two approaches to running a Flink job\.  
The following example submits a Flink job to a running cluster  

```
List<StepConfig> stepConfigs = new ArrayList<StepConfig>();

// The application id specified below is retrieved from the YARN cluster, for example, by running 'yarn application -list' from the master node command line 
HadoopJarStepConfig flinkWordCountConf = new HadoopJarStepConfig()
    .withJar("command-runner.jar")
    .withArgs("flink", "run", "-m", "yarn-cluster", "-yid", "application_1473169569237_0002", "-yn", "2", "/usr/lib/flink/examples/streaming/WordCount.jar", 
      "--input", "s3://bucket/for/my/textfile.txt", "--output", "s3://bucket/for/my/output/");

StepConfig flinkRunWordCount = new StepConfig()
  .withName("Flink add a wordcount step")
  .withActionOnFailure("CONTINUE")
  .withHadoopJarStep(flinkWordCountConf);
  
stepConfigs.add(flinkRunWordCount); 

// Specify the cluster ID of the YARN cluster instead of j-xxxxxxxxx
AddJobFlowStepsResult res = emr.addJobFlowSteps(new AddJobFlowStepsRequest()
   .withJobFlowId("j-xxxxxxxxxx")
   .withSteps(stepConfigs));
```
The following example creates a cluster that runs a Flink job and then terminates on completion\.  

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
Use the `add-steps` subcommand to submit new jobs to an existing Flink cluster:  

```
aws emr add-steps --cluster-id myClusterId \
--steps Type=CUSTOM_JAR,Name=Flink_Transient_No_Terminate,Jar=command-runner.jar,\
Args="flink","run","-m","yarn-cluster","-yid","application_1473169569237_0002","-yn","2",\
"/usr/lib/flink/examples/streaming/WordCount.jar",\
"--input","s3://myBucket/pg11.txt","--output","s3://myBucket/alice2/" \
--region myRegion
```
Use the `create-cluster` subcommand to create a transient EMR cluster that terminates when the Flink job completes:  

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
Args="bash","-c","\"flink run -m yarn-cluster -yn 2 /usr/lib/flink/examples/streaming/WordCount.jar
--input s3://myBucket/pg11.txt --output s3://myBucket/alice/""
```