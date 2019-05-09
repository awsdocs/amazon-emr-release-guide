# Apache HBase<a name="emr-hbase"></a>

[HBase](https://aws.amazon.com//elasticmapreduce/details/hbase/) is an open source, non\-relational, distributed database developed as part of the Apache Software Foundation's Hadoop project\. HBase runs on top of Hadoop Distributed File System \(HDFS\) to provide non\-relational database capabilities for the Hadoop ecosystem\. HBase is included with Amazon EMR release version 4\.6\.0 and later\.

HBase works seamlessly with Hadoop, sharing its file system and serving as a direct input and output to the MapReduce framework and execution engine\. HBase also integrates with Apache Hive, enabling SQL\-like queries over HBase tables, joins with Hive\-based tables, and support for Java Database Connectivity \(JDBC\)\. For more information about HBase, see [Apache HBase](https://hbase.apache.org/) and [HBase documentation](http://hbase.apache.org/book.html) on the Apache website\. For an example of how to use HBase with Hive, see the AWS Big Data Blog post [Combine NoSQL and Massively Parallel Analytics Using Apache HBase and Apache Hive on Amazon EMR](http://aws.amazon.com/blogs/big-data/combine-nosql-and-massively-parallel-analytics-using-apache-hbase-and-apache-hive-on-amazon-emr/)\.

With HBase on Amazon EMR, you can also back up your HBase data directly to Amazon Simple Storage Service \(Amazon S3\), and restore from a previously created backup when launching an HBase cluster\. Amazon EMR offers additional options to integrate with Amazon S3 for data persistence and disaster recovery\. 
+ **HBase on Amazon S3**—With Amazon EMR version 5\.2\.0 and later, you can use HBase on Amazon S3 to store a cluster's HBase root directory and metadata directly to Amazon S3\. You can subsequently start a new cluster, pointing it to the root directory location in Amazon S3\. Only one cluster at a time can use the HBase location in Amazon S3, with the exception of a read\-replica cluster\. For more information, see [HBase on Amazon S3 \(Amazon S3 Storage Mode\)](emr-hbase-s3.md)\.
+ **HBase read\-replicas**—Amazon EMR version 5\.7\.0 and later with HBase on Amazon S3 supports read\-replica clusters\. A read\-replica cluster provides read\-only access to a primary cluster's store files and metadata for read\-only operations\. For more information, see [Using a Read\-Replica Cluster](emr-hbase-s3.md#emr-hbase-s3-read-replica)\.
+ **HBase Snapshots**—As an alternative to HBase on Amazon S3, with EMR version 4\.0 and later you can create snapshots of your HBase data directly to Amazon S3 and then recover data using the snapshots\. For more information, see [Using HBase Snapshots](emr-hbase-snapshot.md)\.

The following table lists the version of HBase included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with HBase\.

For the version of components installed with HBase in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**HBase Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | HBase Version | Components Installed With HBase | 
| --- | --- | --- | 
| emr\-5\.23\.0 | HBase 1\.4\.9 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-mapred, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hbase\-hmaster, hbase\-client, hbase\-region\-server, hbase\-rest\-server, hbase\-thrift\-server, zookeeper\-client, zookeeper\-server | 

**Topics**
+ [Creating a Cluster with HBase](emr-hbase-create.md)
+ [HBase on Amazon S3 \(Amazon S3 Storage Mode\)](emr-hbase-s3.md)
+ [Using the HBase Shell](emr-hbase-connect.md)
+ [Access HBase Tables with Hive](emr-hbase-access-hive.md)
+ [Using HBase Snapshots](emr-hbase-snapshot.md)
+ [Configure HBase](emr-hbase-configure.md)
+ [View the HBase User Interface](hbase-web-ui.md)
+ [View HBase Log Files](emr-hbase-log-files.md)
+ [Monitor HBase with Ganglia](emr-hbase-ganglia.md)
+ [Migrating from Previous HBase Versions](emr-hbase-migrate.md)
+ [HBase Release History](HBase-release-history.md)