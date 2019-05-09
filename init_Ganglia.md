# Create a Cluster with Ganglia<a name="init_Ganglia"></a>

**To create a cluster with Ganglia using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**\.

1. In **Software configuration**, choose either **All Applications**, **Core Hadoop**, or **Spark**\.

1. Proceed with creating the cluster with configurations as appropriate\.

**To add Ganglia to a cluster using the AWS CLI**

In the AWS CLI, you can add Ganglia to a cluster by using `create-cluster` with the `--applications` parameter\. If you specify only Ganglia using the `--applications` parameter, Ganglia is the only application installed\.
+ Type the following command to add Ganglia when you create a cluster and replace *myKey* with the name of your EC2 key pair\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --name "Spark cluster with Ganglia" --release-label emr-5.23.0 \
  --applications Name=Spark Name=Ganglia \
  --ec2-attributes KeyName=myKey --instance-type m4.large \
  --instance-count 3 --use-default-roles
  ```

  When you specify the instance count without using the `--instance-groups` parameter, a single master node is launched, and the remaining instances are launched as core nodes\. All nodes use the instance type specified in the command\.
**Note**  
If you have not previously created the default EMR service role and EC2 instance profile, type aws `emr create-default-roles` to create them before typing the `create-cluster` subcommand\.

  For more information about using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.