# Creating a Cluster with HCatalog<a name="emr-hcatalog-create-cluster"></a>

Although HCatalog is included in the Hive project, you must install it as its own application\.

**To launch a cluster with HCatalog installed using the console**

The following procedure creates a cluster with HCatalog installed\. For more information about creating clusters using the console, including **Advanced Options** see [Plan and Configure Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan.html) in the *Amazon EMR Management Guide*\.

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster** to use **Quick Create**\.

1.  For the **Software Configuration** field, choose **Amazon Release Version emr\-4\.4\.0** or later\.

1.  In the **Select Applications** field, choose either **All Applications** or **HCatalog**\.

1.  Select other options as necessary and then choose **Create cluster**\.

**To launch a cluster with HCatalog using the AWS CLI**
+ Create the cluster with the following command:
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --name "Cluster with Hcat" --release-label emr-5.23.0 \
  --applications Name=HCatalog --ec2-attributes KeyName=myKey \
  --instance-type m4.large --instance-count 3 --use-default-roles
  ```