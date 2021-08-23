# Apache Phoenix<a name="emr-phoenix"></a>

Apache Phoenix is used for OLTP and operational analytics, allowing you to use standard SQL queries and JDBC APIs to work with an Apache HBase backing store\. For more information, see [Phoenix in 15 minutes or less](https://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html)\. Phoenix is included in Amazon EMR release version 4\.7\.0 and later\.

If you upgrade from an earlier version of Amazon EMR to Amazon EMR release version 5\.4\.0 or later and use secondary indexing, upgrade local indexes as described in the [Apache Phoenix documentation](https://phoenix.apache.org/secondary_indexing.html#Upgrading_Local_Indexes_created_before_4.8.0)\. Amazon EMR removes the required configurations from the `hbase-site` classification, but indexes need to be repopulated\. Online and offline upgrade of indexes are supported\. Online upgrades are the default, which means indexes are repopulated while initializing from Phoenix clients of version 4\.8\.0 or greater\. To specify offline upgrades, set the `phoenix.client.localIndexUpgrade` configuration to false in the `phoenix-site` classification, and then SSH to the master node to run `psql [zookeeper] -1`\.

The following table lists the version of Phoenix included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Phoenix\.

For the version of components installed with Phoenix in this release, see [Release 6\.3\.0 Component Versions](emr-release-6x.md#emr-630-release)\.


**Phoenix version information for emr\-6\.3\.0**  

| Amazon EMR Release Label | Phoenix Version | Components Installed With Phoenix | 
| --- | --- | --- | 
| emr\-6\.3\.0 | Phoenix 5\.0\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-mapred, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hbase\-hmaster, hbase\-client, hbase\-region\-server, phoenix\-library, phoenix\-query\-server, zookeeper\-client, zookeeper\-server | 

The following table lists the version of Phoenix included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Phoenix\.

For the version of components installed with Phoenix in this release, see [Release 5\.33\.0 Component Versions](emr-release-5x.md#emr-5330-release)\.


**Phoenix version information for emr\-5\.33\.0**  

| Amazon EMR Release Label | Phoenix Version | Components Installed With Phoenix | 
| --- | --- | --- | 
| emr\-5\.33\.0 | Phoenix 4\.14\.3 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-mapred, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hbase\-hmaster, hbase\-client, hbase\-region\-server, phoenix\-library, phoenix\-query\-server, zookeeper\-client, zookeeper\-server | 

**Topics**
+ [Creating a cluster with Phoenix](phoenix-create-cluster.md)
+ [Phoenix clients](emr-phoenix-clients.md)
+ [Phoenix release history](Phoenix-release-history.md)