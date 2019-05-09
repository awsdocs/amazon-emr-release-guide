# Submit a Streaming Step<a name="CLI_CreateStreaming"></a>

This section covers the basics of submitting a Streaming step to a cluster\. A Streaming application reads input from standard input and then runs a script or executable \(called a mapper\) against each input\. The result from each of the inputs is saved locally, typically on a Hadoop Distributed File System \(HDFS\) partition\. After all the input is processed by the mapper, a second script or executable \(called a reducer\) processes the mapper results\. The results from the reducer are sent to standard output\. You can chain together a series of Streaming steps, where the output of one step becomes the input of another step\. 

The mapper and the reducer can each be referenced as a file or you can supply a Java class\. You can implement the mapper and reducer in any of the supported languages, including Ruby, Perl, Python, PHP, or Bash\.

## Submit a Streaming Step Using the Console<a name="emr-dev-create-stream-console"></a>

This example describes how to use the Amazon EMR console to submit a Streaming step to a running cluster\.

**To submit a Streaming step**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the **Cluster List**, select the name of your cluster\.

1. Scroll to the **Steps** section and expand it, then choose **Add step**\.

1. In the **Add Step** dialog box:
   + For **Step type**, choose **Streaming program**\.
   + For **Name**, accept the default name \(Streaming program\) or type a new name\.
   + For **Mapper**, type or browse to the location of your mapper class in Hadoop, or an S3 bucket where the mapper executable, such as a Python program, resides\. The path value must be in the form *BucketName*/*path*/*MapperExecutable*\.
   + For **Reducer**, type or browse to the location of your reducer class in Hadoop, or an S3 bucket where the reducer executable, such as a Python program, resides\. The path value must be in the form *BucketName*/*path*/*MapperExecutable*\. Amazon EMR supports the special *aggregate* keyword\. For more information, go to the Aggregate library supplied by Hadoop\.
   + For **Input S3 location**, type or browse to the location of your input data\. 
   + For **Output S3 location**, type or browse to the name of your Amazon S3 output bucket\.
   + For **Arguments**, leave the field blank\.
   + For **Action on failure**, accept the default option \(**Continue**\)\.

1. Choose **Add**\. The step appears in the console with a status of Pending\. 

1. The status of the step changes from Pending to Running to Completed as the step runs\. To update the status, choose the **Refresh** icon above the Actions column\. 

## AWS CLI<a name="emr-dev-create-stream-cli"></a>

These examples demonstrate how to use the AWS CLI to create a cluster and submit a Streaming step\. 

**To create a cluster and submit a Streaming step using the AWS CLI**
+ To create a cluster and submit a Streaming step using the AWS CLI, type the following command and replace *myKey* with the name of your EC2 key pair\.

  ```
  aws emr create-cluster --name "Test cluster" --release-label emr-5.23.0 --applications Name=Hue Name=Hive Name=Pig --use-default-roles \
  --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 \
  --steps Type=STREAMING,Name="Streaming Program",ActionOnFailure=CONTINUE,Args=[--files,pathtoscripts,-mapper,mapperscript,-reducer,reducerscript,aggregate,-input,pathtoinputdata,-output,pathtooutputbucket]
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  When you specify the instance count without using the `--instance-groups` parameter, a single master node is launched, and the remaining instances are launched as core nodes\. All nodes use the instance type specified in the command\.
**Note**  
If you have not previously created the default Amazon EMR service role and EC2 instance profile, type aws `emr create-default-roles` to create them before typing the `create-cluster` subcommand\.

  For more information on using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.