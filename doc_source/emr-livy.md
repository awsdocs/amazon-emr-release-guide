# Apache Livy<a name="emr-livy"></a>

Livy enables interaction over a REST interface with an EMR cluster running Spark\. You can use the REST interface or an RPC client library to submit Spark jobs or snippets of Spark code, retrieve results synchronously or asynchronously, and manage Spark Context\. For more information, see the [Apache Livy website](https://livy.incubator.apache.org/)\. Livy is included in Amazon EMR release version 5\.9\.0 and later\.

To access the Livy web interface, set up an SSH tunnel to the master node and a proxy connection\. For more information, see [View Web Interfaces Hosted on EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html)\.

The following table lists the version of Livy included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Livy\.

For the version of components installed with Livy in this release, see [Release 6\.2\.0 Component Versions](emr-release-6x.md#emr-620-release)\.


**Livy Version Information for emr\-6\.2\.0**  

| Amazon EMR Release Label | Livy Version | Components Installed With Livy | 
| --- | --- | --- | 
| emr\-6\.2\.0 | Livy 0\.7\.0 | aws\-sagemaker\-spark\-sdk, emrfs, emr\-goodies, emr\-ddb, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, r, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, livy\-server, nginx | 

The following table lists the version of Livy included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Livy\.

For the version of components installed with Livy in this release, see [Release 5\.32\.0 Component Versions](emr-release-5x.md#emr-5320-release)\.


**Livy Version Information for emr\-5\.32\.0**  

| Amazon EMR Release Label | Livy Version | Components Installed With Livy | 
| --- | --- | --- | 
| emr\-5\.32\.0 | Livy 0\.7\.0 | aws\-sagemaker\-spark\-sdk, emrfs, emr\-goodies, emr\-ddb, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, r, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, livy\-server, nginx | 

**Topics**
+ [Livy Release History](Livy-release-history.md)