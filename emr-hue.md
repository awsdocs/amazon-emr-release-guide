# Hue<a name="emr-hue"></a>

Hue \(Hadoop User Experience\) is an open\-source, web\-based, graphical user interface for use with Amazon EMR and Apache Hadoop\. Hue groups together several different Hadoop ecosystem projects into a configurable interface\. Amazon EMR has also added customizations specific to Hue in Amazon EMR\. Hue acts as a front\-end for applications that run on your cluster, allowing you to interact with applications using an interface that may be more familiar or user\-friendly\. The applications in Hue, such as the Hive and Pig editors, replace the need to log in to the cluster to run scripts interactively using each application's respective shell\. After a cluster launches, you might interact entirely with applications using Hue or a similar interface\. For more information about Hue, see [http://gethue\.com](http://gethue.com)\.

Hue is installed by default when you launch your cluster using the Amazon EMR console\. You can choose not to install Hue by using **Advanced options** in the Amazon EMR console when you launch a cluster, or by explicitly specifying the `--applications` option, and omitting Hue, when you use `create-cluster` from the AWS CLI\.

The following table lists the version of Hue included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Hue\.

For the version of components installed with Hue in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**Hue Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | Hue Version | Components Installed With Hue | 
| --- | --- | --- | 
| emr\-5\.23\.0 | Hue 4\.3\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hue\-server, mysql\-server, oozie\-client, oozie\-server | 

**Topics**
+ [Supported and Unsupported Features of Hue on Amazon EMR](emr-hue-supported-features.md)
+ [Launching the Hue Web Interface](accessing-hue.md)
+ [Using Hue with a Remote Database in Amazon RDS](hue-rds.md)
+ [Advanced Configurations for Hue](advanced-configurations.md)
+ [Hue Release History](Hue-release-history.md)