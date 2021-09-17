# Run commands and scripts on an Amazon EMR cluster<a name="emr-commandrunner"></a>

This topic covers how to run a command or a script as a step on your cluster\. Running a command or script as a step is one of the many ways you can [Submit work to a cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/AddingStepstoaJobFlow.html) and is useful in the following situations:
+ When you don't have SSH access to your Amazon EMR cluster
+ When you want to run a bash or shell command to troubleshoot your cluster

You can run a script either when you create a cluster or when you cluster is in the `WAITING` state\. To run a script before step processing begins, you use a bootstrap action instead\. For more information about bootstrap actions, see [Create bootstrap actions to install additional software](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-bootstrap.html) in the *Amazon EMR Management Guide*\.

Amazon EMR provides the following tools to help you run scripts, commands, and other on\-cluster programs\. You can invoke both tools using the Amazon EMR management console or the AWS CLI\.

`command-runner.jar`  
Located on the Amazon EMR AMI for your cluster\. You can use `command-runner.jar` to run commands on your cluster\. You specify `command-runner.jar` without using its full path\. 

`script-runner.jar`  
Hosted on Amazon S3 at `s3://<region>.elasticmapreduce/libs/script-runner/script-runner.jar` where `<region>` is the Region in which your Amazon EMR cluster resides\. You can use `script-runner.jar` to run scripts saved locally or on Amazon S3 on your cluster\. You must specify the full URI of `script-runner.jar` when you submit a step\.

## Submit a custom JAR step to run a script or command<a name="emr-commandrunner-examples"></a>

The following AWS CLI examples illustrate some common use cases of `command-runner.jar` and `script-runner.jar` on Amazon EMR\.

**Example : Running a command on a cluster using `command-runner.jar`**  
When you use `command-runner.jar`, you specify commands, options, and values in your step's list of arguments\.  
The following AWS CLI example submits a step to a running cluster that invokes `command-runner.jar`\. The specified command in the `Args` list downloads a script called *my\-script\.sh* from Amazon S3 into the hadoop user home directory\. The command then modifies the script's permissions and runs *my\-script\.sh*\.  
When you use the AWS CLI, the items in your `Args` list should be comma separated with no whitespace between list elements\. For example, `Args=[example-command,example-option,"example option value"]` instead of `Args=[example-command, example-option, "example option value"]`\.  

```
aws emr add-steps \
--cluster-id j-2AXXXXXXGAPLF \
--steps Type=CUSTOM_JAR,Name="Download a script from S3, change its permissions, and run it",ActionOnFailure=CONTINUE,Jar=command-runner.jar,Args=[bash,-c,"aws s3 cp s3://EXAMPLE-DOC-BUCKET/my-script.sh /home/hadoop; chmod u+x /home/hadoop/my-script.sh; cd /home/hadoop; ./my-script.sh"]
```

**Example : Running a script on a cluster using `script-runner.jar`**  
When you use `script-runner.jar`, you specify the script that you want to run in your step's list of arguments\.  
The following AWS CLI example submits a step to a running cluster that invokes `script-runner.jar`\. In this case, the script called *my\-script\.sh* is stored on Amazon S3\. You can also specify local scripts that are stored on the master node of your cluster\.  

```
aws emr add-steps \
--cluster-id j-2AXXXXXXGAPLF \
--steps Type=CUSTOM_JAR,Name="Run a script from S3 with script-runner.jar",ActionOnFailure=CONTINUE,Jar=s3://us-west-2.elasticmapreduce/libs/script-runner/script-runner.jar,Args=[s3://EXAMPLE-DOC-BUCKET/my-script.sh]
```

## Other ways to use `command-runner.jar`<a name="emr-commandrunner-other-uses"></a>

You can also use `command-runner.jar` to submit work to a cluster with tools such as `spark-submit` or `hadoop-streaming`\. When you launch an application using `command-runner.jar`, you specify `CUSTOM_JAR` as the step type instead of using a value like `SPARK`, `STREAMING`, or `PIG`\. Tool availability varies depending on which applications you've installed on the cluster\.

The following example command uses `command-runner.jar` to submit a step using `spark-submit`\. The `Args` list specifies `spark-submit` as the command, followed by the Amazon S3 URI of the Spark application *my\-app\.py* with arguments and values\.

```
aws emr add-steps \
--cluster-id j-2AXXXXXXGAPLF \
--steps Type=CUSTOM_JAR,Name="Run spark-submit using command-runner.jar",ActionOnFailure=CONTINUE,Jar=command-runner.jar,Args=[spark-submit,S3://DOC-EXAMPLE-BUCKET/my-app.py,ArgName1,ArgValue1,ArgName2,ArgValue2]
```

The following table identifies additional tools that you can run using `command-runner.jar`\.


****  

| Tool name | Description | 
| --- | --- | 
| hadoop\-streaming | Submits an Hadoop streaming program\. In the console and some SDKs, this is a streaming step\. | 
| hive\-script | Runs a Hive script\. In the console and SDKs, this is a Hive step\. | 
| pig\-script | Runs a Pig script\. In the console and SDKs, this is a Pig step\. | 
| spark\-submit |  Runs a Spark application\. In the console, this is a Spark step\.  | 
| hadoop\-lzo | Runs the [Hadoop LZO indexer](https://github.com/kevinweil/hadoop-lzo/blob/master/README.md) on a directory\. | 
| s3\-dist\-cp | Distributed copy large amounts of data from Amazon S3 into HDFS\. For more information, see [S3DistCp \(s3\-dist\-cp\)](UsingEMR_s3distcp.md)\. | 