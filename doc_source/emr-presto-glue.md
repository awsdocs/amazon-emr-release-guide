# Using Presto with the AWS Glue Data Catalog<a name="emr-presto-glue"></a>

Using Amazon EMR release version 5\.10\.0 and later, you can specify the AWS Glue Data Catalog as the default Hive metastore for Presto\. You can specify this option when you create a cluster using the AWS Management Console, or using the `presto-connector-hive` configuration classification when using the AWS CLI or Amazon EMR API\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Under **Software Configuration** choose a **Release** of **emr\-5\.10\-0** or later and select **Presto**\.

1. Select **Use for Presto table metadata**, choose **Next**, and then complete other settings for your cluster as appropriate for your application\.

**To specify the AWS Glue Data Catalog as the default Hive metastore using the CLI or API**
+ Set the `hive.metastore.glue.datacatalog.enabled` property to `true`, as shown in the following JSON example\.

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

Optionally, you can manually set `hive.metastore.glue.datacatalog.enabled=true` in the `/etc/presto/conf/catalog/hive.properties` file on the master node\. If you use this method, make sure that `hive.table-statistics-enabled=false` in the properties file is set because the Data Catalog does not support Hive table and partition statistics\. If you change the value on a long\-running cluster to switch metastores, you must restart the Presto server on the master node \(`sudo restart presto-server`\)\.

## Considerations When Using AWS Glue Data Catalog<a name="emr-presto-glue-knownissues"></a>

Consider the following items when using AWS Glue Data Catalog as a metastore with Presto:
+ Renaming tables from within AWS Glue is not supported\.
+ When you create a Hive table without specifying a `LOCATION`, the table definition is stored in the location specified by the `hive.metastore.warehouse.dir` property\. By default, this is a location in HDFS\. If another cluster needs to access the table, it fails unless it has adequate permissions to the cluster that created the table\. Furthermore, because HDFS storage is transient, if the cluster terminates, the table definition is lost, and the table must be recreated\. We recommend that you specify a `LOCATION` in Amazon S3 when you create a Hive table using AWS Glue\. Alternatively, you can use the `hive-site` configuration classification to specify a location in Amazon S3 for `hive.metastore.warehouse.dir`, which applies to all Hive tables\. If a table is created in an HDFS location and the cluster that created it is still running, you can update the table location to Amazon S3 from within AWS Glue\. For more information, see [Working with Tables on the AWS Glue Console](http://docs.aws.amazon.com/glue/latest/dg/console-tables.html) in the *AWS Glue Developer Guide*\. 
+ Partition values containing quotes and apostrophes are not supported \(for example, `PARTITION (owner="Doe's").`
+ [Table and partition statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-TableandPartitionStatistics) are not supported\.
+ Using [Hive authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) is not supported\.