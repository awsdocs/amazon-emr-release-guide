# Submit a Custom JAR Step<a name="emr-launch-custom-jar-cli"></a>

This section covers the basics of submitting a custom JAR step in Amazon EMR\. Submitting a custom JAR step enables you to write a script to process your data using the Java programming language\. 

## Submit a Custom JAR Step Using the Console<a name="ConsoleCreatingaCustomJARJob"></a>

This example describes how to use the Amazon EMR console to submit a custom JAR step to a running cluster\.

**To submit a custom JAR step using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the **Cluster List**, select the name of your cluster\.

1. Scroll to the **Steps** section and expand it, then choose **Add step**\.

1. In the **Add Step** dialog:
   + For **Step type**, choose **Custom JAR**\.
   + For **Name**, accept the default name \(Custom JAR\) or type a new name\.
   + For **JAR S3 location**, type or browse to the location of your JAR file\. The value must be in the form `s3://BucketName/path/JARfile`\. 
   + For **Arguments**, type any required arguments as space\-separated strings or leave the field blank\.
   + For **Action on failure**, accept the default option \(**Continue**\)\.

1. Choose **Add**\. The step appears in the console with a status of Pending\. 

1. The status of the step changes from Pending to Running to Completed as the step runs\. To update the status, choose the **Refresh** icon above the Actions column\. 

## Launching a cluster and submitting a custom JAR step using the AWS CLI<a name="emr-dev-create-jar-cli"></a>

**To launch a cluster and submit a custom JAR step using the AWS CLI**

To launch a cluster and submit a custom JAR step using the AWS CLI, type the `create-cluster` subcommand with the `--steps` parameter\.
+ To launch a cluster and submit a custom JAR step, type the following command, replace *myKey* with the name of your EC2 key pair, and replace *mybucket* with your bucket name\.

  ```
  aws emr create-cluster --name "Test cluster" --release-label emr-5.23.0 \
  --applications Name=Hue Name=Hive Name=Pig --use-default-roles \
  --ec2-attributes KeyName=myKey --instance-type m4.large --instance-count 3 \
  --steps Type=CUSTOM_JAR,Name="Custom JAR Step",ActionOnFailure=CONTINUE,Jar=pathtojarfile,Args=["pathtoinputdata","pathtooutputbucket","arg1","arg2"]
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  When you specify the instance count without using the `--instance-groups` parameter, a single master node is launched, and the remaining instances are launched as core nodes\. All nodes use the instance type specified in the command\.
**Note**  
If you have not previously created the default Amazon EMR service role and EC2 instance profile, type `aws emr create-default-roles` to create them before typing the `create-cluster` subcommand\.

  For more information on using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.

## Third\-party dependencies<a name="emr-custom-jar-dependency"></a>

Sometimes it may be necessary to include in the MapReduce classpath JARs for use with your program\. You have two options for doing this:
+ Include the `--libjars s3://URI_to_JAR` in the step options for the procedure in [Launching a cluster and submitting a custom JAR step using the AWS CLI](#emr-dev-create-jar-cli)\.
+ Launch the cluster with a modified `mapreduce.application.classpath` setting in `mapred-site.xml` using the `mapred-site` configuration classification\. To create the cluster with the step using AWS CLI, this would look like the following:

  ```
  aws emr create-cluster --release-label emr-5.23.0 \
  --applications Name=Hue Name=Hive Name=Pig --use-default-roles \
  --instance-type m4.large --instance-count 2  --ec2-attributes KeyName=myKey \
  --steps Type=CUSTOM_JAR,Name="Custom JAR Step",ActionOnFailure=CONTINUE,Jar=pathtojarfile,Args=["pathtoinputdata","pathtooutputbucket","arg1","arg2"] \
  --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```

  `myConfig.json`:

  ```
  [
      {
        "Classification": "mapred-site",
        "Properties": {
          "mapreduce.application.classpath": "path1,path2"
        }
      }
    ]
  ```

  The comma\-separated list of paths should be appended to the classpath for each task's JVM\.