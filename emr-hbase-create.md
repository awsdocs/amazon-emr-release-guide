# Creating a Cluster with HBase<a name="emr-hbase-create"></a>

The procedures in this section cover the basics of launching a cluster using the AWS Management Console and the AWS CLI\. For detailed information about how to plan, configure, and launch EMR clusters, see [Plan and Configure Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan.html) in the *Amazon EMR Management Guide*\.

## Creating a Cluster with HBase Using the Console<a name="emr-hbase-create-console"></a>

For quick steps to launch clusters with the console, see [Step 3: Launch an Amazon EMR Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/gsg-launch-cluster.html) in the *Amazon EMR Management Guide*\.

**To launch a cluster with HBase installed using the console**

**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster** and **Go to advanced options**\.

1. For **Software Configuration**, choose an **Amazon Release Version** of 4\.6\.0 or later \(we recommend the latest version\)\. Choose **HBase** and other applications as desired\.

1. With Amazon EMR version 5\.2\.0 and later, under **HBase Storage Settings**, select **HDFS** or **S3**\. For more information, see [HBase on Amazon S3 \(Amazon S3 Storage Mode\)](emr-hbase-s3.md)\.

1.  Select other options as necessary and then choose **Create cluster**\.

## Creating a Cluster with HBase Using the AWS CLI<a name="emr-hbase-cli"></a>

Use the following command to create a cluster with HBase installed:

```
aws emr create-cluster --name "Test cluster" --release-label emr-5.23.0 \
--applications Name=HBase --use-default-roles --ec2-attributes KeyName=myKey \
--instance-type m4.large --instance-count 3
```

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

If you use HBase on Amazon S3, specify the `--configurations` option with a reference to a JSON configuration object\. The configuration object must contain an `hbase-site` classification that specifies the location in Amazon S3 where HBase data is stored using the `hbase.rootdir` property\. It also must contain an `hbase` classification, which specifies `s3` using the `hbase.emr.storageMode` property\. The following example demonstrates a JSON snippet with these configuration settings\.

```
 1. {
 2.   "Classification": "hbase-site",
 3.   "Properties": {
 4.     "hbase.rootdir": "s3://MyBucket/MyHBaseStore",}
 5. },
 6. {
 7.   "Classification": "hbase",
 8.   "Properties": {
 9.   "hbase.emr.storageMode":"s3",
10.   }
11. }
```

For more information about HBase on Amazon S3, see [HBase on Amazon S3 \(Amazon S3 Storage Mode\)](emr-hbase-s3.md)\. For more information about classifications, see [Configuring Applications](emr-configure-apps.md)\.