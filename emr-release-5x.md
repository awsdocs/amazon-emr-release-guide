# Amazon EMR 5\.x Release Versions<a name="emr-release-5x"></a>

Each tab below lists application versions, release notes, component versions, and configuration classifications available in each Amazon EMR 5\.x release version\.

For a comprehensive diagram of application versions in every release, see [Application Versions in Amazon EMR 5\.x Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)\.

When you launch a cluster, you can choose from multiple release versions of Amazon EMR\. This allows you to test and use application versions that fit your compatibility requirements\. You specify the release version using the *release label*\. Release labels are in the form `emr-x.x.x. For example, emr-5.23.0.`

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

------
#### [ 5\.23\.0 ]<a name="emr-5230-release"></a>

**Amazon EMR Release 5\.23\.0**
+ [Application Versions](#emr-5230-app-versions)
+ [Release Notes](#emr-5230-relnotes)
+ [Component Versions](#emr-5230-components)
+ [Configuration Classifications](#emr-5230-class)

**5\.23\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.23.0.png)

**5\.23\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.23\.0\. Changes are relative to 5\.22\.0\.

Initial release date: April 01, 2019

Last updated date: April 30, 2019

**Upgrades**
+ AWS SDK for Java 1\.11\.519

**New Features**
+ \(April 30, 2019\) With Amazon EMR 5\.23\.0 and later, you can launch a cluster with three master nodes to support high availability of applications like YARN Resource Manager, HDFS Name Node, Spark, Hive, and Ganglia\. The master node is no longer a potential single point of failure with this feature\. If one of the master nodes fails, Amazon EMR automatically fails over to a standby master node and replaces the failed master node with a new one with the same configuration and bootstrap actions\. For more information, see [Plan and Configure Master Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha.html)\.

**Known Issues**
+ Tez UI

  Tez UI does not work on an EMR cluster with multiple master nodes\. 
+ Hue
  + Hue running on Amazon EMR does not support Solr\. Beginning with Amazon EMR release version 5\.20\.0, a misconfiguration issue causes Solr to be enabled and a harmless error message to appear similar to the following:

    `Solr server could not be contacted properly: HTTPConnectionPool('host=ip-xx-xx-xx-xx.ec2.internal', port=1978): Max retries exceeded with url: /solr/admin/info/system?user.name=hue&doAs=administrator&wt=json (Caused by NewConnectionError(': Failed to establish a new connection: [Errno 111] Connection refused',))`

    **To prevent the Solr error message from appearing:**

    1. Connect to the master node command line using SSH\.

    1. Use a text editor to open the `hue.ini` file\. For example:

       `sudo vim /etc/hue/conf/hue.ini`

    1. Search for the term "appblacklist" and modify the line to the following:

       ```
       appblacklist = search
       ```

    1. Save your changes and restart Hue as shown in the following example:

       ```
       sudo stop hue; sudo start hue
       ```

**5\.23\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.8\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.7\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.11\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.2\.0 | EMR S3Select Connector | 
| emrfs | 2\.32\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.7\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.5\-amzn\-3 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.5\-amzn\-3 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.5\-amzn\-3 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.5\-amzn\-3 | HDFS service for tracking file names and block locations\. | 
| hadoop\-hdfs\-journalnode | 2\.8\.5\-amzn\-3 | HDFS service for managing the Hadoop filesystem journal on HA clusters\. | 
| hadoop\-httpfs\-server | 2\.8\.5\-amzn\-3 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.5\-amzn\-3 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.5\-amzn\-3 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.5\-amzn\-3 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.5\-amzn\-3 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.5\-amzn\-3 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.9 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.9 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.9 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.9 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.9 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.4\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.4\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.4\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.4\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.4\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.4\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.4\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.3\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.9\.4 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.3\.1 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.1\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.1\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.1\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.1\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.215 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.215 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.4\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.12\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.1 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.13 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.13 | ZooKeeper command line client\. | 

**5\.23\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.23\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.22\.0 ]<a name="emr-5220-release"></a>

**Amazon EMR Release 5\.22\.0**
+ [Application Versions](#emr-5220-app-versions)
+ [Release Notes](#emr-5220-relnotes)
+ [Component Versions](#emr-5220-components)
+ [Configuration Classifications](#emr-5220-class)

**5\.22\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.22.0.png)

**5\.22\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.22\.0\. Changes are relative to 5\.21\.0\.

**Important**  
Beginning with Amazon EMR release version 5\.22\.0, Amazon EMR uses AWS Signature Version 4 exclusively to authenticate requests to Amazon S3\. Earlier Amazon EMR release versions use AWS Signature Version 2 in some cases, unless the release notes indicate that Signature Version 4 is used exclusively\. For more information, see [Authenticating Requests \(AWS Signature Version 4\)](https://docs.aws.amazon.com/AmazonS3/latest/API/sig-v4-authenticating-requests.html) and [Authenticating Requests \(AWS Signature Version 2\)](https://docs.aws.amazon.com/AmazonS3/latest/API/auth-request-sig-v2.html) in the *Amazon Simple Storage Service Developer Guide*\.

Initial release date: March 20, 2019

**Upgrades**
+ Flink 1\.7\.1
+ HBase 1\.4\.9
+ Oozie 5\.1\.0
+ Phoenix 4\.14\.1
+ Zeppelin 0\.8\.1
+ Connectors and drivers:
  + DynamoDB Connector 4\.8\.0
  + MariaDB Connector 2\.2\.6
  + Amazon Redshift JDBC Driver 1\.2\.20\.1043

**New Features**
+ Modified the default EBS configuration for EC2 instance types with EBS\-only storage\. When you create a cluster using Amazon EMR release version 5\.22\.0 and later, the default amount of EBS storage increases based on the size of the instance\. In addition, we split increased storage across multiple volumes, giving increased IOPS performance\. If you want to use a different EBS instance storage configuration, you can specify it when you create an EMR cluster or add nodes to an existing cluster\. For more information about the amount of storage and number of volumes allocated by default for each instance type, see [Default EBS Storage for Instances](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-storage.html#emr-plan-storage-ebs-storage-default) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Introduced a new configuration property for Spark on YARN, `spark.yarn.executor.memoryOverheadFactor`\. The value of this property is a scale factor that sets the value of memory overhead to a percentage of executor memory, with a minimum of 384 MB\. If memory overhead is set explicitly using `spark.yarn.executor.memoryOverhead`, this property has no effect\. The default value is `0.1875`, representing 18\.75%\. This default for Amazon EMR leaves more space in YARN containers for executor memory overhead than the 10% default set internally by Spark\. The Amazon EMR default of 18\.75% empirically showed fewer memory\-related failures in TPC\-DS benchmarks\.
  + Backported [SPARK\-26316](https://issues.apache.org/jira/browse/SPARK-26316) to improve performance\.

**Known Issues**
+ Hue
  + Hue running on Amazon EMR does not support Solr\. Beginning with Amazon EMR release version 5\.20\.0, a misconfiguration issue causes Solr to be enabled and a harmless error message to appear similar to the following:

    `Solr server could not be contacted properly: HTTPConnectionPool('host=ip-xx-xx-xx-xx.ec2.internal', port=1978): Max retries exceeded with url: /solr/admin/info/system?user.name=hue&doAs=administrator&wt=json (Caused by NewConnectionError(': Failed to establish a new connection: [Errno 111] Connection refused',))`

    **To prevent the Solr error message from appearing:**

    1. Connect to the master node command line using SSH\.

    1. Use a text editor to open the `hue.ini` file\. For example:

       `sudo vim /etc/hue/conf/hue.ini`

    1. Search for the term "appblacklist" and modify the line to the following:

       ```
       appblacklist = search
       ```

    1. Save your changes and restart Hue as shown in the following example:

       ```
       sudo stop hue; sudo start hue
       ```

**5\.22\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.8\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.6\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.11\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.2\.0 | EMR S3Select Connector | 
| emrfs | 2\.31\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.7\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.5\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.5\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.5\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.5\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.5\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.5\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.5\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.5\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.5\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.5\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.9 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.9 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.9 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.9 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.9 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.4\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.4\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.4\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.4\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.4\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.4\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.4\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.3\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.9\.4 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.3\.1 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.1\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.1\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.1\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.1\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.215 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.215 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.4\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.12\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.1 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.13 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.13 | ZooKeeper command line client\. | 

**5\.22\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.22\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.21\.0 ]<a name="emr-5210-release"></a>

**Amazon EMR Release 5\.21\.0**
+ [Application Versions](#emr-5210-app-versions)
+ [Release Notes](#emr-5210-relnotes)
+ [Component Versions](#emr-5210-components)
+ [Configuration Classifications](#emr-5210-class)

**5\.21\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.21.0.png)

**5\.21\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.21\.0\. Changes are relative to 5\.20\.0\.

Initial release date: February 18, 2019

Last updated date: April 3, 2019

**Upgrades**
+ Flink 1\.7\.0
+ Presto 0\.215
+ AWS SDK for Java 1\.11\.479

**New Features**
+ \(April 3, 2019\) With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

**Changes, Enhancements, and Resolved Issues**
+ Zeppelin
  + Backported [ZEPPELIN\-3878](https://issues.apache.org/jira/browse/ZEPPELIN-3878)\.

**Known Issues**
+ Hue
  + Hue running on Amazon EMR does not support Solr\. Beginning with Amazon EMR release version 5\.20\.0, a misconfiguration issue causes Solr to be enabled and a harmless error message to appear similar to the following:

    `Solr server could not be contacted properly: HTTPConnectionPool('host=ip-xx-xx-xx-xx.ec2.internal', port=1978): Max retries exceeded with url: /solr/admin/info/system?user.name=hue&doAs=administrator&wt=json (Caused by NewConnectionError(': Failed to establish a new connection: [Errno 111] Connection refused',))`

    **To prevent the Solr error message from appearing:**

    1. Connect to the master node command line using SSH\.

    1. Use a text editor to open the `hue.ini` file\. For example:

       `sudo vim /etc/hue/conf/hue.ini`

    1. Search for the term "appblacklist" and modify the line to the following:

       ```
       appblacklist = search
       ```

    1. Save your changes and restart Hue as shown in the following example:

       ```
       sudo stop hue; sudo start hue
       ```
+ Tez
  + This issue was fixed in Amazon EMR 5\.22\.0\.

    When you connect to the Tez UI at http://*MasterDNS*:8080/tez\-ui through an SSH connection to the cluster master node, the error "Adapter operation failed \- Timeline server \(ATS\) is out of reach\. Either it is down, or CORS is not enabled" appears, or tasks unexpectedly show N/A\.

    This is caused by the Tez UI making requests to the YARN Timeline Server using `localhost` rather than the host name of the master node\. As a workaround, a script is available to run as a bootstrap action or step\. The script updates the host name in the Tez `configs.env` file\. For more information and the location of the script, see the [Bootstrap Instructions](http://awssupportdatasvcs.com/bootstrap-actions/fix_tez_ui_0-9-1/)\.

**5\.21\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.7\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.5\.1 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.11\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.2\.0 | EMR S3Select Connector | 
| emrfs | 2\.30\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.7\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.5\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.5\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.5\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.5\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.5\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.5\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.5\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.5\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.5\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.5\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.8 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.8 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.8 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.8 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.8 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.4\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.4\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.4\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.4\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.4\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.4\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.4\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.3\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.9\.4 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.3\.1 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.215 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.215 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.4\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.12\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.1 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.13 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.13 | ZooKeeper command line client\. | 

**5\.21\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.21\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.20\.0 ]<a name="emr-5200-release"></a>

**Amazon EMR Release 5\.20\.0**
+ [Application Versions](#emr-5200-app-versions)
+ [Release Notes](#emr-5200-relnotes)
+ [Component Versions](#emr-5200-components)
+ [Configuration Classifications](#emr-5200-class)

**5\.20\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.20.0.png)

**5\.20\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.20\.0\. Changes are relative to 5\.19\.0\.

Initial release date: December 18, 2018

Last updated date: January 22, 2019

**Upgrades**
+ Flink 1\.6\.2
+ HBase 1\.4\.8
+ Hive 2\.3\.4
+ Hue 4\.3\.0
+ MXNet 1\.3\.1
+ Presto 0\.214
+ Spark 2\.4\.0
+ TensorFlow 1\.12\.0
+ Tez 0\.9\.1
+ AWS SDK for Java 1\.11\.461

**New Features**
+ \(January 22, 2019\) Kerberos in Amazon EMR has been improved to support authenticating principals from an external KDC\. This centralizes principal management because multiple clusters can share a single, external KDC\. In addition, the external KDC can have a cross\-realm trust with an Active Directory domain\. This allows all clusters to authenticate principals from Active Directory\. For more information, see [Use Kerberos Authentication](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ Default Amazon Linux AMI for Amazon EMR
  + Python3 package was upgraded from python 3\.4 to 3\.6\.
+ The EMRFS S3\-optimized committer 
  + The EMRFS S3\-optimized committer is now enabled by default, which improves write performance\. For more information, see [Using the EMRFS S3\-optimized Committer](emr-spark-s3-optimized-committer.md)\.
+ Hive
  + Backported [HIVE\-16686](https://issues.apache.org/jira/browse/HIVE-16686)\.
+ Glue with Spark and Hive
  + In EMR 5\.20\.0 or later, parallel partition pruning is enabled automatically for Spark and Hive when AWS Glue Data Catalog is used as the metastore\. This change significantly reduces query planning time by executing multiple requests in parallel to retrieve partitions\. The total number of segments that can be executed concurrently range between 1 and 10\. The default value is 5, which is a recommended setting\. You can change it by specifying the property `aws.glue.partition.num.segments` in `hive-site` configuration classification\. If throttling occurs, you can turn off the feature by changing the value to 1\. For more information, see [AWS Glue Segment Structure](https://docs.aws.amazon.com/glue/latest/dg/aws-glue-api-catalog-partitions.html#aws-glue-api-catalog-partitions-Segment)\.

**Known Issues**
+ Hue
  + Hue running on Amazon EMR does not support Solr\. Beginning with Amazon EMR release version 5\.20\.0, a misconfiguration issue causes Solr to be enabled and a harmless error message to appear similar to the following:

    `Solr server could not be contacted properly: HTTPConnectionPool('host=ip-xx-xx-xx-xx.ec2.internal', port=1978): Max retries exceeded with url: /solr/admin/info/system?user.name=hue&doAs=administrator&wt=json (Caused by NewConnectionError(': Failed to establish a new connection: [Errno 111] Connection refused',))`

    **To prevent the Solr error message from appearing:**

    1. Connect to the master node command line using SSH\.

    1. Use a text editor to open the `hue.ini` file\. For example:

       `sudo vim /etc/hue/conf/hue.ini`

    1. Search for the term "appblacklist" and modify the line to the following:

       ```
       appblacklist = search
       ```

    1. Save your changes and restart Hue as shown in the following example:

       ```
       sudo stop hue; sudo start hue
       ```
+ Tez
  + This issue was fixed in Amazon EMR 5\.22\.0\.

    When you connect to the Tez UI at http://*MasterDNS*:8080/tez\-ui through an SSH connection to the cluster master node, the error "Adapter operation failed \- Timeline server \(ATS\) is out of reach\. Either it is down, or CORS is not enabled" appears, or tasks unexpectedly show N/A\.

    This is caused by the Tez UI making requests to the YARN Timeline Server using `localhost` rather than the host name of the master node\. As a workaround, a script is available to run as a bootstrap action or step\. The script updates the host name in the Tez `configs.env` file\. For more information and the location of the script, see the [Bootstrap Instructions](http://awssupportdatasvcs.com/bootstrap-actions/fix_tez_ui_0-9-1/)\.

**5\.20\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.7\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.5\.1 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.2\.0 | EMR S3Select Connector | 
| emrfs | 2\.29\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.6\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.5\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.5\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.5\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.5\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.5\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.5\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.5\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.5\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.5\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.5\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.8 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.8 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.8 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.8 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.8 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.4\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.4\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.4\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.4\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.4\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.4\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.4\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.3\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.9\.4 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.3\.1 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.214 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.214 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.4\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.12\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.1 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.13 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.13 | ZooKeeper command line client\. | 

**5\.20\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.20\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.19\.0 ]<a name="emr-5190-release"></a>

**Amazon EMR Release 5\.19\.0**
+ [Application Versions](#emr-5190-app-versions)
+ [Release Notes](#emr-5190-relnotes)
+ [Component Versions](#emr-5190-components)
+ [Configuration Classifications](#emr-5190-class)

**5\.19\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.19.0.png)

**5\.19\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.19\.0\. Changes are relative to 5\.18\.0\.

Initial release date: November 7, 2018

Last updated date: November 19, 2018

**Upgrades**
+ Hadoop 2\.8\.5
+ Flink 1\.6\.1
+ JupyterHub 0\.9\.4
+ MXNet 1\.3\.0
+ Presto 0\.212
+ TensorFlow 1\.11\.0
+ Zookeeper 3\.4\.13
+ AWS SDK for Java 1\.11\.433

**New Features**
+ \(Nov\. 19, 2018\) EMR Notebooks is a managed environment based on Jupyter Notebook\. It supports Spark magic kernels for PySpark, Spark SQL, Spark R, and Scala\. EMR Notebooks can be used with clusters created using Amazon EMR release version 5\.18\.0 and later\. For more information, see [Using EMR Notebooks](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks.html) in the *Amazon EMR Management Guide*\.
+ The EMRFS S3\-optimized committer is available when writing Parquet files using Spark and EMRFS\. This committer improves write performance\. For more information, see [Using the EMRFS S3\-optimized Committer](emr-spark-s3-optimized-committer.md)\.

**Changes, Enhancements, and Resolved Issues**
+ YARN
  + Modified the logic that limits the application master process to running on core nodes\. This functionality now uses the YARN node labels feature and properties in the `yarn-site` and `capacity-scheduler` configuration classifications\. For information, see [https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-instances-guidelines.html#emr-plan-spot-YARN.](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-instances-guidelines.html#emr-plan-spot-YARN.)
+ Default Amazon Linux AMI for Amazon EMR
  + `ruby18`, `php56`, and `gcc48` are no longer installed by default\. These can be installed if desired using `yum`\.
  + The aws\-java\-sdk ruby gem is no longer installed by default\. It can be installed using `gem install aws-java-sdk`, if desired\. Specific components can also be installed\. For example, `gem install aws-java-sdk-s3`\.

**Known Issues**
+ **EMR Notebooks**—In some circumstances, with multiple notebook editors open, the notebook editor may appear unable to connect to the cluster\. If this happens, clear browser cookies and then reopen notebook editors\.

**5\.19\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.7\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.5\.1 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.1\.0 | EMR S3Select Connector | 
| emrfs | 2\.28\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.6\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.5\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.5\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.5\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.5\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.5\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.5\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.5\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.5\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.5\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.5\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.7 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.7 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.7 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.7 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.7 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.3\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.3\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.3\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.3\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 2\.3\.3\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.3\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.3\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.2\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.9\.4 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.3\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.212 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.212 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.11\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.13 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.13 | ZooKeeper command line client\. | 

**5\.19\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.19\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.18\.0 ]<a name="emr-5180-release"></a>

**Amazon EMR Release 5\.18\.0**
+ [Application Versions](#emr-5180-app-versions)
+ [Release Notes](#emr-5180-relnotes)
+ [Component Versions](#emr-5180-components)
+ [Configuration Classifications](#emr-5180-class)

**5\.18\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.18.0.png)

**5\.18\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.18\.0\. Changes are relative to 5\.17\.0\.

Initial release date: October 24, 2018

**Upgrades**
+ Flink 1\.6\.0
+ HBase 1\.4\.7
+ Presto 0\.210
+ Spark 2\.3\.2
+ Zeppelin 0\.8\.0

**New Features**
+ Beginning with Amazon EMR 5\.18\.0, you can use the Amazon EMR artifact repository to build your job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions\. For more information, see [Checking Dependencies Using the Amazon EMR Artifact Repository](emr-artifact-repository.md)\.

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Added support for S3 Select\. For more information, see [Using S3 Select with Hive to Improve Performance](emr-hive-s3select.md)\.
+ Presto
  + Added support for [S3 Select](https://aws.amazon.com/blogs/aws/s3-glacier-select/) Pushdown\. For more information, see [Using S3 Select Pushdown with Presto to Improve Performance](emr-presto-s3select.md)\.
+ Spark
  + The default log4j configuration for Spark has been changed to roll container logs hourly for Spark streaming jobs\. This helps prevent the deletion of logs for long\-running Spark streaming jobs\.

**5\.18\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.1\.3 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.6\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.5\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.1\.0 | EMR S3Select Connector | 
| emrfs | 2\.27\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.6\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.4\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.4\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.4\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.4\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.4\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.4\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.4\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.4\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.4\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.4\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.7 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.7 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.7 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.7 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.7 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.3\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.3\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.3\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.3\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 2\.3\.3\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.3\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.3\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.2\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.2\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.210 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.210 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.9\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.8\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.12 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.12 | ZooKeeper command line client\. | 

**5\.18\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.18\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.17\.0 ]<a name="emr-5170-release"></a>

**Amazon EMR Release 5\.17\.0**
+ [Application Versions](#emr-5170-app-versions)
+ [Release Notes](#emr-5170-relnotes)
+ [Component Versions](#emr-5170-components)
+ [Configuration Classifications](#emr-5170-class)

**5\.17\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.17.0.png)

**5\.17\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.17\.0\. Changes are relative to 5\.16\.0\.

Initial release date: August 30, 2018

**Upgrades**
+ Flink 1\.5\.2
+ HBase 1\.4\.6
+ Presto 0\.206

**New Features**
+ Added support for Tensorflow\. For more information, see [TensorFlow](emr-tensorflow.md)\.

**Changes, Enhancements, and Resolved Issues**
+ JupyterHub
  + Added support for notebook persistence in Amazon S3\. For more information, see [Configuring Persistence for Notebooks in Amazon S3](emr-jupyterhub-s3.md)\.
+ Spark
  + Added support for [S3 Select](http://aws.amazon.com/blogs/aws/s3-glacier-select/)\. For more information, see [Using S3 Select with Spark to Improve Query Performance](emr-spark-s3select.md)\.

**Known Issues**
+ When you create a kerberized cluster with Livy installed, Livy fails with an error that simple authentication is not enabled\. Rebooting the Livy server resolves the issue\. As a workaround, add a step during cluster creation that runs `sudo restart livy-server` on the master node\.
+ If you use a custom Amazon Linux AMI based on an Amazon Linux AMI with a creation date of 2018\-08\-11, the Oozie server fails to start\. If you use Oozie, create a custom AMI based on an Amazon Linux AMI ID with a different creation date\. You can use the following AWS CLI command to return a list of Image IDs for all HVM Amazon Linux AMIs with a 2018\.03 version, along with the release date, so that you can choose an appropriate Amazon Linux AMI as your base\. Replace MyRegion with your region identifier, such as us\-west\-2\.

  ```
  aws ec2 --region MyRegion describe-images --owner amazon --query 'Images[?Name!=`null`]|[?starts_with(Name, `amzn-ami-hvm-2018.03`) == `true`].[CreationDate,ImageId,Name]' --output text | sort -rk1
  ```

**5\.17\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.1\.3 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.6\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.5\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.0\.0 | EMR S3Select Connector | 
| emrfs | 2\.26\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.5\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.4\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.4\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.4\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.4\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.4\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.4\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.4\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.4\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.4\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.4\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.6 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.6 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.6 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.6 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.6 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.3\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.3\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.3\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.3\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.3\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.3\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.3\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.2\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.2\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.206 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.206 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 1\.9\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.12 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.12 | ZooKeeper command line client\. | 

**5\.17\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.17\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.16\.0 ]<a name="emr-5160-release"></a>

**Amazon EMR Release 5\.16\.0**
+ [Application Versions](#emr-5160-app-versions)
+ [Release Notes](#emr-5160-relnotes)
+ [Component Versions](#emr-5160-components)
+ [Configuration Classifications](#emr-5160-class)

**5\.16\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.16.0.png)

**5\.16\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.16\.0\. Changes are relative to 5\.15\.0\.

Initial release date: July 19, 2018

**Upgrades**
+ Hadoop 2\.8\.4
+ Flink 1\.5\.0
+ Livy 0\.5\.0
+ MXNet 1\.2\.0
+ Phoenix 4\.14\.0
+ Presto 0\.203
+ Spark 2\.3\.1
+ AWS SDK for Java 1\.11\.336
+ CUDA 9\.2
+ Redshift JDBC Driver 1\.2\.15\.1025

**Changes, Enhancements, and Resolved Issues**
+ HBase
  + Backported [HBASE\-20723](https://issues.apache.org/jira/browse/HBASE-20723)
+ Presto
  + Configuration changes to support LDAP authentication\. For more information, see [Using LDAP Authentication for Presto on Amazon EMR](emr-presto-ldap.md)\.
+ Spark
  + Apache Spark version 2\.3\.1, available beginning with Amazon EMR release version 5\.16\.0, addresses [CVE\-2018\-8024](https://nvd.nist.gov/vuln/detail/CVE-2018-8024) and [CVE\-2018\-1334](https://nvd.nist.gov/vuln/detail/CVE-2018-1334)\. We recommend that you migrate earlier versions of Spark to Spark version 2\.3\.1 or later\.

**Known Issues**
+ This release version does not support the c1\.medium or m1\.small instance types\. Clusters using either of these instance types fail to start\. As a workaround, specify a different instance type or use a different release version\.
+ When you create a kerberized cluster with Livy installed, Livy fails with an error that simple authentication is not enabled\. Rebooting the Livy server resolves the issue\. As a workaround, add a step during cluster creation that runs `sudo restart livy-server` on the master node\.

**5\.16\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.1\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.6\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.25\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.5\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.4\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.4\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.4\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.4\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.4\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.4\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.4\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.4\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.4\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.4\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.4 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.4 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.4 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.4 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.4 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.3\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.3\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.3\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.3\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.3\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.3\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.3\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.2\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.5\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.2\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.203 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.203 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.12 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.12 | ZooKeeper command line client\. | 

**5\.16\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.16\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.15\.0 ]<a name="emr-5150-release"></a>

**Amazon EMR Release 5\.15\.0**
+ [Application Versions](#emr-5150-app-versions)
+ [Release Notes](#emr-5150-relnotes)
+ [Component Versions](#emr-5150-components)
+ [Configuration Classifications](#emr-5150-class)

**5\.15\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.15.0.png)

**5\.15\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.15\.0\. Changes are relative to 5\.14\.0\.

Initial release date: June 21, 2018

**Upgrades**
+ Upgraded HBase to 1\.4\.4
+ Upgraded Hive to 2\.3\.3
+ Upgraded Hue to 4\.2\.0
+ Upgraded Oozie to 5\.0\.0
+ Upgraded Zookeeper to 3\.4\.12
+ Upgraded AWS SDK to 1\.11\.333

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Backported [HIVE\-18069](https://issues.apache.org/jira/browse/HIVE-18069)
+ Hue
  + Updated Hue to correctly authenticate with Livy when Kerberos is enabled\. Livy is now supported when using Kerberos with Amazon EMR\.
+ JupyterHub
  + Updated JupyterHub so that Amazon EMR installs LDAP client libraries by default\.
  + Fixed an error in the script that generates self\-signed certificates\. For more information about the issue, see [Release Notes](#emr-5140-relnotes)

**Known Issues**
+ This release version does not support the c1\.medium or m1\.small instance types\. Clusters using either of these instance types fail to start\. As a workaround, specify a different instance type or use a different release version\.

**5\.15\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.24\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.4 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.4 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.4 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.4 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.4 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.3\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.3\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.3\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.3\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.3\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.3\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.3\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.2\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.1\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.0\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.0\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.194 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.194 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.12 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.12 | ZooKeeper command line client\. | 

**5\.15\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.15\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.14\.x ]<a name="emr-514x-releases"></a>

There are multiple releases within the 5\.14 series\. Choose a link below to see information for a specific release within this tab\.

**[5.14.1](#emr-5141-release) \(Latest\) \| [5.14.0](#emr-5140-release)**

**Amazon EMR Release 5\.14\.1**
+ [Application Versions](#emr-5141-app-versions)
+ [Release Notes](#emr-5141-relnotes)
+ [Component Versions](#emr-5141-components)
+ [Configuration Classifications](#emr-5141-class)

**Release 5\.14\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.14.1.png)

**Release 5\.14\.1 Release Notes**

The following release notes include information for Amazon EMR release version 5\.14\.1\. Changes are relative to 5\.14\.0\.

Initial release date: October 17, 2018

Updated the default AMI for Amazon EMR to address potential security vulnerabilities\.

**Release 5\.14\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.23\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.1\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.194 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.194 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.14\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.14\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.14\.0**
+ [Application Versions](#emr-5140-app-versions)
+ [Release Notes](#emr-5140-relnotes)
+ [Component Versions](#emr-5140-components)
+ [Configuration Classifications](#emr-5140-class)

**Release 5\.14\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.14.0.png)

**Release 5\.14\.0 Release Notes**

The following release notes include information for Amazon EMR release version 5\.14\.0\. Changes are relative to 5\.13\.0\.

Initial release date: June 4, 2018

**Upgrades**
+ Upgraded Apache Flink to 1\.4\.2
+ Upgraded Apache MXnet to 1\.1\.0
+ Upgraded Apache Sqoop to 1\.4\.7

**New Features**
+ Added JupyterHub support\. For more information, see [JupyterHub](emr-jupyterhub.md)\.

**Changes, Enhancements, and Resolved Issues**
+ EMRFS
  + The userAgent string in requests to Amazon S3 has been updated to contain the user and group information of the invoking principal\. This can be used with AWS CloudTrail logs for more comprehensive request tracking\.
+ HBase
  +  Included [HBASE\-20447](https://issues.apache.org/jira/browse/HBASE-20447), which addresses an issue that could cause cache issues, especially with split regions\. 
+ MXnet
  + Added OpenCV libraries\.
+ Spark
  + When Spark writes Parquet files to an Amazon S3 location using EMRFS, the FileOutputCommitter algorithm has been updated to use version 2 instead of version 1\. This reduces the number of renames, which improves application performance\. This change does not affect: 
    + Applications other than Spark\. 
    + Applications that write to other file systems, such as HDFS \(which still use version 1 of FileOutputCommitter\)\.
    + Applications that use other output formats, such as text or csv, that already use EMRFS direct write\.

**Known Issues**
+ JupyterHub
  + Using configuration classifications to set up JupyterHub and individual Jupyter notebooks when you create a cluster is not supported\. Edit the jupyterhub\_config\.py file and jupyter\_notebook\_config\.py files for each user manually\. For more information, see [Configuring JupyterHub](emr-jupyterhub-configure.md)\.
  + JupyterHub fails to start on clusters within a private subnet, failing with the message `Error: ENOENT: no such file or directory, open '/etc/jupyter/conf/server.crt' `\. This is caused by an error in the script that generates self\-signed certificates\. Use the following workaround to generate self\-signed certificates\. All commands are executed while connected to the master node\.

    1. Copy the certificate generation script from the container to the master node:

       ```
       sudo docker cp jupyterhub:/tmp/gen_self_signed_cert.sh ./
       ```

    1. Use a text editor to change line 23 to change public hostname to local hostname as shown below:

       ```
       local hostname=$(curl -s $EC2_METADATA_SERVICE_URI/local-hostname)
       ```

    1. Run the script to generate self\-signed certificates:

       ```
       sudo bash ./gen_self_signed_cert.sh
       ```

    1. Move the certificate files that the script generates to the `/etc/jupyter/conf/` directory:

       ```
       sudo mv /tmp/server.crt /tmp/server.key /etc/jupyter/conf/
       ```

    You can `tail` the `jupyter.log` file to verify that JupyterHub restarted and is returning a 200 response code\. For example:

    ```
    tail -f /var/log/jupyter/jupyter.log
    ```

    This should return a response similar to the following:

    ```
    # [I 2018-06-14 18:56:51.356 JupyterHub app:1581] JupyterHub is now running at https://:9443/
    # 19:01:51.359 - info: [ConfigProxy] 200 GET /api/routes
    ```

**Release 5\.14\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.23\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 0\.8\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.1\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.194 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.194 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.14\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.14\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.13\.0 ]<a name="emr-5130-release"></a>

**Amazon EMR Release 5\.13\.0**
+ [Application Versions](#emr-5130-app-versions)
+ [Release Notes](#emr-5130-relnotes)
+ [Component Versions](#emr-5130-components)
+ [Configuration Classifications](#emr-5130-class)

**5\.13\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.13.0.png)

**5\.13\.0 Release Notes**

The following release notes include information for the Amazon EMR release version 5\.13\.0\. Changes are relative to 5\.12\.0\.

**Upgrades**
+ Upgraded Spark to 2\.3\.0
+ Upgraded HBase to 1\.4\.2
+ Upgraded Presto to 0\.194
+ Upgraded AWS Java SDK to 1\.11\.297

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Backported [HIVE\-15436](https://issues.apache.org/jira/browse/HIVE-15436)\. Enhanced Hive APIs to return only views\.

**Known Issues**
+ MXNet does not currently have OpenCV libraries\.

**5\.13\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.10\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.22\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.0\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.194 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.194 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.1 | The R Project for Statistical Computing | 
| spark\-client | 2\.3\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.3\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.3\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.3\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**5\.13\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.13\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.12\.x ]<a name="emr-512x-releases"></a>

There are multiple releases within the 5\.12 series\. Choose a link below to see information for a specific release within this tab\.

**[5.12.2](#emr-5122-release) \| [5.12.1](#emr-5121-release) \| [5.12.0](#emr-5120-release)**

**Amazon EMR Release 5\.12\.2**
+ [Application Versions](#emr-5122-app-versions)
+ [Release Notes](#emr-5122-relnotes)
+ [Component Versions](#emr-5122-components)
+ [Configuration Classifications](#emr-5122-class)

**Release 5\.12\.2 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.12.2.png)

**Release 5\.12\.2 Release Notes**

The following release notes include information for Amazon EMR release version 5\.12\.2\. Changes are relative to 5\.12\.1\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

**Release 5\.12\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.9\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.21\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.0\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.188 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.188 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.12\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.12\.2 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.12\.1**
+ [Application Versions](#emr-5121-app-versions)
+ [Release Notes](#emr-5121-relnotes)
+ [Component Versions](#emr-5121-components)
+ [Configuration Classifications](#emr-5121-class)

**Release 5\.12\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.12.1.png)

**Release 5\.12\.1 Release Notes**

The following release notes include information for Amazon EMR release version 5\.12\.1\. Changes are relative to 5\.12\.0\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

**Release 5\.12\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.9\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.21\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.0\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.188 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.188 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.12\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.12\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.12\.0**
+ [Application Versions](#emr-5120-app-versions)
+ [Release Notes](#emr-5120-relnotes)
+ [Component Versions](#emr-5120-components)
+ [Configuration Classifications](#emr-5120-class)

**Release 5\.12\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.12.0.png)

**Release 5\.12\.0 Release Notes**

The following release notes include information for the Amazon EMR release version 5\.12\.0\. Changes are relative to 5\.11\.1\.

**Upgrades**
+ AWS SDK for Java 1\.11\.238 ⇒ 1\.11\.267\. For more information, see the [AWS SDK for Java Change Log](https://github.com/aws/aws-sdk-java/blob/master/CHANGELOG.md) on GitHub\.
+ Hadoop 2\.7\.3 ⇒ 2\.8\.3\. For more information, see [Apache Hadoop Releases](http://hadoop.apache.org/releases.html)\.
+ Flink 1\.3\.2 ⇒ 1\.4\.0\. For more information, see the [Apache Flink 1\.4\.0 Release Announcement](https://flink.apache.org/news/2017/12/12/release-1.4.0.html)\.
+ HBase 1\.3\.1 ⇒ 1\.4\.0\. For more information, see the [HBase Release Announcement](http://mail-archives.apache.org/mod_mbox/www-announce/201712.mbox/%3CCA+RK=_AU+tB=7SU1HRbeKVEd-sKA5WcJo3oa43vQ6PMB3L9pgQ@mail.gmail.com%3E)\.
+ Hue 4\.0\.1 ⇒ 4\.1\.0\. For more information, see the [Release Notes](http://cloudera.github.io/hue/latest/release-notes/release-notes-4.1.0.html)\.
+ MxNet 0\.12\.0 ⇒ 1\.0\.0\. For more information, see the [MXNet Change Log](https://github.com/apache/incubator-mxnet/releases/tag/1.0.0) on GitHub\.
+ Presto 0\.187 ⇒ 0\.188\. For more information, see the [Release Notes](https://prestodb.io/docs/current/release/release-0.188.html)\.

**Changes, Enhancements, and Resolved Issues**
+ **Hadoop**
  + The `yarn.resourcemanager.decommissioning.timeout` property has changed to `yarn.resourcemanager.nodemanager-graceful-decommission-timeout-secs`\. You can use this property to customize cluster scale\-down\. For more information, see [Cluster Scale\-Down](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scaledown-behavior.html) in the *Amazon EMR Management Guide*\.
  + The Hadoop CLI added the `-d` option to the `cp` \(copy\) command, which specifies direct copy\. You can use this to avoid creating an intermediary `.COPYING` file, which makes copying data between Amazon S3 faster\. For more information, see [HADOOP\-12384](https://issues.apache.org/jira/browse/HADOOP-12384)\.
+ **Pig**
  + Added the `pig-env` configuration classification, which simplifies the configuration of Pig environment properties\. For more information, see [Configuring Applications](emr-configure-apps.md)\.
+ **Presto**
  + Added the `presto-connector-redshift` configuration classification, which you can use to configure values in the Presto `redshift.properties` configuration file\. For more information, see [Redshift Connector](https://prestodb.io/docs/current/connector/redshift.html) in Presto documentation, and [Configuring Applications](emr-configure-apps.md)\.
  + Presto support for EMRFS has been added and is the default configuration\. Earlier Amazon EMR release versions used PrestoS3FileSystem, which was the only option\. For more information, see [EMRFS and PrestoS3FileSystem Configuration](emr-presto-considerations.md#emr-presto-prestos3)\.
**Note**  
A configuration issue can cause Presto errors when querying underlying data in Amazon S3 with Amazon EMR release version 5\.12\.0\. This is because Presto fails to pick up configuration classification values from `emrfs-site.xml`\. As a workaround, create an `emrfs` subdirectory under `usr/lib/presto/plugin/hive-hadoop2/`, create a symlink in `usr/lib/presto/plugin/hive-hadoop2/emrfs` to the existing `/usr/share/aws/emr/emrfs/conf/emrfs-site.xml` file, and then restart the presto\-server process \(`sudo presto-server stop` followed by `sudo presto-server start`\)\.
+ **Spark**
  + Backported [SPARK\-22036: BigDecimal multiplication sometimes returns null](https://issues.apache.org/jira/browse/SPARK-22036)\.

**Known Issues**
+ MXNet does not include OpenCV libraries\.
+ SparkR is not available for clusters created using a custom AMI because R is not installed by default on cluster nodes\.

**Release 5\.12\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.9\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.21\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.4\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.8\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.8\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.8\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.8\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.8\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.8\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.8\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.8\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.8\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.8\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-1 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-1 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-1 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-1 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-1 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.1\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.0\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.1\.85 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.13\.0\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.13\.0\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.188 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.188 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.12\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.12\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-env | Change values in the Pig environment\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.11\.x ]

There are multiple releases within the 5\.11 series\. Choose a link below to see information for a specific release within this tab\.

**[5.11.2](#emr-5112-release) \| [5.11.1](#emr-5111-release) \| [5.11.0](#emr-5110-release)**

**Amazon EMR Release 5\.11\.2**
+ [Application Versions](#emr-5112-app-versions)
+ [Release Notes](#emr-5112-relnotes)
+ [Component Versions](#emr-5112-components)
+ [Configuration Classifications](#emr-5112-class)

**Release 5\.11\.2 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.11.2.png)

**Release 5\.11\.2 Release Notes**

The following release notes include information for Amazon EMR release version 5\.11\.2\. Changes are relative to 5\.11\.1\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

**Release 5\.11\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.8\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.20\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-6 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-6 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-6 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-6 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-6 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-6 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-6 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-6 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-6 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-6 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.0\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 0\.12\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.0\.176 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.187 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.187 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.11\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.11\.2 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.11\.1**
+ [Application Versions](#emr-5111-app-versions)
+ [Release Notes](#emr-5111-relnotes)
+ [Component Versions](#emr-5111-components)
+ [Configuration Classifications](#emr-5111-class)

**Release 5\.11\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.11.1.png)

**Release 5\.11\.1 Release Notes**

The following release notes include information for the Amazon EMR 5\.11\.1 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Initial release date: January 22, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

**Release 5\.11\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.8\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.20\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-6 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-6 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-6 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-6 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-6 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-6 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-6 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-6 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-6 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-6 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.0\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 0\.12\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.0\.176 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.187 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.187 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.11\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.11\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.11\.0**
+ [Application Versions](#emr-5110-app-versions)
+ [Release Notes](#emr-5110-relnotes)
+ [Component Versions](#emr-5110-components)
+ [Configuration Classifications](#emr-5110-class)

**Release 5\.11\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.11.0.png)

**Release 5\.11\.0 Release Notes**

The following release notes include information for the Amazon EMR release version 5\.11\.0\. Changes are relative to 5\.10\.0\.

**Upgrades**
+ Hive 2\.3\.2
+ Spark 2\.2\.1
+ SDK for Java 1\.11\.238

**New Features**
+ Spark
  + Added `spark.decommissioning.timeout.threshold` setting, which improves Spark decommissioning behavior when using Spot Instances\. For more information, see [Configuring Node Decommissioning Behavior](emr-spark-configure.md#spark-decommissioning)\.
  + Added the `aws-sagemaker-spark-sdk` component to Spark, which installs Amazon SageMaker Spark and associated dependencies for Spark integration with [Amazon SageMaker](https://aws.amazon.com/sagemaker/)\. You can use Amazon SageMaker Spark to construct Spark machine learning \(ML\) pipelines using Amazon SageMaker stages\. For more information, see the [SageMaker Spark Readme](https://github.com/aws/sagemaker-spark/blob/master/README.md) on GitHub and [Using Apache Spark with Amazon SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/apache-spark.html) in the *Amazon SageMaker Developer Guide*\.

**Known Issues**
+ MXNet does not include OpenCV libraries\.
+ Hive 2\.3\.2 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

**Release 5\.11\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.8\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.20\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-6 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-6 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-6 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-6 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-6 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-6 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-6 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-6 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-6 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-6 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.2\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.2\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.2\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.2\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.2\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.2\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.2\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.0\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 0\.12\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.0\.176 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.187 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.187 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.11\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.11\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.10\.0 ]

**Amazon EMR Release 5\.10\.0**
+ [Application Versions](#emr-5100-app-versions)
+ [Release Notes](#emr-5100-relnotes)
+ [Component Versions](#emr-5100-components)
+ [Configuration Classifications](#emr-5100-class)

**Release 5\.10\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.10.0.png)

**Release 5\.10\.0 Release Notes**

The following release notes include information for the Amazon EMR version 5\.10\.0 release\. Changes are relative to the Amazon EMR 5\.9\.0 release\.

**Upgrades**
+ AWS SDK for Java 1\.11\.221
+ Hive 2\.3\.1
+ Presto 0\.187

**New Features**
+ Added support for Kerberos authentication\. For more information, see [Use Kerberos Authentication](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html) in the *Amazon EMR Management Guide*
+ Added support for IAM roles for EMRFS\. For more information, see [Configure IAM Roles for EMRFS Requests to Amazon S3](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-iam-role.html) in the *Amazon EMR Management Guide*
+ Added support for GPU\-based P2 and P3 instance types\. For more information, see [Amazon EC2 P2 Instances](https://aws.amazon.com/ec2/instance-types/p2/) and [Amazon EC2 P3 Instances](https://aws.amazon.com/ec2/instance-types/p3/)\. NVIDIA driver 384\.81 and CUDA driver 9\.0\.176 are installed on these instance types by default\.
+ Added support for [Apache MXNet](emr-mxnet.md)\.

**Changes, Enhancements, and Resolved Issues**
+ Presto
  + Added support for using the AWS Glue Data Catalog as the default Hive metastore\. For more information, see [Using Presto with the AWS Glue Data Catalog](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-presto.html#emr-presto-glue)\.
  + Added support for [geospatial functions](https://prestodb.io/docs/current/functions/geospatial.html)\.
  + Added [spill to disk](https://prestodb.io/docs/current/admin/spill.html) support for joins\.
  + Added support for the [Redshift connector](https://prestodb.io/docs/current/connector/redshift.html)\.
+ Spark
  + Backported [SPARK\-20640](https://issues.apache.org/jira/browse/SPARK-20640), which makes the rpc timeout and the retries for shuffle registration values configurable using `spark.shuffle.registration.timeout` and `spark.shuffle.registration.maxAttempts` properties\.
  + Backported [SPARK\-21549](https://issues.apache.org/jira/browse/SPARK-21549), which corrects an error that occurs when writing custom OutputFormat to non\-HDFS locations\.
+ Backported [Hadoop\-13270](https://issues.apache.org/jira/browse/HADOOP-13270)
+ The Numpy, Scipy, and Matplotlib libraries have been removed from the base Amazon EMR AMI\. If these libraries are required for your application, they are available in the application repository, so you can use a bootstrap action to install them on all nodes using `yum install`\.
+ The Amazon EMR base AMI no longer has application RPM packages included, so the RPM packages are no longer present on cluster nodes\. Custom AMIs and the Amazon EMR base AMI now reference the RPM package repository in Amazon S3\.
+ Because of the introduction of per\-second billing in Amazon EC2, the default **Scale down behavior** is now **Terminate at task completion** rather than **Terminate at instance hour**\. For more information, see [Configure Cluster Scale\-Down](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scaledown-behavior.html)\.

**Known Issues**
+ MXNet does not include OpenCV libraries\.
+ Hive 2\.3\.1 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

**Release 5\.10\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.5\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.7\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.20\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-5 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-5 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-5 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-5 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-5 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-5 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-5 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-5 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-5 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-5 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.0\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 0\.12\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| nvidia\-cuda | 9\.0\.176 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.187 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.187 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.3 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.10\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.10\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.9\.0 ]

**Amazon EMR Release 5\.9\.0**
+ [Application Versions](#emr-590-app-versions)
+ [Release Notes](#emr-590-relnotes)
+ [Component Versions](#emr-590-components)
+ [Configuration Classifications](#emr-590-class)

**Release 5\.9\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Livy](https://livy.incubator.apache.org/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.9.0.png)

**Release 5\.9\.0 Release Notes**

The following release notes include information for the Amazon EMR version 5\.9\.0 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Release date: October 5, 2017

Latest feature update: October 12, 2017

**Upgrades**
+ AWS SDK for Java version 1\.11\.183
+ Flink 1\.3\.2
+ Hue 4\.0\.1
+ Pig 0\.17\.0
+ Presto 0\.184

**New Features**
+ Added Livy support \(version 0\.4\.0\-incubating\)\. For more information, see [Apache Livy](emr-livy.md)\.
+ Added support for Hue Notebook for Spark\.
+ Added support for i3\-series Amazon EC2 instances \(October 12, 2017\)\.

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Added a new set of features that help ensure Spark handles node termination because of a manual resize or an automatic scaling policy request more gracefully\. For more information, see [Configuring Node Decommissioning Behavior](emr-spark-configure.md#spark-decommissioning)\.
  + SSL is used instead of 3DES for in\-transit encryption for the block transfer service, which enhances performance when using Amazon EC2 instance types with AES\-NI\.
  + Backported [SPARK\-21494](https://issues.apache.org/jira/browse/SPARK-21494)\.
+ Zeppelin
  + Backported [ZEPPELIN\-2377](https://issues.apache.org/jira/browse/ZEPPELIN-2377)\.
+ HBase
  + Added patch [HBASE\-18533](https://issues.apache.org/jira/browse/HBASE-18533), which allows additional values for HBase BucketCache configuration using the `hbase-site` configuration classification\.
+ Hue
  + Added AWS Glue Data Catalog support for the Hive query editor in Hue\.
  + By default, superusers in Hue can access all files that Amazon EMR IAM roles are allowed to access\. Newly created users do not automatically have permissions to access the Amazon S3 filebrowser and must have the `filebrowser.s3_access` permissions enabled for their group\.
+ Resolved an issue that caused underlying JSON data created using AWS Glue Data Catalog to be inaccessible\.

**Known Issues**
+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.
+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

**Release 5\.9\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.4\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.7\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.19\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.2 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-4 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-4 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-4 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-4 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-4 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-4 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-4 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-4 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-4 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-4 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.0\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.0\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 4\.0\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| livy\-server | 0\.4\.0\-incubating | REST interface for interacting with Apache Spark | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.184 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.184 | Service for executing pieces of a query\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| spark\-client | 2\.2\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.9\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.9\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | 
| livy\-env | Change values in the Livy environment\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.8\.x ]

There are multiple releases within the 5\.8 series\. Choose a link below to see information for a specific release within this tab\.

**[5.8.2](#emr-582-release) \| [5.8.1](#emr-581-release) \| [5.8.0](#emr-580-release) **

**Amazon EMR Release 5\.8\.2**
+ [Application Versions](#emr-582-app-versions)
+ [Release Notes](#emr-582-relnotes)
+ [Component Versions](#emr-582-components)
+ [Configuration Classifications](#emr-582-class)

**Release 5\.8\.2 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.8.2.png)

**Release 5\.8\.2 Release Notes**

The following release notes include information for Amazon EMR release version 5\.8\.2\. Changes are relative to 5\.8\.1\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

**Release 5\.8\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.4\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.6\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.18\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-3 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-3 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-3 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-3 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-3 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-3 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-3 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-3 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-3 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-3 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.0\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.0\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-1 | Pig command\-line client\. | 
| spark\-client | 2\.2\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.8\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.8\.2 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.8\.1**
+ [Application Versions](#emr-581-app-versions)
+ [Release Notes](#emr-581-relnotes)
+ [Component Versions](#emr-581-components)
+ [Configuration Classifications](#emr-581-class)

**Release 5\.8\.1**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.8.1.png)

**Release 5\.8\.1 Release Notes**

The following release notes include information for the Amazon EMR 5\.8\.1 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Initial release date: January 22, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

**Release 5\.8\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.4\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.6\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.18\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-3 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-3 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-3 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-3 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-3 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-3 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-3 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-3 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-3 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-3 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.0\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.0\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-1 | Pig command\-line client\. | 
| spark\-client | 2\.2\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.8\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.8\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.8\.0**
+ [Application Versions](#emr-580-app-versions)
+ [Release Notes](#emr-580-relnotes)
+ [Component Versions](#emr-580-components)
+ [Configuration Classifications](#emr-580-class)

**Release 5\.8\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.8.0.png)

**Release 5\.8\.0 Release Notes**

The following release notes include information for the Amazon EMR version 5\.8\.0 release\. Changes are relative to the Amazon EMR 5\.7\.0 release\.

Initial release date: August 10, 2017

Latest feature update: September 25, 2017

**Upgrades**
+ AWS SDK 1\.11\.160
+ Flink 1\.3\.1
+ Hive 2\.3\.0\. For more information, see [Release Notes](https://issues.apache.org/jira/secure/ConfigureReleaseNote.jspa?projectId=12310843&version=12340269) on the Apache Hive site\.
+ Spark 2\.2\.0\. For more information, see [Release Notes](https://spark.apache.org/releases/spark-release-2-2-0.html) on the Apache Spark site\.

**New Features**
+ Added support for viewing application history \(September 25, 2017\)\. For more information, see [Viewing Application History](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ **Integration with AWS Glue Data Catalog**
  + Added ability for Hive and Spark SQL to use AWS Glue Data Catalog as the Hive metadata store\. For more information, see [Using the AWS Glue Data Catalog as the Metastore for Hive](emr-hive-metastore-glue.md) and [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md)\.
+ Added **Application history** to cluster details, which allows you to view historical data for YARN applications and additional details for Spark applications\. For more information, see [View Application History](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.
+ **Oozie**
  + Backported [OOZIE\-2748](https://issues.apache.org/jira/browse/OOZIE-2748)\.
+ **Hue**
  + Backported [HUE\-5859](https://issues.cloudera.org/browse/HUE-5859)
+ **HBase**
  + Added patch to expose the HBase master server start time through Java Management Extensions \(JMX\) using `getMasterInitializedTime`\.
  + Added patch that improves cluster start time\.

**Known Issues**
+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.
+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.
+ **Spark**—When using Spark, there is a file handler leak issue with the apppusher daemon, which can appear for a long\-running Spark job after several hours or days\. To fix the issue, connect to the master node and type `sudo /etc/init.d/apppusher stop`\. This stops that apppusher daemon, which Amazon EMR will restart automatically\.
+ **Application history**
  + Historical data for dead Spark executors is not available\.
  + Application history is not available for clusters that use a security configuration to enable in\-flight encryption\.

**Release 5\.8\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.4\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.4\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.4\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.6\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.18\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-3 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-3 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-3 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-3 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-3 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-3 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-3 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-3 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-3 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-3 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.0\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.0\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-1 | Pig command\-line client\. | 
| spark\-client | 2\.2\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.2\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.2\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.2\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.8\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.8\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.7\.0 ]

**Amazon EMR Release 5\.7\.0**
+ [Application Versions](#emr-570-app-versions)
+ [Release Notes](#emr-570-relnotes)
+ [Component Versions](#emr-570-components)
+ [Configuration Classifications](#emr-570-class)

**Release 5\.7\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.7.0.png)

**Release 5\.7\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.7\.0 release\. Changes are relative to the Amazon EMR 5\.6\.0 release\.

Release date: July 13, 2017

**Upgrades**
+ Flink 1\.3\.0
+ Phoenix 4\.11\.0
+ Zeppelin 0\.7\.2

**New Features**
+ Added the ability to specify a custom Amazon Linux AMI when you create a cluster\. For more information, see [Using a Custom AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html)\.

**Changes, Enhancements, and Resolved Issues**
+ **HBase**
  + Added capability to configure HBase read\-replica clusters\. See [Using a Read\-Replica Cluster\.](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-read-replica)
  + Multiple bug fixes and enhancements
+ **Presto**—added ability to configure `node.properties`\.
+ **YARN**—added ability to configure `container-log4j.properties`
+ **Sqoop**—backported [SQOOP\-2880](https://issues.apache.org/jira/browse/SQOOP-2880), which introduces an argument that allows you to set the Sqoop temporary directory\.

**Release 5\.7\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.18\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.3\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.11\.0\-HBase\-1\.3 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.11\.0\-HBase\-1\.3 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.7\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.7\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.6\.0 ]

**Amazon EMR Release 5\.6\.0**
+ [Application Versions](#emr-560-app-versions)
+ [Release Notes](#emr-560-relnotes)
+ [Component Versions](#emr-560-components)
+ [Configuration Classifications](#emr-560-class)

**Release 5\.6\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.6.0.png)

**Release 5\.6\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.6\.0 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Release date: June 5, 2017

**Upgrades**
+ Flink 1\.2\.1
+ HBase 1\.3\.1
+ Mahout 0\.13\.0\. This is the first version of Mahout to support Spark 2\.x in Amazon EMR version 5\.0 and later\.
+ Spark 2\.1\.1

**Changes, Enhancements, and Resolved Issues**
+ **Presto**
  + Added the ability to enable SSL/TLS secured communication between Presto nodes by enabling in\-transit encryption using a security configuration\. For more information, see [In\-transit Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption-options.html#emr-encryption-intransit)\.
  + Backported [Presto 7661](https://github.com/prestodb/presto/pull/7661/commits), which adds the `VERBOSE` option to the `EXPLAIN ANALYZE` statement to report more detailed, low\-level statistics about a query plan\.

**Release 5\.6\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.17\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.1 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.6\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.6\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | 
| presto\-node | Change values in Presto's node\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.5\.x ]

There are multiple releases within the 5\.5 series\. Choose a link below to see information for a specific release within this tab\.

**[5.5.3](#emr-553-release) \| [5.5.2](#emr-552-release) \| [5.5.1](#emr-551-release) \| [5.5.0](#emr-550-release)**

**Amazon EMR Release 5\.5\.3**
+ [Application Versions](#emr-553-app-versions)
+ [Release Notes](#emr-553-relnotes)
+ [Component Versions](#emr-553-components)
+ [Configuration Classifications](#emr-553-class)

**Release 5\.5\.3 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.5.3.png)

**Release 5\.5\.3 Release Notes**

The following release notes include information for Amazon EMR release version 5\.5\.3\. Changes are relative to 5\.5\.2\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

**Release 5\.5\.3 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.16\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.5\.3 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.5\.3 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.5\.2**
+ [Application Versions](#emr-552-app-versions)
+ [Release Notes](#emr-552-relnotes)
+ [Component Versions](#emr-552-components)
+ [Configuration Classifications](#emr-552-class)

**Release 5\.5\.2 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.5.2.png)

**Release 5\.5\.2 Release Notes**

The following release notes include information for Amazon EMR release version 5\.5\.2\. Changes are relative to 5\.5\.1\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

**Release 5\.5\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.16\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.5\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.5\.2 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.5\.1**
+ [Application Versions](#emr-551-app-versions)
+ [Release Notes](#emr-551-relnotes)
+ [Component Versions](#emr-551-components)
+ [Configuration Classifications](#emr-551-class)

**Release 5\.5\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.5.1.png)

**Release 5\.5\.1 Release Notes**

The following release notes include information for the Amazon EMR 5\.5\.1 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Initial release date: January 22, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

**Release 5\.5\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.16\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.5\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.5\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.5\.0**
+ [Application Versions](#emr-550-app-versions)
+ [Release Notes](#emr-550-relnotes)
+ [Component Versions](#emr-550-components)
+ [Configuration Classifications](#emr-550-class)

**Release 5\.5\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.5.0.png)

**Release 5\.5\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.5\.0 release\. Changes are relative to the Amazon EMR 5\.4\.0 release\.

Release date: April 26, 2017

**Upgrades**
+ Hue 3\.12
+ Presto 0\.170
+ Zeppelin 0\.7\.1
+ ZooKeeper 3\.4\.10

**Changes, Enhancements, and Resolved Issues**
+ **Spark**
  + Backported Spark Patch [\(SPARK\-20115\) Fix DAGScheduler to recompute all the lost shuffle blocks when external shuffle service is unavailable](https://issues.apache.org/jira/browse/SPARK-20115) to version 2\.1\.0 of Spark, which is included in this release\.
+ **Flink**
  + Flink is now built with Scala 2\.11\. If you use the Scala API and libraries, we recommend that you use Scala 2\.11 in your projects\.
  + Addressed an issue where `HADOOP_CONF_DIR` and `YARN_CONF_DIR` defaults were not properly set, so `start-scala-shell.sh` failed to work\. Also added the ability to set these values using `env.hadoop.conf.dir` and `env.yarn.conf.dir` in `/etc/flink/conf/flink-conf.yaml` or the `flink-conf` configuration classification\.
  + Introduced a new EMR\-specific command, `flink-scala-shell` as a wrapper for `start-scala-shell.sh`\. We recommend using this command instead of `start-scala-shell`\. The new command simplifies execution\. For example, `flink-scala-shell -n 2` starts a Flink Scala shell with a task parallelism of 2\.
  + Introduced a new EMR\-specific command, `flink-yarn-session` as a wrapper for `yarn-session.sh`\. We recommend using this command instead of `yarn-session`\. The new command simplifies execution\. For example, `flink-yarn-session -n 2 -d` starts a long\-running Flink session in a detached state with two task managers\. 
  + Addressed [\(FLINK\-6125\) Commons httpclient is not shaded anymore in Flink 1\.2](https://issues.apache.org/jira/browse/FLINK-6125)\.
+ **Presto**
  + Added support for LDAP authentication\. Using LDAP with Presto on Amazon EMR requires that you enable HTTPS access for the Presto coordinator \(`http-server.https.enabled=true` in `config.properties`\)\. For configuration details, see [LDAP Authentication](https://prestodb.io/docs/current/security/ldap.html) in Presto documentation\.
  + Added support for `SHOW GRANTS`\.
+ **Amazon EMR Base Linux AMI**
  + Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [Amazon Linux AMI 2017\.03 Release Notes](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.
  + Removed Python 2\.6 from the Amazon EMR base Linux image\. Python 2\.7 and 3\.4 are installed by default\. You can install Python 2\.6 manually if necessary\.

**Release 5\.5\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.5\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.16\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.12\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.170 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.170 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.10 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.10 | ZooKeeper command line client\. | 

**Release 5\.5\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.5\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.4\.0 ]

**Amazon EMR Release 5\.4\.0**
+ [Application Versions](#emr-540-app-versions)
+ [Release Notes](#emr-540-relnotes)
+ [Component Versions](#emr-540-components)
+ [Configuration Classifications](#emr-540-class)

**Release 5\.4\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.4.0.png)

**Release 5\.4\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.4\.0 release\. Changes are relative to the Amazon EMR 5\.3\.0 release\.

Release date: March 08, 2017

**Upgrades**
+ Upgraded to Flink 1\.2\.0
+ Upgraded to HBase 1\.3\.0
+ Upgraded to Phoenix 4\.9\.0
**Note**  
If you upgrade from an earlier version of Amazon EMR to Amazon EMR version 5\.4\.0 or later and use secondary indexing, upgrade local indexes as described in the [Apache Phoenix documentation](https://phoenix.apache.org/secondary_indexing.html#Upgrading_Local_Indexes_created_before_4.8.0)\. Amazon EMR removes the required configurations from the `hbase-site` classification, but indexes need to be repopulated\. Online and offline upgrade of indexes are supported\. Online upgrades are the default, which means indexes are repopulated while initializing from Phoenix clients of version 4\.8\.0 or greater\. To specify offline upgrades, set the `phoenix.client.localIndexUpgrade` configuration to false in the `phoenix-site` classification, and then SSH to the master node to run `psql [zookeeper] -1`\.
+ Upgraded to Presto 0\.166
+ Upgraded to Zeppelin 0\.7\.0

**Changes and Enhancements**
+ Added support for r4 instances\. See [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)\.

**Release 5\.4\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.3\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.15\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.2\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.3\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.3\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.3\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.3\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.3\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.1\.1\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.11\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.9\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.9\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.166 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.166 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.7\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 5\.4\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.4\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.3\.x ]<a name="emr-53x-releases"></a>

There are multiple releases within the 5\.3 series\. Choose a link below to see information for a specific release within this tab\.

**[5.3.1](#emr-531-release) \(Latest\) \| [5.3.0](#emr-530-release)**

**Amazon EMR Release 5\.3\.1**
+ [Application Versions](#emr-531-app-versions)
+ [Release Notes](#emr-531-relnotes)
+ [Component Versions](#emr-531-components)
+ [Configuration Classifications](#emr-531-class)

**Release 5\.3\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.3.1.png)

**Release 5\.3\.1 Release Notes**

The following release notes include information for the Amazon EMR 5\.3\.1 release\. Changes are relative to the Amazon EMR 5\.3\.0 release\.

Release date: February 7, 2017

Minor changes to backport Zeppelin patches and update the default AMI for Amazon EMR\.

**Release 5\.3\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.14\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.4 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.11\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 5\.3\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.3\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.3\.0**
+ [Application Versions](#emr-530-app-versions)
+ [Release Notes](#emr-530-relnotes)
+ [Component Versions](#emr-530-components)
+ [Configuration Classifications](#emr-530-class)

**Release 5\.3\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.3.0.png)

**Release 5\.3\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.3\.0 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: January 26, 2017

**Upgrades**
+ Upgraded to Hive 2\.1\.1
+ Upgraded to Hue 3\.11\.0
+ Upgraded to Spark 2\.1\.0
+ Upgraded to Oozie 4\.3\.0
+ Upgraded to Flink 1\.1\.4

**Changes and Enhancements**
+ Added a patch to Hue that allows you to use the `interpreters_shown_on_wheel` setting to configure what interpreters to show first on the Notebook selection wheel, regardless of their ordering in the `hue.ini` file\.
+ Added the `hive-parquet-logging` configuration classification, which you can use to configure values in the Hive `parquet-logging.properties` file\.

**Release 5\.3\.0 Component Versions**


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.14\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.4 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.1\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.1\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.1\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.1\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.1\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.1\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.11\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.3\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.3\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.1\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.1\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.1\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.1\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 5\.3\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.3\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.2\.x ]

There are multiple releases within the 5\.2 series\. Choose a link below to see information for a specific release within this tab\.

**[5.2.2](#emr-522-release) \| [5.2.1](#emr-521-release) \| [5.2.0](#emr-520-release)** 

**Amazon EMR Release 5\.2\.2**
+ [Application Versions](#emr-522-app-versions)
+ [Release Notes](#emr-522-relnotes)
+ [Component Versions](#emr-522-components)
+ [Configuration Classifications](#emr-522-class)

**Release 5\.2\.2 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.2.2.png)

**Release 5\.2\.2 Release Notes**

The following release notes include information for the Amazon EMR 5\.2\.2 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: May 2, 2017

**Known Issues Resolved from the Previous Releases**
+ Backported [SPARK\-194459](https://issues.apache.org/jira/browse/SPARK-19459), which addresses an issue where reading from an ORC table with char/varchar columns can fail\.

**Release 5\.2\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.13\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.3 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 5\.2\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.2\.2 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.2\.1**
+ [Application Versions](#emr-521-app-versions)
+ [Release Notes](#emr-521-relnotes)
+ [Component Versions](#emr-521-components)
+ [Configuration Classifications](#emr-521-class)

**Release 5\.2\.1 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.2.1.png)

**Release 5\.2\.1 Release Notes**

The following release notes include information for the Amazon EMR 5\.2\.1 release\. Changes are relative to the Amazon EMR 5\.2\.0 release\.

Release date: December 29, 2016

**Upgrades**
+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\. 
+ Upgraded to Zookeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

**Changes and Enhancements**
+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.
+ The location of Flink and YARN configuration paths are now set by default in `/etc/default/flink` that you do not need to set the environment variables `FLINK_CONF_DIR` and `HADOOP_CONF_DIR` when running the `flink` or `yarn-session.sh` driver scripts to launch Flink jobs\.
+ Added support for FlinkKinesisConsumer class\.

**Known Issues Resolved from the Previous Releases**
+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.
+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

**Release 5\.2\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.13\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.3 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 5\.2\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.2\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.2\.0**
+ [Application Versions](#emr-520-app-versions)
+ [Release Notes](#emr-520-relnotes)
+ [Component Versions](#emr-520-components)
+ [Configuration Classifications](#emr-520-class)

**Release 5\.2\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.2.0.png)

**Release 5\.2\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.2\.0 release\. Changes are relative to the Amazon EMR 5\.1\.0 release\.

Release date: November 21, 2016

**Changes and enhancements**
+ Added Amazon S3 storage mode for HBase\.
+  Enables you to specify an Amazon S3 location for the HBase rootdir\. For more information, see [HBase on Amazon S3](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html)\.

**Upgrades**
+ Upgraded to Spark 2\.0\.2

**Known Issues Resolved from the Previous Releases**
+ Fixed an issue with /mnt being constrained to 2 TB on EBS\-only instance types\.
+ Fixed an issue with instance\-controller and logpusher logs being output to their corresponding \.out files instead of to their normal log4j\-configured \.log files, which rotate hourly\. The \.out files do not rotate, so this would eventually fill up the /emr partition\. This issue only affects hardware virtual machine \(HVM\) instance types\.

**Release 5\.2\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.1\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.12\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.3 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.152\.3 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.152\.3 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 5\.2\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.2\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.1\.0 ]

**Amazon EMR Release 5\.1\.0**
+ [Application Versions](#emr-51-app-versions)
+ [Release Notes](#emr-51-relnotes)
+ [Component Versions](#emr-51-components)
+ [Configuration Classifications](#emr-51-class)

**Release 5\.1\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.1.0.png)

**Release 5\.1\.0 Release Notes**

The following release notes include information for the Amazon EMR 5\.1\.0 release\. Changes are relative to the Amazon EMR 5\.0\.3 release\.

Release date: November 03, 2016

**Changes and enhancements**
+ Added support for Flink 1\.1\.3\.
+ Presto has been added as an option in the notebook section of Hue\.

**Upgrades**
+ Upgraded to HBase 1\.2\.3
+ Upgraded to Zeppelin 0\.6\.2

**Known Issues Resolved from the Previous Releases**
+ Fixed an issue with Tez queries on Amazon S3 with ORC files did not perform as well as earlier Amazon EMR 4\.x versions\.

**Release 5\.1\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.1\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.11\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.1\.3 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.152\.3 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.152\.3 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.2 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.1\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 5\.0\.x ]

There are multiple releases within the 5\.0 series\. Choose a link below to see information for a specific release within this tab\.

**[5.0.3](#emr-503-release) \| [5.0.0](#emr-500-release)**

**Amazon EMR Release 5\.0\.3**
+ [Application Versions](#emr-503-app-versions)
+ [Release Notes](#emr-503-relnotes)
+ [Component Versions](#emr-503-components)
+ [Configuration Classifications](#emr-503-class)

**Release 5\.0\.3 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.0.3.png)

**Release 5\.0\.3 Release Notes**

The following release notes include information for the Amazon EMR 5\.0\.3 release\. Changes are relative to the Amazon EMR 5\.0\.0 release\.

Release date: October 24, 2016

**Upgrades**
+ Upgraded to Hadoop 2\.7\.3
+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.
+ Upgraded to Spark 2\.0\.1
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

**Release 5\.0\.3 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.1\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.10\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.3\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.3\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.3\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.3\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.3\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.3\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.3\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.3\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.3\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.3\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.152\.3 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.152\.3 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 5\.0\.3 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.0\.3 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

**Amazon EMR Release 5\.0\.0**
+ [Application Versions](#emr-500-app-versions)
+ [Release Notes](#emr-500-relnotes)
+ [Component Versions](#emr-500-components)
+ [Configuration Classifications](#emr-500-class)

**Release 5\.0\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-5.0.0.png)

**Release 5\.0\.0 Release Notes**

 Release date: July 27, 2016

**Upgrades**
+ Upgraded to Hive 2\.1
+ Upgraded to Presto 0\.150
+ Upgraded to Spark 2\.0
+ Upgraded to Hue 3\.10\.0
+ Upgraded to Pig 0\.16\.0
+ Upgraded to Tez 0\.8\.4
+ Upgraded to Zeppelin 0\.6\.1

**Changes and Enhancements**
+ Amazon EMR supports the latest open\-source versions of Hive \(version 2\.1\) and Pig \(version 0\.16\.0\)\. If you have used Hive or Pig on Amazon EMR in the past, this may affect some use cases\. For more information, see [Hive](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive.html) and [Pig](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-pig.html)\.
+ The default execution engine for Hive and Pig is now Tez\. To change this, you would edit the appropriate values in the `hive-site` and `pig-properties` configuration classifications, respectively\.
+ An enhanced step debugging feature was added, which allows you to see the root cause of step failures if the service can determine the cause\. For more information, see [ Enhanced Step Debugging](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-enhanced-step-debugging.html) in the Amazon EMR Management Guide\.
+ Applications that previously ended with "\-Sandbox" no longer have that suffix\. This may break your automation, for example, if you are using scripts to launch clusters with these applications\. The following table shows application names in Amazon EMR 4\.7\.2 versus Amazon EMR 5\.0\.0\.   
**Application name changes**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-5x.html)
+ Spark is now compiled for Scala 2\.11\.
+ Java 8 is now the default JVM\. All applications run using the Java 8 runtime\. There are no changes to any application’s byte code target\. Most applications continue to target Java 7\.
+ Zeppelin now includes authentication features\. For more information, see [Zeppelin](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-zeppelin.html)\.
+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

**Release 5\.0\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.9\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-3 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-3 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-3 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-3 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-3 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-3 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-3 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-3 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-3 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.2\-amzn\-3 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.1\.0\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.1\.0\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.1\.0\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.1\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 2\.1\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 2\.1\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.10\.0\-amzn\-0 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.46 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.150 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.150 | Service for executing pieces of a query\. | 
| pig\-client | 0\.16\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 2\.0\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.0\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.0\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.0\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1\-SNAPSHOT | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 5\.0\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-5\.0\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | 
| hbase\-env | Change values in HBase's environment\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbaase\.properties file\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | 
| hue\-ini | Change values in Hue's ini file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| oozie\-env | Change values in Oozie's environment\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------