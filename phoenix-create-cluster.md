# Creating a Cluster with Phoenix<a name="phoenix-create-cluster"></a>

You install Phoenix by choosing the application when you create a cluster in the console or using the AWS CLI\. The following procedures and examples show how to create a cluster with Phoenix and HBase\. For more information about creating clusters using the console, including **Advanced Options** see [Plan and Configure Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan.html) in the *Amazon EMR Management Guide*\.

**To launch a cluster with Phoenix installed using **Quick Options** for creating a cluster in the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster** to use **Quick Create**\.

1. For **Software Configuration**, choose the most recent release appropriate for your application\. Phoenix appears as an option only when **Amazon Release Version emr\-4\.7\.0** or later is selected\.

1. For **Applications**, choose the second option, ** HBase: HBase *ver* with Ganglia *ver*, Hadoop *ver*, Hive *ver*, Hue *ver*, Phoenix *ver*, and ZooKeeper *ver***\.

1.  Select other options as necessary and then choose **Create cluster**\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

The following example launches a cluster with Phoenix installed using default configuration settings\.

**To launch a cluster with Phoenix and HBase using the AWS CLI**
+ Create the cluster with the following command:

  ```
  aws emr create-cluster --name "Cluster with Phoenix" --release-label emr-5.23.0 \
  --applications Name=Phoenix Name=HBase --ec2-attributes KeyName=myKey \
  --instance-type m4.large --instance-count 3 --use-default-roles
  ```

## Customizing Phoenix Configurations<a name="phoenix-custom-config"></a>

When creating a cluster, you configure Phoenix by setting values in `hbase-site.xml` using the `hbase-site` configuration classification\.

For more information, see [Configuration and Tuning](https://phoenix.apache.org/tuning.html) in the Phoenix documentation\.

The following example demonstrates using a JSON file stored in Amazon S3 to specify the value of `false` for the `phoenix.schema.dropMetaData` property\. Multiple properties can be specified for a single classification\. For more information, see [Configuring Applications](emr-configure-apps.md)\. The `create-cluster` command then references the JSON file as the `--configurations` parameter\.

The contents of the JSON file saved to /mybucket/myfolder/myconfig\.json is the following\.

```
[
    {
      "Classification": "hbase-site",
      "Properties": {
        "phoenix.schema.dropMetaData": "false"
      }
    }
  ]
```

The `create cluster` command that references the JSON file is shown in the following example\.

```
aws emr create-cluster --release-label emr-5.23.0 --applications Name=Phoenix \
Name=HBase --instance-type m4.large --instance-count 2 \
--configurations https://s3.amazonaws.com/mybucket/myfolder/myconfig.json
```

**Note**  
Reconfiguration request for any Phoenix configuration classifications is only supported in Amazon EMR version 5\.23\.0 and later, and is not supported in Amazon EMR version 5\.21\.0 or 5\.22\.0\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)