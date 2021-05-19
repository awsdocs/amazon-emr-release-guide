# Apache Zeppelin<a name="emr-zeppelin"></a>

Use Apache Zeppelin as a notebook for interactive data exploration\. For more information about Zeppelin, see [https://zeppelin\.apache\.org/](https://zeppelin.apache.org/)\. Zeppelin is included in Amazon EMR release version 5\.0\.0 and later\. Earlier release versions include Zeppelin as a sandbox application\. For more information, see [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

To access the Zeppelin web interface, set up an SSH tunnel to the master node and a proxy connection\. For more information, see [View Web Interfaces Hosted on EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html)\.

The following table lists the version of Zeppelin included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Zeppelin\.

For the version of components installed with Zeppelin in this release, see [Release 6\.3\.0 Component Versions](emr-release-6x.md#emr-630-release)\.


**Zeppelin Version Information for emr\-6\.3\.0**  

| Amazon EMR Release Label | Zeppelin Version | Components Installed With Zeppelin | 
| --- | --- | --- | 
| emr\-6\.3\.0 | Zeppelin 0\.9\.0 | aws\-sagemaker\-spark\-sdk, emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, livy\-server, r, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 

The following table lists the version of Zeppelin included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Zeppelin\.

For the version of components installed with Zeppelin in this release, see [Release 5\.33\.0 Component Versions](emr-release-5x.md#emr-5330-release)\.


**Zeppelin Version Information for emr\-5\.33\.0**  

| Amazon EMR Release Label | Zeppelin Version | Components Installed With Zeppelin | 
| --- | --- | --- | 
| emr\-5\.33\.0 | Zeppelin 0\.9\.0 | aws\-sagemaker\-spark\-sdk, emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, livy\-server, r, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 

**Topics**
+ [Considerations When Using Zeppelin on Amazon EMR](zeppelin-considerations.md)
+ [Zeppelin Release History](Zeppelin-release-history.md)