# Submit Pig Work<a name="emr-pig-launch"></a>

This section demonstrates submitting Pig work to an Amazon EMR cluster\. The examples that follow generate a report containing the total bytes transferred, a list of the top 50 IP addresses, a list of the top 50 external referrers, and the top 50 search terms using Bing and Google\. The Pig script is located in the Amazon S3 bucket `s3://elasticmapreduce/samples/pig-apache/do-reports2.pig`\. Input data is located in the Amazon S3 bucket `s3://elasticmapreduce/samples/pig-apache/input`\. The output is saved to an Amazon S3 bucket\. 

**Important**  
For EMR 4\.x or greater, you must copy and modify the Pig script do\-reports\.pig to make it work\. In your modified script, replace the following line  

```
register file:/home/hadoop/lib/pig/piggybank.jar 
```
with this:  

```
register file:/usr/lib/pig/lib/piggybank.jar 
```
Then replace this script in your own bucket in Amazon S3\.

## Submit Pig Work Using the Amazon EMR Console<a name="ConsoleCreatingaPigJob"></a>

This example describes how to use the Amazon EMR console to add a Pig step to a cluster\. 

**To submit a Pig step**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the **Cluster List**, select the name of your cluster\.

1. Scroll to the **Steps** section and expand it, then choose **Add step**\.

1. In the **Add Step** dialog:
   + For **Step type**, choose **Pig program**\.
   + For **Name**, accept the default name \(Pig program\) or type a new name\.
   + For **Script S3 location**, type the location of the Pig script\. For example: **s3://elasticmapreduce/samples/pig\-apache/do\-reports2\.pig**\.
   + For **Input S3 location**, type the location of the input data\. For example: **s3://elasticmapreduce/samples/pig\-apache/input**\.
   + For **Output S3 location**, type or browse to the name of your Amazon S3 output bucket\.
   + For **Arguments**, leave the field blank\.
   + For **Action on failure**, accept the default option \(**Continue**\)\.

1. Choose **Add**\. The step appears in the console with a status of Pending\. 

1. The status of the step changes from Pending to Running to Completed as the step runs\. To update the status, choose the **Refresh** icon above the **Actions** column\. 

## Submit Pig Work Using the AWS CLI<a name="emr-pig-submit-work"></a>

**To submit a Pig step using the AWS CLI**

When you launch a cluster using the AWS CLI, use the `--applications` parameter to install Pig\. To submit a Pig step, use the `--steps` parameter\. 
+ To launch a cluster with Pig installed and to submit a Pig step, type the following command, replace *myKey* with the name of your EC2 key pair, and replace *mybucket* with the name of your Amazon S3 bucket\.
  + 

    ```
    aws emr create-cluster --name "Test cluster" --release-label emr-5.23.0 --applications Name=Pig \
    --use-default-roles --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 \
    --steps Type=PIG,Name="Pig Program",ActionOnFailure=CONTINUE,Args=[-f,s3://elasticmapreduce/samples/pig-apache/do-reports2.pig,-p,INPUT=s3://elasticmapreduce/samples/pig-apache/input,-p,OUTPUT=s3://mybucket/pig-apache/output]
    ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  When you specify the instance count without using the `--instance-groups` parameter, a single master node is launched, and the remaining instances are launched as core nodes\. All nodes use the instance type specified in the command\.
**Note**  
If you have not previously created the default EMR service role and EC2 instance profile, type aws `emr create-default-roles` to create them before typing the `create-cluster` subcommand\.

  For more information about using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.