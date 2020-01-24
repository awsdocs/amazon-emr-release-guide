# Using the AWS Glue Data Catalog as the Metastore for Spark SQL<a name="emr-spark-glue"></a>

Using Amazon EMR version 5\.8\.0 or later, you can configure Spark SQL to use the AWS Glue Data Catalog as its metastore\. We recommend this configuration when you require a persistent metastore or a metastore shared by different clusters, services, applications, or AWS accounts\.

AWS Glue is a fully managed extract, transform, and load \(ETL\) service that makes it simple and cost\-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores\. The AWS Glue Data Catalog provides a unified metadata repository across a variety of data sources and data formats, integrating with Amazon EMR as well as Amazon RDS, Amazon Redshift, Redshift Spectrum, Athena, and any application compatible with the Apache Hive metastore\. AWS Glue crawlers can automatically infer schema from source data in Amazon S3 and store the associated metadata in the Data Catalog\. For more information about the Data Catalog, see [Populating the AWS Glue Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html) in the *AWS Glue Developer Guide*\.

Separate charges apply for AWS Glue\. There is a monthly rate for storing and accessing the metadata in the Data Catalog, an hourly rate billed per minute for AWS Glue ETL jobs and crawler runtime, and an hourly rate billed per minute for each provisioned development endpoint\. The Data Catalog allows you to store up to a million objects at no charge\. If you store more than a million objects, you are charged USD$1 for each 100,000 objects over a million\. An object in the Data Catalog is a table, partition, or database\. For more information, see [Glue Pricing](https://aws.amazon.com//glue/pricing)\.

**Important**  
If you created tables using Amazon Athena or Amazon Redshift Spectrum before August 14, 2017, databases and tables are stored in an Athena\-managed catalog, which is separate from the AWS Glue Data Catalog\. To integrate Amazon EMR with these tables, you must upgrade to the AWS Glue Data Catalog\. For more information, see [Upgrading to the AWS Glue Data Catalog](https://docs.aws.amazon.com/athena/latest/ug/glue-upgrade.html) in the *Amazon Athena User Guide*\.

## Specifying AWS Glue Data Catalog as the Metastore<a name="emr-spark-glue-configure"></a>

You can specify the AWS Glue Data Catalog as the metastore using the AWS Management Console, AWS CLI, or Amazon EMR API\. When you use the CLI or API, you use the configuration classification for Spark to specify the Data Catalog\. In addition, with Amazon EMR 5\.16\.0 and later, you can use the configuration classification to specify a Data Catalog in a different AWS account\. When you use the console, you can specify the Data Catalog using **Advanced Options** or **Quick Options**\.

**Note**  
The option to use AWS Glue Data Catalog is also available with Zeppelin because Zeppelin is installed with Spark SQL components\.

**To specify the AWS Glue Data Catalog as the metastore for Spark SQL using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. For **Release**, choose **emr\-5\.8\.0** or later\.

1. Under **Release**, select **Spark** or **Zeppelin**\.

1. Under **AWS Glue Data Catalog settings**, select **Use for Spark table metadata**\.

1. Choose other options for your cluster as appropriate, choose **Next**, and then configure other cluster options as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the metastore using the configuration classification**

For more information about specifying a configuration classification using the AWS CLI and EMR API, see [Configuring Applications](emr-configure-apps.md)\.
+ Specify the value for `hive.metastore.client.factory.class` using the `spark-hive-site` classification as shown in the following example:

  ```
  [
    {
      "Classification": "spark-hive-site",
      "Properties": {
        "hive.metastore.client.factory.class": "com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory"
      }
    },
  ]
  ```

  To specify a Data Catalog in a different AWS account, add the `hive.metastore.glue.catalogid` property as shown in the following example\. Replace `acct-id` with the AWS account of the Data Catalog\.

  ```
  [
    {
      "Classification": "spark-hive-site",
      "Properties": {
        "hive.metastore.client.factory.class": "com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory",
        "hive.metastore.glue.catalogid": "acct-id"
      }
    },
  ]
  ```

## IAM Permissions<a name="emr-hive-glue-permissions"></a>

The EC2 instance profile for a cluster must have IAM permissions for AWS Glue actions\. In addition, if you enable encryption for AWS Glue Data Catalog objects, the role must also be allowed to encrypt, decrypt and generate the customer master key \(CMK\) used for encryption\.

### Permissions for AWS Glue Actions<a name="emr-hive-glue-permissions-actions"></a>

The default `AmazonElasticMapReduceforEC2Role` managed policy attached to `EMR_EC2_DefaultRole` allows the required AWS Glue actions\. If you use the default EC2 instance profile, no action is required\. However, if you specify a custom EC2 instance profile and permissions when you create a cluster, ensure that the appropriate AWS Glue actions are allowed\. Use the `AmazonElasticMapReduceforEC2Role` managed policy as a starting point\. For a listing of AWS Glue actions, see [Service Role for Cluster EC2 Instances \(EC2 Instance Profile\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-role-for-ec2.html) in the *Amazon EMR Management Guide*\.

### Permissions for Encrypting and Decrypting AWS Glue Data Catalog<a name="emr-hive-glue-permissions-encrypt"></a>

This section is about the encryption feature of the AWS Glue Data Catalog\. For more information about AWS Glue Data Catalog encryption, see [Encrypting Your Data Catalog](https://docs.aws.amazon.com/glue/latest/dg/encrypt-glue-data-catalog.html) in the *AWS Glue Developer Guide*\.

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

### Resource\-Based Permissions<a name="emr-hive-glue-permissions-resource"></a>

If you use AWS Glue in conjunction with Hive, Spark, or Presto in Amazon EMR, AWS Glue supports resource\-based policies to control access to Data Catalog resources\. These resources include databases, tables, connections, and user\-defined functions\. For more information, see [AWS Glue Resource Policies](https://docs.aws.amazon.com/glue/latest/dg/glue-resource-policies.html) in the *AWS Glue Developer Guide*\.

When using resource\-based policies to limit access to AWS Glue from within Amazon EMR, the principal that you specify in the permissions policy must be the role ARN associated with the EC2 instance profile that is specified when a cluster is created\. For example, for a resource\-based policy attached to a catalog, you can specify the role ARN for the default service role for cluster EC2 instances, *EMR\_EC2\_DefaultRole* as the `Principal`, using the format shown in the following example:

```
arn:aws:iam::acct-id:role/EMR_EC2_DefaultRole
```

The *acct\-id* can be different from the AWS Glue account ID\. This enables access from EMR clusters in different accounts\. You can specify multiple principals, each from a different account\.

## Considerations When Using AWS Glue Data Catalog<a name="emr-hive-glue-considerations-hive"></a>

Consider the following items when using AWS Glue Data Catalog as a metastore with Spark:
+ Having a default database without a location URI causes failures when you create a table\. As a workaround, use the `LOCATION` clause to specify a bucket location, such as `s3://mybucket`, when you use `CREATE TABLE`\. Alternatively create tables within a database other than the default database\.
+ Renaming tables from within AWS Glue is not supported\.
+ When you create a Hive table without specifying a `LOCATION`, the table data is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table data is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](https://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 
+ Partition values containing quotes and apostrophes are not supported, for example, `PARTITION (owner="Doe's").`
+ [Column statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ColumnStatistics) are not supported\.
+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\. As an alternative, consider using [AWS Glue Resource\-Based Policies](https://docs.aws.amazon.com/glue/latest/dg/glue-resource-policies.html)\. For more information, see [Use Resource\-Based Policies for Amazon EMR Access to AWS Glue Data Catalog](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-roles-glue.html)\.
+ [Hive constraints](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-Constraints) are not supported\.
+ [Cost\-based Optimization in Hive](https://cwiki.apache.org/confluence/display/Hive/Cost-based+optimization+in+Hive) is not supported\. Changing the value of `hive.cbo.enable` to `true` is not supported\.
+ Setting `hive.metastore.partition.inherit.table.properties` is not supported\. 
+ Using the following metastore constants is not supported: `BUCKET_COUNT, BUCKET_FIELD_NAME, DDL_TIME, FIELD_TO_DIMENSION, FILE_INPUT_FORMAT, FILE_OUTPUT_FORMAT, HIVE_FILTER_FIELD_LAST_ACCESS, HIVE_FILTER_FIELD_OWNER, HIVE_FILTER_FIELD_PARAMS, IS_ARCHIVED, META_TABLE_COLUMNS, META_TABLE_COLUMN_TYPES, META_TABLE_DB, META_TABLE_LOCATION, META_TABLE_NAME, META_TABLE_PARTITION_COLUMNS, META_TABLE_SERDE, META_TABLE_STORAGE, ORIGINAL_LOCATION`\.
+ When you use a predicate expression, explicit values must be on the right side of the comparison operator, or queries might fail\.
  + **Correct**: `SELECT * FROM mytable WHERE time > 11`
  + **Incorrect**: `SELECT * FROM mytable WHERE 11 > time`
+ We do not recommend using user\-defined functions \(UDFs\) in predicate expressions\. Queries may fail because of the way Hive tries to optimize query execution\.
+ [Temporary tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-TemporaryTables) are not supported\.
+ We recommend creating tables using applications through Amazon EMR rather than creating them directly using AWS Glue\. Creating a table through AWS Glue may cause required fields to be missing and cause query exceptions\.
+ In EMR 5\.20\.0 or later, parallel partition pruning is enabled automatically for Spark and Hive when AWS Glue Data Catalog is used as the metastore\. This change significantly reduces query planning time by executing multiple requests in parallel to retrieve partitions\. The total number of segments that can be executed concurrently range between 1 and 10\. The default value is 5, which is a recommended setting\. You can change it by specifying the property `aws.glue.partition.num.segments` in `hive-site` configuration classification\. If throttling occurs, you can turn off the feature by changing the value to 1\. For more information, see [AWS Glue Segment Structure](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-catalog-partitions.html#aws-glue-api-catalog-partitions-Segment)\.