# Apache HCatalog<a name="emr-hcatalog"></a>

HCatalog is a tool that allows you to access Hive metastore tables within Pig, Spark SQL, and/or custom MapReduce applications\. HCatalog has a REST interface and command line client that allows you to create tables or do other operations\. You then write your applications to access the tables using HCatalog libraries\. For more information, see [Using HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog+UsingHCat)\. HCatalog is included in Amazon EMR release version 4\.4\.0 and later\.

HCatalog on Amazon EMR release version 5\.8\.0 and later supports using AWS Glue Data Catalog as the metastore for Hive\. For more information, see [Using AWS Glue Data Catalog as the metastore for Hive](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive-metastore-glue.html)\.

The following table lists the version of HCatalog included in the latest release of the Amazon EMR 6\.x series, along with the components that Amazon EMR installs with HCatalog\.

For the version of components installed with HCatalog in this release, see [Release 6\.5\.0 Component Versions](emr-650-release.md)\.


**HCatalog version information for emr\-6\.5\.0**  

| Amazon EMR Release Label | HCatalog Version | Components Installed With HCatalog | 
| --- | --- | --- | 
| emr\-6\.5\.0 | HCatalog 3\.1\.2 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hcatalog\-client, hcatalog\-server, hcatalog\-webhcat\-server, hive\-client, mariadb\-server | 

The following table lists the version of HCatalog included in the latest release of the Amazon EMR 5\.x series, along with the components that Amazon EMR installs with HCatalog\.

For the version of components installed with HCatalog in this release, see [Release 5\.34\.0 Component Versions](emr-5340-release.md)\.


**HCatalog version information for emr\-5\.34\.0**  

| Amazon EMR Release Label | HCatalog Version | Components Installed With HCatalog | 
| --- | --- | --- | 
| emr\-5\.34\.0 | HCatalog 2\.3\.8 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hcatalog\-client, hcatalog\-server, hcatalog\-webhcat\-server, hive\-client, mariadb\-server | 

**Topics**
+ [Creating a cluster with HCatalog](emr-hcatalog-create-cluster.md)
+ [Using HCatalog](emr-hcatalog-using.md)
+ [Example: Create an HCatalog table and write to it using Pig](emr-hcatalog-pig.md)
+ [HCatalog release history](HCatalog-release-history.md)