# Using Presto with the AWS Glue Data Catalog<a name="emr-presto-glue"></a>

Using Amazon EMR release version 5\.10\.0 and later, you can specify the AWS Glue Data Catalog as the default Hive metastore for Presto\. We recommend this configuration when you require a persistent metastore or a metastore shared by different clusters, services, applications, or AWS accounts\.

AWS Glue is a fully managed extract, transform, and load \(ETL\) service that makes it simple and cost\-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores\. The AWS Glue Data Catalog provides a unified metadata repository across a variety of data sources and data formats, integrating with Amazon EMR as well as Amazon RDS, Amazon Redshift, Redshift Spectrum, Athena, and any application compatible with the Apache Hive metastore\. AWS Glue crawlers can automatically infer schema from source data in Amazon S3 and store the associated metadata in the Data Catalog\. For more information about the Data Catalog, see [Populating the AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html) in the *AWS Glue Developer Guide*\.

Separate charges apply for AWS Glue\. There is a monthly rate for storing and accessing the metadata in the Data Catalog, an hourly rate billed per minute for AWS Glue ETL jobs and crawler runtime, and an hourly rate billed per minute for each provisioned development endpoint\. The Data Catalog allows you to store up to a million objects at no charge\. If you store more than a million objects, you are charged USD$1 for each 100,000 objects over a million\. An object in the Data Catalog is a table, partition, or database\. For more information, see [Glue Pricing](https://aws.amazon.com/glue/pricing)\.

**Important**  
If you created tables using Amazon Athena or Amazon Redshift Spectrum before August 14, 2017, databases and tables are stored in an Athena\-managed catalog, which is separate from the AWS Glue Data Catalog\. To integrate Amazon EMR with these tables, you must upgrade to the AWS Glue Data Catalog\. For more information, see [Upgrading to the AWS Glue Data Catalog](https://docs.aws.amazon.com/athena/latest/ug/glue-upgrade.html) in the *Amazon Athena User Guide*\.

## Specifying AWS Glue Data Catalog as the metastore<a name="emr-presto-glue-configure"></a>

You can specify the AWS Glue Data Catalog as the metastore using the AWS Management Console, AWS CLI, or Amazon EMR API\. When you use the CLI or API, you use the configuration classification for Presto to specify the Data Catalog\. In addition, with Amazon EMR 5\.16\.0 and later, you can use the configuration classification to specify a Data Catalog in a different AWS account\. When you use the console, you can specify the Data Catalog using **Advanced Options** or **Quick Options**\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under **Software Configuration** choose a **Release** of **emr\-5\.10\-0** or later and select **Presto**\.

1. Select **Use for Presto table metadata**, choose **Next**, and then complete other settings for your cluster as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the configuration classification**

For examples of how to specify the following configuration classifications when you create a cluster, see [Configure applications](emr-configure-apps.md)\.

**Amazon EMR 5\.16\.0 and later**
+ Set the `hive.metastore` property to `glue` as shown in the following JSON example\.

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

  To specify a Data Catalog in a different AWS account, add the `hive.metastore.glue.catalogid` property as shown in the following JSON example\. Replace `acct-id` with the AWS account of the Data Catalog\. Using a Data Catalog in another AWS account is not available using Amazon EMR version 5\.15\.0 and earlier\.

  ```
  [
    {
      "Classification": "presto-connector-hive",
      "Properties": {
        "hive.metastore": "glue",
        "hive.metastore.glue.catalogid": "acct-id"
      }
    }
  ]
  ```

  **Amazon EMR 5\.10\.0 through 5\.15\.0**

  Set the `hive.metastore.glue.datacatalog.enabled` property to `true`, as shown in the following JSON example:

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

  **Amazon EMR 6\.1\.0 and later using PrestoSQL**

  Starting with EMR version 6\.1\.0, PrestoSQL also supports Glue as the default Hive metastore\. Use the `prestosql-connector-hive` configuration classification and set the `hive.metastore` property to `glue`, as shown in the following JSON example\.

  ```
  [
    {
      "Classification": "prestosql-connector-hive",
      "Properties": {
        "hive.metastore": "glue"
      }
    }
  ]
  ```

To switch metastores on a long\-running cluster, you can manually set these values as appropriate for your release version by connecting to the master node, editing the property values in the `/etc/presto/conf/catalog/hive.properties` file directly, and restarting the Presto server \(`sudo restart presto-server`\)\. If you use this method with Amazon EMR 5\.15\.0 and earlier, make sure that `hive.table-statistics-enabled` is set to `false`\. This setting is not required when using release versions 5\.16\.0 and later; nevertheless, table and partition statistics are not supported\.

## IAM permissions<a name="emr-hive-glue-permissions"></a>

The EC2 instance profile for a cluster must have IAM permissions for AWS Glue actions\. In addition, if you enable encryption for AWS Glue Data Catalog objects, the role must also be allowed to encrypt, decrypt and generate the AWS KMS key used for encryption\.

### Permissions for AWS Glue actions<a name="emr-hive-glue-permissions-actions"></a>

If you use the default EC2 instance profile for Amazon EMR, no action is required\. The `AmazonElasticMapReduceforEC2Role` managed policy that is attached to the `EMR_EC2_DefaultRole` allows all necessary AWS Glue actions\. However, if you specify a custom EC2 instance profile and permissions, you must configure the appropriate AWS Glue actions\. Use the `AmazonElasticMapReduceforEC2Role` managed policy as a starting point\. For more information, see [Service role for cluster EC2 instances \(EC2 instance profile\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-role-for-ec2.html) in the *Amazon EMR Management Guide*\.

### Permissions for encrypting and decrypting AWS Glue Data Catalog<a name="emr-hive-glue-permissions-encrypt"></a>

Your instance profile needs permission to encrypt and decrypt data using your key\. You do *not* need to configure these permissions if both of the following statements apply:
+ You enable encryption for AWS Glue Data Catalog objects using managed keys for AWS Glue\.
+ You use a cluster that's in the same AWS account as the AWS Glue Data Catalog\.

Otherwise, you must add the following statement to the permissions policy attached to your EC2 instance profile\. 

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

For more information about AWS Glue Data Catalog encryption, see [Encrypting your data catalog](https://docs.aws.amazon.com/glue/latest/dg/encrypt-glue-data-catalog.html) in the *AWS Glue Developer Guide*\.

### Resource\-based permissions<a name="emr-hive-glue-permissions-resource"></a>

If you use AWS Glue in conjunction with Hive, Spark, or Presto in Amazon EMR, AWS Glue supports resource\-based policies to control access to Data Catalog resources\. These resources include databases, tables, connections, and user\-defined functions\. For more information, see [AWS Glue Resource Policies](https://docs.aws.amazon.com/glue/latest/dg/glue-resource-policies.html) in the *AWS Glue Developer Guide*\.

When using resource\-based policies to limit access to AWS Glue from within Amazon EMR, the principal that you specify in the permissions policy must be the role ARN associated with the EC2 instance profile that is specified when a cluster is created\. For example, for a resource\-based policy attached to a catalog, you can specify the role ARN for the default service role for cluster EC2 instances, *EMR\_EC2\_DefaultRole* as the `Principal`, using the format shown in the following example:

```
arn:aws:iam::acct-id:role/EMR_EC2_DefaultRole
```

The *acct\-id* can be different from the AWS Glue account ID\. This enables access from EMR clusters in different accounts\. You can specify multiple principals, each from a different account\.

## Considerations when using AWS Glue Data Catalog<a name="emr-presto-glue-knownissues"></a>

Consider the following items when using AWS Glue Data Catalog as a metastore with Presto:
+ Renaming tables from within AWS Glue is not supported\.
+ When you create a Hive table without specifying a `LOCATION`, the table data is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table data is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](https://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 
+ Partition values containing quotes and apostrophes are not supported, for example, `PARTITION (owner="Doe's").`
+ [Column statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ColumnStatistics) are supported for emr\-5\.31\.0 and later\.
+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\. As an alternative, consider using [AWS Glue Resource\-Based Policies](https://docs.aws.amazon.com/glue/latest/dg/glue-resource-policies.html)\. For more information, see [Use Resource\-Based Policies for Amazon EMR Access to AWS Glue Data Catalog](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-roles-glue.html)\.