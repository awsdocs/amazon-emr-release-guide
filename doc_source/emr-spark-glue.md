# Using the AWS Glue Data Catalog as the Metastore for Spark SQL<a name="emr-spark-glue"></a>

Using Amazon EMR version 5\.8\.0 or later, you can configure Spark SQL to use the AWS Glue Data Catalog as its metastore\. We recommend this configuration when you require a persistent metastore or a metastore shared by different clusters, services, and applications\.

AWS Glue is a fully managed extract, transform, and load \(ETL\) service that makes it simple and cost\-effective to categorize your data, clean it, enrich it, and move it reliably between various data stores\. The AWS Glue Data Catalog provides a unified metadata repository across a variety of data sources and data formats, integrating with Amazon EMR as well as Amazon RDS, Amazon Redshift, Redshift Spectrum, Athena, and any application compatible with the Apache Hive metastore\. AWS Glue crawlers can automatically infer schema from source data in Amazon S3 and store the associated metadata in the Data Catalog\. For more information about the Data Catalog, see [Populating the AWS Glue Data Catalog](http://docs.aws.amazon.com/glue/latest/dg/populate-data-catalog.html) in the *AWS Glue Developer Guide*\.

Separate charges apply for AWS Glue\. There is a monthly rate for storing and accessing the metadata in the Data Catalog, an hourly rate billed per minute for AWS Glue ETL jobs and crawler runtime, and an hourly rate billed per minute for each provisioned development endpoint\. The Data Catalog allows you to store up to a million objects at no charge\. If you store more than a million objects, you are charged USD$1 for each 100,000 objects over a million\. An object in the Data Catalog is a table, partition, or database\. For more information, see [Glue Pricing](https://aws.amazon.com//glue/pricing)\.

**Important**  
If you created tables using Amazon Athena or Amazon Redshift Spectrum before August 14, 2017, databases and tables are stored in an Athena\-managed catalog, which is separate from the AWS Glue Data Catalog\. To integrate Amazon EMR with these tables, you must upgrade to the AWS Glue Data Catalog\. For more information, see [Upgrading to the AWS Glue Data Catalog](http://docs.aws.amazon.com/athena/latest/ug/glue-upgrade.html) in the *Amazon Athena User Guide*\.

## Specifying AWS Glue Data Catalog as the Metastore<a name="emr-spark-glue-configure"></a>

You can specify the AWS Glue Data Catalog as the metastore using the AWS Management Console, AWS CLI, or Amazon EMR API\. When you create a cluster using the CLI or API, you use the `spark-hive-site` configuration classification to specify the Data Catalog\. When you create a cluster using the console, you can specify the Data Catalog using **Advanced Options** or **Quick Options**\.

**Note**  
The option to use AWS Glue Data Catalog is also available with Zeppelin because Zeppelin is installed with Spark SQL components\.

**To specify the AWS Glue Data Catalog as the metastore for Spark SQL using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. For **Release**, choose **emr\-5\.8\.0** or later\.

1. Under **Release**, select **Spark** or **Zeppelin**\.

1. Under **AWS Glue Data Catalog settings**, select **Use for Hive table metadata**\.

1. Choose other options for your cluster as appropriate, choose **Next**, and then configure other cluster options as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the metastore using the AWS CLI or Amazon EMR API**

+ Specify the value for `hive.metastore.client.factory.class` using the `spark-hive-site` classification as shown in the following example\. For more information, see [Configuring Applications](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.  
**Example Example Configuration JSON for Using the AWS Glue Data Catalog**  

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

## IAM Permissions<a name="emr-hive-glue-permissions"></a>

The `EMR_EC2_DefaultRole` must be allowed IAM permissions for AWS Glue actions\. This is only a concern if you don't use the default `AmazonElasticMapReduceforEC2Role` managed policy and you attach a customer\-managed policy to the role\. In this case, you need to configure the policy to allow permission to perform AWS Glue actions\. Open the IAM console \([https://console\.aws\.amazon\.com/iam/](https://console.aws.amazon.com/iam/)\) and view the contents of the `AmazonElasticMapReduceforEC2Role` managed policy to see the required AWS Glue actions to allow\.

## Considerations When Using AWS Glue Data Catalog<a name="emr-hive-glue-considerations-hive"></a>

Consider the following items when using AWS Glue Data Catalog as a metastore with Spark:

+ Having a default database without a location URI causes failures when you create a table\. As a workaround, use the `LOCATION` clause to specify a bucket location, such as `s3://mybucket`, when you use `CREATE TABLE`\. Alternatively create tables within a database other than the default database\.

+ Renaming tables from within AWS Glue is not supported\.

+ When you create a Hive table without specifying a `LOCATION`, the table definition is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table definition is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](http://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 

+ Partition values containing quotes and apostrophes are not supported \(for example, `PARTITION (owner="Doe's").`

+ [Table and partition statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-TableandPartitionStatistics) are not supported\.

+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\.

+ [Hive constraints](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-Constraints) are not supported\.

+ Setting `hive.metastore.partition.inherit.table.properties` is not supported\. 

+ Using the following metastore constants is not supported: `BUCKET_COUNT, BUCKET_FIELD_NAME, DDL_TIME, FIELD_TO_DIMENSION, FILE_INPUT_FORMAT, FILE_OUTPUT_FORMAT, HIVE_FILTER_FIELD_LAST_ACCESS, HIVE_FILTER_FIELD_OWNER, HIVE_FILTER_FIELD_PARAMS, IS_ARCHIVED, META_TABLE_COLUMNS, META_TABLE_COLUMN_TYPES, META_TABLE_DB, META_TABLE_LOCATION, META_TABLE_NAME, META_TABLE_PARTITION_COLUMNS, META_TABLE_SERDE, META_TABLE_STORAGE, ORIGINAL_LOCATION`\.

+ When you use a predicate expression, explicit values must be on the right side of the comparison operator, or queries might fail\.

  + **Correct**: `SELECT * FROM mytable WHERE time > 11`

  + **Incorrect**: `SELECT * FROM mytable WHERE 11 > time`

+ We do not recommend using user\-defined functions \(UDFs\) in predicate expressions\. Queries may fail because of the way Hive tries to optimize query execution\.

+ [Temporary tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-TemporaryTables) are not supported\.