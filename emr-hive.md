# Apache Hive<a name="emr-hive"></a>

Hive is an open\-source, data warehouse, and analytic package that runs on top of a Hadoop cluster\. Hive scripts use an SQL\-like language called Hive QL \(query language\) that abstracts programming models and supports typical data warehouse interactions\. Hive enables you to avoid the complexities of writing Tez jobs based on directed acyclic graphs \(DAGs\) or MapReduce programs in a lower level computer language, such as Java\. 

Hive extends the SQL paradigm by including serialization formats\. You can also customize query processing by creating table schema that match your data, without touching the data itself\. In contrast to SQL \(which only supports primitive value types such as dates, numbers, and strings\), values in Hive tables are structured elements, such as JSON objects, any user\-defined data type, or any function written in Java\. 

For more information about Hive, see [http://hive\.apache\.org/](http://hive.apache.org/)\.

The following table lists the version of Hive included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Hive\.

For the version of components installed with Hive in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**Hive Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | Hive Version | Components Installed With Hive | 
| --- | --- | --- | 
| emr\-5\.23\.0 | Hive 2\.3\.4 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, emr\-s3\-select, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hive\-client, hive\-hbase, hcatalog\-server, hive\-server2, mysql\-server, tez\-on\-yarn | 

Beginning with Amazon EMR 5\.18\.0, you can use the Amazon EMR artifact repository to build your job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions\. For more information, see [Checking Dependencies Using the Amazon EMR Artifact Repository](emr-artifact-repository.md)\.

**Topics**
+ [Differences and Considerations for Hive on Amazon EMR](emr-hive-differences.md)
+ [Configuring an External Metastore for Hive](emr-metastore-external-hive.md)
+ [Use the Hive JDBC Driver](HiveJDBCDriver.md)
+ [Using S3 Select with Hive to Improve Performance](emr-hive-s3select.md)
+ [Hive Release History](Hive-release-history.md)