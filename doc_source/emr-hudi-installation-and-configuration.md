# Creating a Cluster with Hudi Installed<a name="emr-hudi-installation-and-configuration"></a>

With Amazon EMR release version 5\.28\.0 and later, Amazon EMR installs Hudi components by default when Spark, Hive, or Presto is installed\. To use Hudi on Amazon EMR, create a cluster with the following applications installed:
+ Hadoop
+ Hive
+ Spark
+ Presto
+ Tez

You can create a cluster using the AWS Management Console, the AWS CLI, or the Amazon EMR API\.

## To create a cluster with Hudi using the AWS Management Console<a name="emr-hudi-create-cluster-console"></a>

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under Software Configuration, choose **emr\-5\.28\.0** or later for **Release** and select **Hadoop**, **Hive**, **Spark**, **Presto**, and **Tez** along with other applications that your cluster requires\.

1. Configure other options as required for your application, and then choose **Next**\.

1. Configure options for **Hardware** and **General cluster settings** as desired\.

1. For **Security Options**, we recommend that you select an **EC2 key pair** that you can use to connect to the master node command line using SSH\. This allows you to run the Spark shell commands, Hive CLI commands, and Hudi CLI commands described in this guide\.

1. Choose other security options as desired, and then choose **Create cluster**\.