# Run a Script in a Cluster<a name="emr-hadoop-script"></a>

Amazon EMR enables you to run a script at any time during step processing in your cluster\. You specify a step that runs a script either when you create your cluster or you can add a step if your cluster is in the `WAITING` state\. For more information about adding steps, see [Submit Work to a Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/AddingStepstoaJobFlow.html) in the *Amazon EMR Management Guide*\.

To run a script before step processing begins, use a bootstrap action\. For more information about bootstrap actions, see [Create Bootstrap Actions to Install Additional Software](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html) in the *Amazon EMR Management Guide*\.

## Submitting a Custom JAR Step Using the AWS CLI<a name="emr-dev-cli-add-step-script"></a>

**Note**  
You can now use command\-runner\.jar in many cases instead of script\-runner\.jar\. command\-runner\.jar does not need to have a full path for the JAR\. For more information, see [Command Runner](emr-commandrunner.md)\.

This section describes how to add a step to run a script\. The `script-runner.jar` takes arguments to the path to a script and any additional arguments for the script\. The JAR file runs the script with the passed arguments\. 

**Important**  
`script-runner.jar` is located at `s3://region.elasticmapreduce/libs/script-runner/script-runner.jar` where *region* is the region in which your EMR cluster resides\.

The cluster containing a step that runs a script looks similar to the following examples\.

**To add a step to run a script using the AWS CLI**
+ To run a script using the AWS CLI, type the following command, replace *myKey* with the name of your EC2 key pair and replace *mybucket* with your S3 bucket\. This cluster runs the script `my_script.sh` on the master node when the step is processed\.

  ```
  aws emr create-cluster --name "Test cluster" –-release-label emr-5.23.0 --applications Name=Hive Name=Pig --use-default-roles --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 --steps Type=CUSTOM_JAR,Name=CustomJAR,ActionOnFailure=CONTINUE,Jar=s3://region.elasticmapreduce/libs/script-runner/script-runner.jar,Args=["s3://mybucket/script-path/my_script.sh"]
  ```

  When you specify the instance count without using the `--instance-groups` parameter, a single master node is launched, and the remaining instances are launched as core nodes\. All nodes use the instance type specified in the command\.
**Note**  
If you have not previously created the default Amazon EMR service role and EC2 instance profile, type aws `emr create-default-roles` to create them before typing the `create-cluster` subcommand\.

  For more information on using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.