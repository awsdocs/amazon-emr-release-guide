# Configuring an External Metastore for Hive<a name="emr-metastore-external-hive"></a>

By default, Hive records metastore information in a MySQL database on the master node's file system\. The metastore contains a description of the table and the underlying data on which it is built, including the partition names, data types, and so on\. When a cluster terminates, all cluster nodes shut down, including the master node\. When this happens, local data is lost because node file systems use ephemeral storage\. If you need the metastore to persist, you must create an *external metastore* that exists outside the cluster\.

You have two options for an external metastore:
+ AWS Glue Data Catalog \(Amazon EMR version 5\.8\.0 or later only\)\.

  For more information, see [Using the AWS Glue Data Catalog as the Metastore for Hive](emr-hive-metastore-glue.md)\.
+ Amazon RDS or Amazon Aurora\.

  For more information, see [Using an External MySQL Database or Amazon Aurora](emr-hive-metastore-external.md)\.