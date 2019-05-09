# Create a Cluster With JupyterHub<a name="emr-jupyterhub-launch"></a>

You can create an Amazon EMR cluster with JupyterHub using the AWS Management Console, AWS Command Line Interface, or the Amazon EMR API\. Ensure that the cluster is not created with the option to terminate automatically after completing steps \(`--auto-terminate` option in the AWS CLI\)\. Also, make sure that administrators and notebook users can access the key pair that you use when you create the cluster\. For more information, see [Use a Key Pair for SSH Credentials](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-access-ssh.html) in the *Amazon EMR Management Guide*\.

## Create a Cluster With JupyterHub Using the Console<a name="emr-jupyterhub-launch-console"></a>

Use the following procedure to create a cluster with JupyterHub installed using **Advanced Options** in the Amazon EMR console\.

**To create an Amazon EMR cluster with JupyterHub installed using the Amazon EMR console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under **Software Configuration**:
   + For **Release**, select emr\-5\.23\.0, and choose JupyterHub\.
   + If you use Spark, to use the AWS Glue Data Catalog as the metastore for Spark SQL, select **Use for Hive table metadata**\. For more information, see [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md)\.
   + For **Edit software settings** choose **Enter configuration** and specify values, or choose **Load JSON from S3** and specify a JSON configuration file\. For more information, see [Configuring JupyterHub](emr-jupyterhub-configure.md)\.

1. Under **Add steps \(optional\)** configure steps to run when the cluster is created, make sure that **Auto\-terminate cluster after the last step is completed** is not selected, and choose **Next**\.

1. Choose **Hardware Configuration** options, **Next**\. For more information, see [Configure Cluster Hardware and Networking](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-instances.html) in the *Amazon EMR Management Guide*\.

1. Choose options for **General Cluster Settings**, **Next**\.

1. Choose **Security Options**, specifying a key pair, and choose **Create Cluster**\.

## Create a Cluster With JupyterHub Using the AWS CLI<a name="emr-jupyterhub-launch-cli"></a>

To launch a cluster with JupyterHub, use the `aws emr create-cluster` command and, for the `--applications` option, specify `Name=JupyterHub`\. The following example launches a JupyterHub cluster on Amazon EMR with two EC2 instances \(one master and one core instance\)\. Also, debugging is enabled, with logs stored in the Amazon S3 location as specified by `--log-uri`\. The specified key pair provides access to Amazon EC2 instances in the cluster\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name="MyJupyterHubCluster" --release-label emr-5.23.0 \
--applications Name=JupyterHub --log-uri s3://MyBucket/MyJupyterClusterLogs \
--use-default-roles --instance-type m4.large --instance-count 2 --ec2-attributes KeyName=MyKeyPair
```