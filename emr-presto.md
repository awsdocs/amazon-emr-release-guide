# Presto<a name="emr-presto"></a>

[Presto](https://aws.amazon.com/big-data/what-is-presto/) is a fast SQL query engine designed for interactive analytic queries over large datasets from multiple sources\. For more information, see the [Presto website](https://prestodb.io/)\. Presto is included in Amazon EMR release version 5\.0\.0 and later\. Earlier release versions include Presto as a sandbox application\. For more information, see [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

The following table lists the version of Presto included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Presto\.

For the version of components installed with Presto in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**Presto Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | Presto Version | Components Installed With Presto | 
| --- | --- | --- | 
| emr\-5\.23\.0 | Presto 0\.215 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 

**Topics**
+ [Considerations with Presto on Amazon EMR](emr-presto-considerations.md)
+ [Using Presto with the AWS Glue Data Catalog](emr-presto-glue.md)
+ [Using S3 Select Pushdown with Presto to Improve Performance](emr-presto-s3select.md)
+ [Adding Database Connectors](presto-adding-db-connectors.md)
+ [Using SSL/TLS and Configuring LDAPS with Presto on Amazon EMR](presto-ssl.md)
+ [Presto Release History](Presto-release-history.md)