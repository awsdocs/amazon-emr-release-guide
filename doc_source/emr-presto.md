# Presto and Trino<a name="emr-presto"></a>

**Note**  
PrestoSQL was renamed to Trino in December 2020\. Amazon EMR versions 6\.4\.0 and later use the name Trino, while earlier release versions use the name PrestoSQL\.

[Presto](https://aws.amazon.com/big-data/what-is-presto/) is a fast SQL query engine designed for interactive analytic queries over large datasets from multiple sources\. For more information, see the [Presto website](https://prestodb.io/)\. Presto is included in Amazon EMR release versions 5\.0\.0 and later\. Earlier release versions include Presto as a sandbox application\. For more information, see [Amazon EMR 4\.x release versions](emr-release-4x.md)\. Amazon EMR release versions 6\.1\.0 and later support [Trino](https://trino.io/) \(PrestoSQL\) in addition to Presto\. For more information, see [Installing PrestoDB and Trino](emr-presto-considerations.md#emr-prestodb-prestosql)\.

The following table lists the version of Presto included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Presto\.

For the version of components installed with Presto in this release, see [Release 6\.4\.0 Component Versions](emr-640-release.md)\.


**Presto version information for emr\-6\.4\.0**  

| Amazon EMR Release Label | Presto Version | Components Installed With Presto | 
| --- | --- | --- | 
| emr\-6\.4\.0 | Presto 0\.254\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hive\-client, hudi, hudi\-presto, hcatalog\-server, mariadb\-server, presto\-coordinator, presto\-worker | 

The following table lists the version of Presto included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Presto\.

For the version of components installed with Presto in this release, see [Release 5\.33\.0 Component Versions](emr-5330-release.md)\.


**Presto version information for emr\-5\.33\.0**  

| Amazon EMR Release Label | Presto Version | Components Installed With Presto | 
| --- | --- | --- | 
| emr\-5\.33\.0 | Presto 0\.245\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hive\-client, hudi, hudi\-presto, hcatalog\-server, mariadb\-server, presto\-coordinator, presto\-worker | 

**Topics**
+ [Considerations with Presto on Amazon EMR](emr-presto-considerations.md)
+ [Using Presto with the AWS Glue Data Catalog](emr-presto-glue.md)
+ [Using S3 Select Pushdown with Presto to improve performance](emr-presto-s3select.md)
+ [Adding database connectors](presto-adding-db-connectors.md)
+ [Using SSL/TLS and configuring LDAPS with Presto on Amazon EMR](presto-ssl.md)
+ [Using Presto automatic scaling with Graceful Decommission](presto-graceful-autoscale.md)
+ [Presto release history](Presto-release-history.md)