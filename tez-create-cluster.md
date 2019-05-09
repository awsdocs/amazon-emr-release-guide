# Creating a Cluster with Tez<a name="tez-create-cluster"></a>

Install Tez by choosing that application when you create the cluster\.<a name="emr-tez-create"></a>

**To create a cluster with Tez installed using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under **Software Configuration**, select a **Release** of **emr\-4\.7\.0** or later\.

1. Select **Tez** along with other applications you want Amazon EMR to install\.

1.  Select other options as necessary and then choose **Create cluster**\.

**To create a cluster with Tez using the AWS CLI**
+ Use the `create-cluster` command along with the `-- applications` option to specify **Tez**\. The following example creates a cluster with Tez installed\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --name "Cluster with Tez" --release-label emr-5.23.0 \
  --applications Name=Tez --ec2-attributes KeyName=myKey \
  --instance-type m4.large --instance-count 3 --use-default-roles
  ```