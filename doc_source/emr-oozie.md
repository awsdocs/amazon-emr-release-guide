# Apache Oozie<a name="emr-oozie"></a>

Use the Apache Oozie Workflow Scheduler to manage and coordinate Hadoop jobs\. For more information, see [http://oozie\.apache\.org/](http://oozie.apache.org/)\.

**Important**  
The Oozie native web interface is not supported on Amazon EMR\. To use a front\-end interface for Oozie, try the Hue Oozie application\. For more information, see [Hue](emr-hue.md)\. Oozie is included with Amazon EMR release version 5\.0\.0 and later\. Oozie is included as a sandbox application in earlier releases\. For more information, see [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

The following table lists the version of Oozie included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Oozie\.

For the version of components installed with Oozie in this release, see [Release 5\.14\.0 Component Versions](emr-release-5x.md#emr-5140-release)\.


**Oozie Version Information for emr\-5\.14\.0**  

| Amazon EMR Release Label | Oozie Version | Components Installed With Oozie | 
| --- | --- | --- | 
| emr\-5\.14\.0 | Oozie 4\.3\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, oozie\-client, oozie\-server, tez\-on\-yarn | 

**Topics**
+ [Oozie Release History](Oozie-release-history.md)