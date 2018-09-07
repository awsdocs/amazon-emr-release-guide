# Using Presto with the AWS Glue Data Catalog<a name="emr-presto-glue"></a>

Using Amazon EMR release version 5\.10\.0 and later, you can specify the AWS Glue Data Catalog as the default Hive metastore for Presto\. You can specify this option when you create a cluster using the AWS Management Console, or using the `presto-connector-hive` configuration classification when using the AWS CLI or Amazon EMR API\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under **Software Configuration** choose a **Release** of **emr\-5\.10\-0** or later and select **Presto**\.

1. Select **Use for Presto table metadata**, choose **Next**, and then complete other settings for your cluster as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the CLI or API**

1. **Amazon EMR 5\.16\.0 and later**

   Set the `hive.metastore` property to `glue` as shown in the following JSON example

1. 

   ```
   [
     {
       "Classification": "presto-connector-hive",
       "Properties": {
         "hive.metastore": "glue"
       }
     }
   ]
   ```

   **Amazon EMR 5\.10\.0 through 5\.15\.0**

   Set the `hive.metastore.glue.datacatalog.enabled` property to `true`, as shown in the following JSON example\.

   ```
   [
     {
       "Classification": "presto-connector-hive",
       "Properties": {
         "hive.metastore.glue.datacatalog.enabled": "true"
       }
     }
   ]
   ```

To switch metastores on a long\-running cluster, you can manually set these values as appropriate for your release version by connecting to the master node, editing the property values in the `/etc/presto/conf/catalog/hive.properties` file directly, and restarting the Presto server \(`sudo restart presto-server`\)\. If you use this method on a version earlier than 5\.16\.0, make sure that `hive.table-statistics-enabled` is set to `false`\. This setting is not required when using release versions 5\.16\.0 and later; nevertheless, table and partition statistics are not supported\.

## Considerations When Using AWS Glue Data Catalog<a name="emr-presto-glue-knownissues"></a>

Consider the following items when using AWS Glue Data Catalog as a metastore with Presto:
+ Renaming tables from within AWS Glue is not supported\.
+ When you create a Hive table without specifying a `LOCATION`, the table definition is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table definition is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](http://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 
+ Partition values containing quotes and apostrophes are not supported \(for example, `PARTITION (owner="Doe's").`
+ [Column statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ColumnStatistics) are not supported\.
+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\.

## IAM Permissions<a name="emr-hive-glue-permissions"></a>

The EC2 instance profile for a cluster must have IAM permissions for AWS Glue actions\. In addition, if you enable encryption for AWS Glue Data Catalog objects, the role must also be allowed to encrypt, decrypt and generate the customer master key \(CMK\) used for encryption\.

### Permissions for AWS Glue Actions<a name="w3aac44c15c13b5"></a>

The default `AmazonElasticMapReduceforEC2Role` managed policy attached to `EMR_EC2_DefaultRole` allows the required AWS Glue actions\. If you use the default EC2 instance profile, no action is required\. However, if you specify a custom EC2 instance profile and permissions when you create a cluster, ensure that the appropriate AWS Glue actions are allowed\. Use the `AmazonElasticMapReduceforEC2Role` managed policy as a starting point\. For a listing of AWS Glue actions, see [Default Contents of AmazonElasticMapReduceforEC2Role Permissions Policy](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-roles-defaultroles.html#emr-iam-contents-ec2role) in the *Amazon EMR Management Guide*\.

### Permissions for Encrypting and Decrypting AWS Glue Data Catalog<a name="w3aac44c15c13b7"></a>

This section is about the encryption feature of the AWS Glue Data Catalog\. For more information about AWS Glue Data Catalog encryption, see [Encrypting Your Data Catalog](http://docs.aws.amazon.com/glue/latest/dg/encrypt-glue-data-catalog.html) in the *AWS Glue Developer Guide*\.

If you enable encryption for AWS Glue Data Catalog objects using AWS managed CMKs for AWS Glue, and the cluster that accesses the AWS Glue Data Catalog is within the same AWS account, you don't need to update the permissions policy attached to the EC2 instance profile\. If you use a customer managed CMK, or if the cluster is in a different AWS account, you must update the permissions policy so that the EC2 instance profile has permission to encrypt and decrypt using the key\. The contents of the following policy statement needs to be added regardless of whether you use the default permissions policy, `AmazonElasticMapReduceforEC2Role`, or you use a custom permissions policy attached to a custom EC2 instance profile\. 

```
[
    {
        "Version": "2012-10-17",
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "kms:Decrypt",
                    "kms:Encrypt",
                    "kms:GenerateDataKey"
                ],
                "Resource": "arn:aws:kms:region:acct-id:key/12345678-1234-1234-1234-123456789012"
            }
        ]
    }
]
```