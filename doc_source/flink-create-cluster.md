# Creating a cluster with Flink<a name="flink-create-cluster"></a>

Clusters can be launched using the AWS Management Console, AWS CLI, or an AWS SDK\.<a name="emr-flink-create-console"></a>

**To launch a cluster with Flink installed using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1.  For **Software Configuration**, choose **EMR Release emr\-5\.1\.0** or later\.

1.  Choose **Flink** as an application, along with any others to install\.

1.  Select other options as necessary and choose **Create cluster**\.

**To launch a cluster with Flink using the AWS CLI**
+ Create the cluster with the following command:

  ```
  aws emr create-cluster --release-label emr-5.34.0 \
  --applications Name=Flink \
  --configurations file://./configurations.json \
  --region us-east-1 \
  --log-uri s3://myLogUri \
  --instance-type m5.xlarge \
  --instance-count 2 \
  --service-role EMR_DefaultRole \ 
  --ec2-attributes KeyName=MyKeyName,InstanceProfile=EMR_EC2_DefaultRole \
  --steps Type=CUSTOM_JAR,Jar=command-runner.jar,Name=Flink_Long_Running_Session,\
  Args=flink-yarn-session,-d
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.