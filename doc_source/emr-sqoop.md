# Apache Sqoop<a name="emr-sqoop"></a>

Apache Sqoop is a tool for transferring data between Amazon S3, Hadoop, HDFS, and RDBMS databases\. For more information, see the [Apache Sqoop website](http://sqoop.apache.org/)\. Sqoop is included in Amazon EMR release version 5\.0\.0 and later\. Earlier release versions include Sqoop as a sandbox application\. For more information, see [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

The following table lists the version of Sqoop included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Sqoop\.

For the version of components installed with Sqoop in this release, see [Release 5\.29\.0 Component Versions](emr-release-5x.md#emr-5290-release)\.


**Sqoop Version Information for emr\-5\.29\.0**  

| Amazon EMR Release Label | Sqoop Version | Components Installed With Sqoop | 
| --- | --- | --- | 
| emr\-5\.29\.0 | Sqoop 1\.4\.7 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, mysql\-server, sqoop\-client | 

**Topics**
+ [Considerations with Sqoop on Amazon EMR](emr-sqoop-considerations.md)
+ [Sqoop Release History](Sqoop-release-history.md)