# Apache Hadoop<a name="emr-hadoop"></a>

[Apache Hadoop](https://aws.amazon.com/elasticmapreduce/details/hadoop/) is an open\-source Java software framework that supports massive data processing across a cluster of instances\. It can run on a single instance or thousands of instances\. Hadoop uses various processing models, such as MapReduce and Tez, to distribute processing across multiple instances and also uses a distributed file system called HDFS to store data across multiple instances\. Hadoop monitors the health of instances in the cluster and can recover from the failure of one or more nodes\. In this way, Hadoop provides increased processing and storage capacity, as well as high availability\.

For more information, see [http://hadoop.apache.org](http://hadoop.apache.org)

The following table lists the version of Hadoop included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Hadoop\.

For the version of components installed with Hadoop in this release, see [Release 6\.2\.0 Component Versions](emr-release-6x.md#emr-620-release)\.


**Hadoop Version Information for emr\-6\.2\.0**  

| Amazon EMR Release Label | Hadoop Version | Components Installed With Hadoop | 
| --- | --- | --- | 
| emr\-6\.2\.0 | Hadoop 3\.2\.1 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-mapred, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server | 

The following table lists the version of Hadoop included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Hadoop\.

For the version of components installed with Hadoop in this release, see [Release 5\.32\.0 Component Versions](emr-release-5x.md#emr-5320-release)\.


**Hadoop Version Information for emr\-5\.32\.0**  

| Amazon EMR Release Label | Hadoop Version | Components Installed With Hadoop | 
| --- | --- | --- | 
| emr\-5\.32\.0 | Hadoop 2\.10\.1 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-mapred, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server | 

Beginning with Amazon EMR 5\.18\.0, you can use the Amazon EMR artifact repository to build your job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions\. For more information, see [Checking Dependencies Using the Amazon EMR Artifact Repository](emr-artifact-repository.md)\.

**Topics**
+ [Configure Hadoop](emr-hadoop-config.md)
+ [Transparent Encryption in HDFS on Amazon EMR](emr-encryption-tdehdfs.md)
+ [Create or Run a Hadoop Application](emr-hadoop-application.md)
+ [Hadoop Version History](Hadoop-release-history.md)