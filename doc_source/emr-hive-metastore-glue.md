# Using the AWS Glue Data Catalog as the Metastore for Hive<a name="emr-hive-metastore-glue"></a>

Using Amazon EMR version 5\.8\.0 or later, you can configure Hive to use the AWS Glue Data Catalog as its metastore\. We recommend this configuration when you require a persistent metastore or a metastore shared by different clusters, services, and applications\.

AWS Glue is a fully managed extract, transform, and load \(ETL\) service that makes it simple and cost\-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores\. The AWS Glue Data Catalog provides a unified metadata repository across a variety of data sources and data formats, integrating with Amazon EMR as well as Amazon RDS, Amazon Redshift, Redshift Spectrum, Athena, and any application compatible with the Apache Hive metastore\. AWS Glue crawlers can automatically infer schema from source data in Amazon S3 and store the associated metadata in the Data Catalog\. For more information about the Data Catalog, see [Populating the AWS Glue Data Catalog](http://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html) in the *AWS Glue Developer Guide*\.

Separate charges apply for AWS Glue\. There is a monthly rate for storing and accessing the metadata in the Data Catalog, an hourly rate billed per minute for AWS Glue ETL jobs and crawler runtime, and an hourly rate billed per minute for each provisioned development endpoint\. The Data Catalog allows you to store up to a million objects at no charge\. If you store more than a million objects, you are charged USD$1 for each 100,000 objects over a million\. An object in the Data Catalog is a table, partition, or database\. For more information, see [Glue Pricing](https://aws.amazon.com//glue/pricing)\.

**Important**  
If you created tables using Amazon Athena or Amazon Redshift Spectrum before August 14, 2017, databases and tables are stored in an Athena\-managed catalog, which is separate from the AWS Glue Data Catalog\. To integrate Amazon EMR with these tables, you must upgrade to the AWS Glue Data Catalog\. For more information, see [Upgrading to the AWS Glue Data Catalog](http://docs.aws.amazon.com/athena/latest/ug/glue-upgrade.html) in the *Amazon Athena User Guide*\.

## Specifying AWS Glue Data Catalog as the Metastore<a name="emr-hive-glue-configure"></a>

You can specify the AWS Glue Data Catalog as the metastore using the AWS Management Console, AWS CLI, or Amazon EMR API\. When you create a cluster using the CLI or API, you use the `hive-site` configuration classification to specify the Data Catalog\. When you create a cluster using the console, you can specify the Data Catalog using **Advanced Options** or **Quick Options**\.

**Note**  
The option to use the Data Catalog is also available with HCatalog because Hive is installed with HCatalog\.

**To specify AWS Glue Data Catalog as the metastore using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. For **Release**, choose **emr\-5\.8\.0** or later\.

1. Under **Release**, select **Hive** or **HCatalog**\.

1. Under **AWS Glue Data Catalog settings** select **Use for Hive table metadata**\.

1. Choose other options for your cluster as appropriate, choose **Next**, and then configure other cluster options as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the metastore using the AWS CLI or Amazon EMR API**
+ Specify the value for `hive.metastore.client.factory.class` using the `hive-site` classification as shown in the following example\. For more information, see [Configuring Applications](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.

  Example Configuration JSON for Using the AWS Glue Data Catalog:

  ```
  [
    {
      "Classification": "hive-site",
      "Properties": {
        "hive.metastore.client.factory.class": "com.amazonaws.glue.catalog.metastore.AWSGlueDataCatalogHiveClientFactory"
      }
    }
  ]
  ```

## IAM Permissions<a name="emr-hive-glue-permissions"></a>

The EC2 instance profile for a cluster must have IAM permissions for AWS Glue actions\. In addition, if you enable encryption for AWS Glue Data Catalog objects, the role must also be allowed to encrypt, decrypt and generate the customer master key \(CMK\) used for encryption\.

### Permissions for AWS Glue Actions<a name="w3aac26c23c11c17b5"></a>

The default `AmazonElasticMapReduceforEC2Role` managed policy attached to `EMR_EC2_DefaultRole` allows the required AWS Glue actions\. If you use the default EC2 instance profile, no action is required\. However, if you specify a custom EC2 instance profile and permissions when you create a cluster, ensure that the appropriate AWS Glue actions are allowed\. Use the `AmazonElasticMapReduceforEC2Role` managed policy as a starting point\. For a listing of AWS Glue actions, see [Default Contents of AmazonElasticMapReduceforEC2Role Permissions Policy](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-roles-defaultroles.html#emr-iam-contents-ec2role) in the *Amazon EMR Management Guide*\.

### Permissions for Encrypting and Decrypting AWS Glue Data Catalog<a name="w3aac26c23c11c17b7"></a>

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

## Considerations When Using AWS Glue Data Catalog<a name="emr-hive-glue-considerations-hive"></a>

Consider the following items when using the AWS Glue Data Catalog as the metastore with Hive:
+ Adding auxiliary JARs using the Hive shell is not supported\. As a workaround, use the `hive-site` configuration classification to set the `hive.aux.jars.path` property, which adds auxiliary JARs into the Hive classpath\.
+ The [VALUES keyword](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML#LanguageManualDML-InsertingvaluesintotablesfromSQL) is not supported\.
+ [Hive transactions](https://cwiki.apache.org/confluence/display/Hive/Hive+Transactions) are not supported\.
+ Renaming tables from within AWS Glue is not supported\.
+ When you create a Hive table without specifying a `LOCATION`, the table definition is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table definition is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](http://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 
+ Partition values containing quotes and apostrophes are not supported \(for example, `PARTITION (owner="Doe's").`
+ [Column statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ColumnStatistics) are not supported\.
+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\.
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