# Command Runner<a name="emr-commandrunner"></a>

Many scripts or programs are placed on the shell login path environment so you do not need to specify the full path when executing them when using `command-runner.jar`\. You also do not have to know the full path to `command-runner.jar`\. `command-runner.jar` is located on the AMI so there is no need to know a full URI as was the case with `script-runner.jar`\. 

The following is a list of scripts that can be executed with `command-runner.jar`:

hadoop\-streaming  
Submit a Hadoop streaming program\. In the console and some SDKs, this is a streaming step\.

hive\-script  
Run a Hive script\. In the console and SDKs, this is a Hive step\.

pig\-script  
Run a Pig script\. In the console and SDKs, this is a Pig step\.

spark\-submit  
Run a Spark application\. In the console, this is a Spark step\.

s3\-dist\-cp  
Distributed copy large amounts of data from Amazon S3 into HDFS\.

hadoop\-lzo  
Run the Hadoop LZO indexer on a directory\.

The following is an example usage of `command-runner.jar` using the AWS CLI:

```
aws emr add-steps --cluster-id j-2AXXXXXXGAPLF --steps Name="Command Runner",Jar="command-runner.jar",Args=["spark-submit","Args..."]
```