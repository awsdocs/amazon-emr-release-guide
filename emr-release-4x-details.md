# Details for Amazon EMR 4\.x Release Versions<a name="emr-release-4x-details"></a>

Each tab below lists application versions, release notes, component versions, and configuration classifications available in each Amazon EMR 4\.x release version\.

For a comprehensive diagram of application versions in every release, see [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-4x.png)\.

For application\-specific differences between Amazon EMR 4\.x release versions and versions beginning with Amazon EMR 5\.0\.0, see [Differences in Amazon EMR 4\.x Release Versions](emr-release-differences-4x.md)\.

------
#### [ 4\.9\.x ]

There are multiple releases within the 4\.9 series\. Choose a link below to see information for a specific release within this tab\.

**[4.9.5](#emr-495-release) \| [4.9.4](#emr-494-release) \| [4.9.3](#emr-493-release) \| [4.9.2](#emr-492-release) \| [4.9.1](#emr-491-release)** 

**Amazon EMR Release 4\.9\.5**
+ [Application Versions](#emr-495-app-versions)
+ [Release Notes](#emr-495-relnotes)
+ [Component Versions](#emr-495-components)
+ [Configuration Classifications](#emr-495-class)

**Release 4\.9\.5 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.9.5.png)

**Release 4\.9\.5 Release Notes**

The following release notes include information for Amazon EMR release version 4\.9\.5\. Changes are relative to 4\.9\.4\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ HBase
  + This release addresses a potential security vulnerability\.

**Release 4\.9\.5 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.17\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-9 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-9 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-9 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-9 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-9 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-9 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.9\.5 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.9\.5 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Amazon EMR Release 4\.9\.4**
+ [Application Versions](#emr-494-app-versions)
+ [Release Notes](#emr-494-relnotes)
+ [Component Versions](#emr-494-components)
+ [Configuration Classifications](#emr-494-class)

**Release 4\.9\.4 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.9.4.png)

**Release 4\.9\.4 Release Notes**

The following release notes include information for Amazon EMR release version 4\.9\.4\. Changes are relative to 4\.9\.3\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

**Release 4\.9\.4 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.17\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-9 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-9 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-9 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-9 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-9 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-9 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.9\.4 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.9\.4 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Amazon EMR Release 4\.9\.3**
+ [Application Versions](#emr-493-app-versions)
+ [Release Notes](#emr-493-relnotes)
+ [Component Versions](#emr-493-components)
+ [Configuration Classifications](#emr-493-class)

**Release 4\.9\.3 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.9.3.png)

**Release 4\.9\.3 Release Notes**

The following release notes include information for the Amazon EMR 4\.9\.3 release\. Changes are relative to the Amazon EMR 4\.9\.2 release\.

Initial release date: January 22, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the default Amazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

**Release 4\.9\.3 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.17\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-9 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-9 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-9 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-9 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-9 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-9 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.9\.3 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.9\.3 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Release 4\.9\.2**
+ [Application Versions](#emr-492-app-versions)
+ [Release Notes](#emr-492-relnotes)
+ [Component Versions](#emr-492-components)
+ [Configuration Classifications](#emr-492-class)

**Release 4\.9\.2 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.9.2.png)

**Release 4\.9\.2 Release Notes**

The following release notes include information for the Amazon EMR 4\.9\.2 release\. Changes are relative to the Amazon EMR 4\.9\.1 release\.

Release date: July 13, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

**Release 4\.9\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.3\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.17\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-9 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-9 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-9 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-9 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-9 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-9 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.9\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.9\.2 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Release 4\.9\.1**
+ [Application Versions](#emr-491-app-versions)
+ [Release Notes](#emr-491-relnotes)
+ [Component Versions](#emr-491-components)
+ [Configuration Classifications](#emr-491-class)

**Release 4\.9\.1 Application Versions**

The following applications are supported in this release:[Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.9.1.png)

**Release 4\.9\.1 Release Notes**

The following release notes include information for the Amazon EMR 4\.9\.1 release\. Changes are relative to the Amazon EMR 4\.8\.4 release\.

Release date: April 10, 2017

**Known Issues Resolved from the Previous Releases**
+ Backports of [HIVE\-9976](https://issues.apache.org/jira/browse/HIVE-9976) and [HIVE\-10106](https://issues.apache.org/jira/browse/HIVE-10106)
+ Fixed an issue in YARN where a large number of nodes \(greater than 2,000\) and containers \(greater than 5,000\) would cause an out\-of\-memory error, for example: `"Exception in thread main java.lang.OutOfMemoryError"`\.

**Changes and Enhancements**
+ Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.
+ Removed Python 2\.6 from the Amazon EMR base Linux image\. You can install Python 2\.6 manually if necessary\.

**Release 4\.9\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.3\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.15\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-9 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-9 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-9 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-9 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-9 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-9 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A lightweight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.9\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.8\.5 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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
#### [ 4\.8\.x  ]

There are multiple releases within the 4\.8 series\. Choose a link below to see information for a specific release within this tab\.

**[4.8.4](#emr-484-release) \| [4.8.3](#emr-483-release) \| [4.8.2](#emr-482-release) \| [4.8.0](#emr-480-release)**

**Amazon EMR Release 4\.8\.4**
+ [Application Versions](#emr-484-app-versions)
+ [Release Notes](#emr-484-relnotes)
+ [Component Versions](#emr-484-components)
+ [Configuration Classifications](#emr-484-class)

**Release 4\.8\.4 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.8.4.png)

**Release 4\.8\.4 Release Notes**

The following release notes include information for the Amazon EMR 4\.8\.4 release\. Changes are relative to the Amazon EMR 4\.8\.3 release\.

Release date: February 7, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

**Release 4\.8\.4 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.14\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-8 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-8 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-8 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-8 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-8 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-8 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.54\+ | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.8\.4 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.8\.4 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Amazon EMR Release 4\.8\.3**
+ [Application Versions](#emr-483-app-versions)
+ [Release Notes](#emr-483-relnotes)
+ [Component Versions](#emr-483-components)
+ [Configuration Classifications](#emr-483-class)

**Release 4\.8\.3 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.8.3.png)

**Release 4\.8\.3 Release Notes**

The following release notes include information for the Amazon EMR 4\.8\.3 release\. Changes are relative to the Amazon EMR 4\.8\.2 release\.

Release date: December 29, 2016

**Upgrades**
+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\.
+ Upgraded to Spark 1\.6\.3\. For more information, see [Spark Release Notes](http://spark.apache.org/releases/spark-release-1-6-3.html) in the Apache Spark documentation\.
+ Upgraded to ZooKeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

**Changes and Enhancements**
+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

**Known Issues Resolved from the Previous Releases**
+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.
+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

**Release 4\.8\.3 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 4\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.2\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.13\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-8 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-8 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-8 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-8 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-8 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-8 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.157\.1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.157\.1 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.3 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.3 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.3 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.3 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.9 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.9 | ZooKeeper command line client\. | 

**Release 4\.8\.3 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.8\.3 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Amazon EMR Release 4\.8\.2**
+ [Application Versions](#emr-482-app-versions)
+ [Release Notes](#emr-482-relnotes)
+ [Component Versions](#emr-482-components)
+ [Configuration Classifications](#emr-482-class)

**Release 4\.8\.2 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.8.2.png)

**Release 4\.8\.2 Release Notes**

The following release notes include information for the Amazon EMR 4\.8\.2 release\. Changes are relative to the Amazon EMR 4\.8\.0 release\.

Release date: October 24, 2016

**Upgrades**
+ Upgraded to Hadoop 2\.7\.3
+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

**Release 4\.8\.2 Component Versions**

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
| hcatalog\-client | 1\.0\.0\-amzn\-7 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-7 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-7 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-7 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-7 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-7 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.52 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.152\.3 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.152\.3 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.8\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.8\.2 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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

**Amazon EMR Release 4\.8\.0**
+ [Application Versions](#emr-480-app-versions)
+ [Release Notes](#emr-480-relnotes)
+ [Component Versions](#emr-480-components)
+ [Configuration Classifications](#emr-480-class)

**Release 4\.8\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.8.0.png)

**Release 4\.8\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.8\.0 release\. Changes are relative to the Amazon EMR 4\.7\.2 release\.

Release date: September 7, 2016

**Upgrades**
+ Upgraded to HBase 1\.2\.2
+ Upgraded to Presto\-Sandbox 0\.151
+ Upgraded to Tez 0\.8\.4
+ Upgraded to Zeppelin\-Sandbox 0\.6\.1

**Changes and Enhancements**
+ Fixed an issue in YARN where the ApplicationMaster would attempt to clean up containers that no longer exist because their instances have been terminated\.
+ Corrected the hive\-server2 URL for Hive2 actions in the Oozie examples\.
+ Added support for additional Presto catalogs\.
+ Backported patches: [HIVE\-8948](https://issues.apache.org/jira/browse/HIVE-8948), [HIVE\-12679](https://issues.apache.org/jira/browse/HIVE-12679), [HIVE\-13405](https://issues.apache.org/jira/browse/HIVE-13405), [PHOENIX\-3116](https://issues.apache.org/jira/browse/PHOENIX-3116), [HADOOP\-12689](https://issues.apache.org/jira/browse/HADOOP-12689)
+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

**Release 4\.8\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.9\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-4 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-4 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-4 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-4 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-4 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-4 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-4 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-4 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-4 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.2\-amzn\-4 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.2 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.2 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.2 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.2 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.2 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-7 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-7 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-7 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-7 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-7 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-7 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.51 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.151 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.151 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.4 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.6\.1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.8\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.8\.0 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
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
#### [ 4\.7\.x ]

There are multiple releases within the 4\.7 series\. Choose a link below to see information for a specific release within this tab\.

**[4.7.2](#emr-472-release) \| [4.7.1](#emr-471-release) \| [4.7.1](#emr-471-release)**

**Amazon EMR Release 4\.7\.2**
+ [Application Versions](#emr-472-app-versions)
+ [Release Notes](#emr-472-relnotes)
+ [Component Versions](#emr-472-components)
+ [Configuration Classifications](#emr-472-class)

**Release 4\.7\.2 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.7.2.png)

**Release 4\.7\.2 Release Notes**

The following release notes include information for Amazon EMR 4\.7\.2\.

Release date: July 15, 2016

**Features**
+ Upgraded to Mahout 0\.12\.2
+ Upgraded to Presto 0\.148
+ Upgraded to Spark 1\.6\.2
+ You can now create an AWSCredentialsProvider for use with EMRFS using a URI as a parameter\. For more information, see [Create an AWSCredentialsProvider for EMRFS](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-plan-credentialsprovider.html)\.
+ EMRFS now allows users to configure a custom DynamoDB endpoint for their Consistent View metadata using the `fs.s3.consistent.dynamodb.endpoint` property in `emrfs-site.xml`\.
+ Added a script in `/usr/bin` called `spark-example`, which wraps `/usr/lib/spark/spark/bin/run-example` so you can run examples directly\. For instance, to run the SparkPi example that comes with the Spark distribution, you can run `spark-example SparkPi 100` from the command line or using `command-runner.jar` as a step in the API\.

**Known Issues Resolved from Previous Releases**
+ Fixed an issue where Oozie had the `spark-assembly.jar` was not in the correct location when Spark was also installed, which resulted in failure to launch Spark applications with Oozie\.
+ Fixed an issue with Spark Log4j\-based logging in YARN containers\.

**Release 4\.7\.2 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.2\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.8\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
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
| hbase\-hmaster | 1\.2\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-6 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-6 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-6 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-6 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-6 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-6 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.2 | Library for machine learning\. | 
| mysql\-server | 5\.5\.46 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.148 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.148 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.2 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.3 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.23 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.7\.2 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.7\.2 Classifications**  

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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
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

**Amazon EMR Release 4\.7\.1**
+ [Application Versions](#emr-471-app-versions)
+ [Release Notes](#emr-471-relnotes)
+ [Component Versions](#emr-471-components)
+ [Configuration Classifications](#emr-471-class)

**Release 4\.7\.1 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.7.0.png)

**Release 4\.7\.1 Release Notes**

The following release notes include information for Amazon EMR 4\.7\.1\.

Release date: June 10, 2016

**Known Issues Resolved from Previous Releases**
+ Fixed an issue that extended the startup time of clusters launched in a VPC with private subnets\. The bug only impacted clusters launched with the Amazon EMR 4\.7\.0 release\. 
+ Fixed an issue that improperly handled listing of files in Amazon EMR for clusters launched with the Amazon EMR 4\.7\.0 release\.

**Release 4\.7\.1 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.1\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.7\.1 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.2\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-5 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-5 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-5 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-5 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-5 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-5 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.46 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.147 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.147 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.3 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.18 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.7\.1 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.7\.1 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
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

**Amazon EMR Release 4\.7\.0**
+ [Application Versions](#emr-470-app-versions)
+ [Release Notes](#emr-470-relnotes)
+ [Component Versions](#emr-470-components)
+ [Configuration Classifications](#emr-470-class)

**Release 4\.7\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Tez](https://tez.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.7.0.png)

**Release 4\.7\.0 Release Notes**

**Important**  
Amazon EMR 4\.7\.0 is deprecated\. Use Amazon EMR 4\.7\.1 or later instead\.

Release date: June 2, 2016

**Features**
+ Added Apache Phoenix 4\.7\.0
+ Added Apache Tez 0\.8\.3
+ Upgraded to HBase 1\.2\.1
+ Upgraded to Mahout 0\.12\.0
+ Upgraded to Presto 0\.147
+ Upgraded the AWS SDK for Java to 1\.10\.75
+ The final flag was removed from the `mapreduce.cluster.local.dir` property in `mapred-site.xml` to allow users to run Pig in local mode\.
+ Amazon Redshift JDBC Drivers Available on Cluster

  Amazon Redshift JDBC drivers are now included at `/usr/share/aws/redshift/jdbc`\. `/usr/share/aws/redshift/jdbc/RedshiftJDBC41.jar` is the JDBC 4\.1\-compatible Amazon Redshift driver and `/usr/share/aws/redshift/jdbc/RedshiftJDBC4.jar` is the JDBC 4\.0\-compatible Amazon Redshift driver\. For more information, see [Configure a JDBC Connection](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html) in the *Amazon Redshift Cluster Management Guide*\.
+ Java 8

  Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

**Known Issues Resolved from Previous Releases**
+ Fixed a kernel issue that significantly affected performance on Throughput Optimized HDD \(st1\) EBS volumes for Amazon EMR in emr\-4\.6\.0\.
+ Fixed an issue where a cluster would fail if any HDFS encryption zone were specified without choosing Hadoop as an application\.
+ Changed the default HDFS write policy from `RoundRobin` to `AvailableSpaceVolumeChoosingPolicy`\. Some volumes were not properly utilized with the RoundRobin configuration, which resulted in failed core nodes and an unreliable HDFS\.
+ Fixed an issue with the EMRFS CLI, which would cause an exception when creating the default DynamoDB metadata table for consistent views\.
+ Fixed a deadlock issue in EMRFS that potentially occurred during multipart rename and copy operations\.
+ Fixed an issue with EMRFS that caused the CopyPart size default to be 5 MB\. The default is now properly set at 128 MB\.
+ Fixed an issue with the Zeppelin upstart configuration that potentially prevented you from stopping the service\.
+ Fixed an issue with Spark and Zeppelin, which prevented you from using the `s3a://` URI scheme because `/usr/lib/hadoop/hadoop-aws.jar` was not properly loaded in their respective classpath\.
+ Backported [HUE\-2484](https://issues.cloudera.org/browse/HUE-2484)\.
+ Backported a [commit](https://github.com/cloudera/hue/commit/c3c89f085e7a29c9fac7de016d881142d90af3eb) from Hue 3\.9\.0 \(no JIRA exists\) to fix an issue with the HBase browser sample\. 
+ Backported [HIVE\-9073](https://issues.apache.org/jira/browse/HIVE-9073)\.

**Release 4\.7\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.1\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.2\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.4\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.7\.1 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.7\.2\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.2\.1 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.1 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.1 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.1 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.1 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-5 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-5 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-5 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-5 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-5 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-5 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-7 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.12\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5\.46 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| phoenix\-library | 4\.7\.0\-HBase\-1\.2 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.7\.0\-HBase\-1\.2 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.147 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.147 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| tez\-on\-yarn | 0\.8\.3 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.18 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.7\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.7\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
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
#### [ 4\.6\.0 ]

**Amazon EMR Release 4\.6\.0**
+ [Application Versions](#emr-460-app-versions)
+ [Release Notes](#emr-460-relnotes)
+ [Component Versions](#emr-460-components)
+ [Configuration Classifications](#emr-460-class)

**Release 4\.6\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/), and [ZooKeeper\-Sandbox](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.6.0.png)

**Release 4\.6\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.6\.0 release\.
+ Added HBase 1\.2\.0
+ Added Zookeeper\-Sandbox 3\.4\.8 
+ Upgraded to Presto\-Sandbox 0\.143
+ Amazon EMR releases are now based on Amazon Linux 2016\.03\.0\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/)\.
+ Issue Affecting Throughput Optimized HDD \(st1\) EBS Volume Types

  An issue in the Linux kernel versions 4\.2 and above significantly affects performance on Throughput Optimized HDD \(st1\) EBS volumes for EMR\. This release \(emr\-4\.6\.0\) uses kernel version 4\.4\.5 and hence is impacted\. Therefore, we recommend not using emr\-4\.6\.0 if you want to use st1 EBS volumes\. You can use emr\-4\.5\.0 or prior Amazon EMR releases with st1 without impact\. In addition, we provide the fix with future releases\.
+ Python Defaults

  Python 3\.4 is now installed by default, but Python 2\.7 remains the system default\. You may configure Python 3\.4 as the system default using either a bootstrap action; you can use the configuration API to set PYSPARK\_PYTHON export to `/usr/bin/python3.4` in the `spark-env` classification to affect the Python version used by PySpark\.
+ Java 8

  Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

**Known Issues Resolved from Previous Releases**
+ Fixed an issue where application provisioning would sometimes randomly fail due to a generated password\.
+ Previously, `mysqld` was installed on all nodes\. Now, it is only installed on the master instance and only if the chosen application includes `mysql-server` as a component\. Currently, the following applications include the `mysql-server` component: HCatalog, Hive, Hue, Presto\-Sandbox, and Sqoop\-Sandbox\.
+ Changed `yarn.scheduler.maximum-allocation-vcores` to 80 from the default of 32, which fixes an issue introduced in emr\-4\.4\.0 that mainly occurs with Spark while using the `maximizeResourceAllocation` option in a cluster whose core instance type is one of a few large instance types that have the YARN vcores set higher than 32; namely c4\.8xlarge, cc2\.8xlarge, hs1\.8xlarge, i2\.8xlarge, m2\.4xlarge, r3\.8xlarge, d2\.8xlarge, or m4\.10xlarge were affected by this issue\.
+ s3\-dist\-cp now uses EMRFS for all Amazon S3 nominations and no longer stages to a temporary HDFS directory\.
+ Fixed an issue with exception handling for client\-side encryption multipart uploads\.
+ Added an option to allow users to change the Amazon S3 storage class\. By default this setting is `STANDARD`\. The `emrfs-site` configuration classification setting is `fs.s3.storageClass` and the possible values are `STANDARD`, `STANDARD_IA`, and `REDUCED_REDUNDANCY`\. For more information about storage classes, see [Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html) in the Amazon Simple Storage Service Developer Guide\. 

**Release 4\.6\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.3\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.6\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hbase\-hmaster | 1\.2\.0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.2\.0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.2\.0 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.2\.0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.2\.0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-4 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-4 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-4 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-4 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-4 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-4 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-6 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.1 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.143 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.143 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| webserver | 2\.4 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.8 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.8 | ZooKeeper command line client\. | 

**Release 4\.6\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.6\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
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
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------
#### [ 4\.5\.0 ]

**Amazon EMR Release 4\.5\.0**
+ [Application Versions](#emr-450-app-versions)
+ [Release Notes](#emr-450-relnotes)
+ [Component Versions](#emr-450-components)
+ [Configuration Classifications](#emr-450-class)

**Release 4\.5\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), and [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.5.0.png)

**Release 4\.5\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.5\.0 release\.

Release date: April 4, 2016

**Features**
+ Upgraded to Spark 1\.6\.1
+ Upgraded to Hadoop 2\.7\.2
+ Upgraded to Presto 0\.140
+ Added AWS KMS support for Amazon S3 server\-side encryption\.

**Known Issues Resolved from Previous Releases**
+ Fixed an issue where MySQL and Apache servers would not start after a node was rebooted\. 
+ Fixed an issue where IMPORT did not work correctly with non\-partitioned tables stored in Amazon S3
+ Fixed an issue with Presto where it requires the staging directory to be `/mnt/tmp` rather than `/tmp` when writing to Hive tables\.

**Release 4\.5\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.2\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.5\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.2\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.2\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.2\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.2\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.2\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.2\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.2\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.2\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.2\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-4 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-4 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-4 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-4 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-4 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-4 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-5 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.1 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.140 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.140 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.1 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| webserver | 2\.4 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 

**Release 4\.5\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.5\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 

------
#### [ 4\.4\.0 ]

**Amazon EMR Release 4\.4\.0**
+ [Application Versions](#emr-440-app-versions)
+ [Release Notes](#emr-440-relnotes)
+ [Component Versions](#emr-440-components)
+ [Configuration Classifications](#emr-440-class)

**Release 4\.4\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop\-Sandbox](http://sqoop.apache.org/), and [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.4.0.png)

**Release 4\.4\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.4\.0 release\.

Release date: March 14, 2016

**Features**
+ Added HCatalog 1\.0\.0
+ Added Sqoop\-Sandbox 1\.4\.6
+ Upgraded to Presto 0\.136
+ Upgraded to Zeppelin 0\.5\.6
+ Upgraded to Mahout 0\.11\.1
+ Enabled `dynamicResourceAllocation` by default\.
+ Added a table of all configuration classifications for the release\. For more information, see the Configuration Classifications table in [Configuring Applications](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.

**Known Issues Resolved from Previous Releases**
+ Fixed an issue where the `maximizeResourceAllocation` setting would not reserve enough memory for YARN ApplicationMaster daemons\.
+ Fixed an issue encountered with a custom DNS\. If any entries in `resolve.conf` precede the custom entries provided, then the custom entries are not resolvable\. This behavior was affected by clusters in a VPC where the default VPC name server is inserted as the top entry in `resolve.conf`\.
+ Fixed an issue where the default Python moved to version 2\.7 and boto was not installed for that version\.
+ Fixed an issue where YARN containers and Spark applications would generate a unique Ganglia round robin database \(rrd\) file, which resulted in the first disk attached to the instance filling up\. Because of this fix, YARN container level metrics have been disabled and Spark application level metrics have been disabled\.
+ Fixed an issue in log pusher where it would delete all empty log folders\. The effect was that the Hive CLI was not able to log because log pusher was removing the empty `user` folder under `/var/log/hive`\.
+ Fixed an issue affecting Hive imports, which affected partitioning and resulted in an error during import\.
+ Fixed an issue where EMRFS and s3\-dist\-cp did not properly handle bucket names that contain periods\.
+ Changed a behavior in EMRFS so that in versioning\-enabled buckets the `_$folder$` marker file is not continuously created, which may contribute to improved performance for versioning\-enabled buckets\.
+ Changed the behavior in EMRFS such that it does not use instruction files except for cases where client\-side encryption is enabled\. If you want to delete instruction files while using client\-side encryption, you can set the emrfs\-site\.xml property, `fs.s3.cse.cryptoStorageMode.deleteInstructionFiles.enabled`, to true\. 
+ Changed YARN log aggregation to retain logs at the aggregation destination for two days\. The default destination is your cluster HDFS storage\. If you want to change this duration, change the value of `yarn.log-aggregation.retain-seconds` using the `yarn-site` configuration classification when you create your cluster\. As always, you can save your application logs to Amazon S3 using the `log-uri` parameter when you create your cluster\.

**Patches Applied**
+ [HIVE\-9655](https://issues.apache.org/jira/browse/HIVE-9655)
+ [HIVE\-9183](https://issues.apache.org/jira/browse/HIVE-9183)
+ [HADOOP\-12810](https://issues.apache.org/jira/browse/HADOOP-12810)

**Release 4\.4\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.2\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.4\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.1\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.1\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.1\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.1\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.1\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.1\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.1\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.1\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.1\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hcatalog\-client | 1\.0\.0\-amzn\-3 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 1\.0\.0\-amzn\-3 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 1\.0\.0\-amzn\-3 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 1\.0\.0\-amzn\-3 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-3 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-3 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-5 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.1 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.136 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.136 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.6 | Apache Sqoop command\-line client\. | 
| webserver | 2\.4 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.6\-incubating | Web\-based notebook that enables interactive data analytics\. | 

**Release 4\.4\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.4\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j | Change values in HCatalog WebHCat's log4j\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| sqoop\-env | Change values in Sqoop's environment\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 

------
#### [ 4\.3\.0 ]

**Amazon EMR Release 4\.3\.0**
+ [Application Versions](#emr-430-app-versions)
+ [Release Notes](#emr-430-relnotes)
+ [Component Versions](#emr-430-components)
+ [Configuration Classifications](#emr-430-class)

**Release 4\.3\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), and [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.3.0.png)

**Release 4\.3\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.3\.0 release\.

Release date: January 19, 2016

**Features**
+ Upgraded to Hadoop 2\.7\.1
+ Upgraded to Spark 1\.6\.0
+ Upgraded Ganglia to 3\.7\.2 
+ Upgraded Presto to 0\.130
+ Amazon EMR made some changes to `spark.dynamicAllocation.enabled` when it is set to true; it is false by default\. When set to true, this affects the defaults set by the `maximizeResourceAllocation` setting:
  + If `spark.dynamicAllocation.enabled` is set to true, `spark.executor.instances` is not set by `maximizeResourceAllocation`\.
  + The `spark.driver.memory` setting is now configured based on the instance types in the cluster in a similar way to how `spark.executors.memory` is set\. However, because the Spark driver application may run on either the master or one of the core instances \(for example, in YARN client and cluster modes, respectively\), the `spark.driver.memory` setting is set based on the instance type of the smaller instance type between these two instance groups\.
  + The `spark.default.parallelism` setting is now set at twice the number of CPU cores available for YARN containers\. In previous releases, this was half that value\.
  + The calculations for the memory overhead reserved for Spark YARN processes were adjusted to be more accurate, resulting in a small increase in the total amount of memory available to Spark \(that is, `spark.executor.memory`\)\.

**Known Issues Resolved from the Previous Releases**
+ YARN log aggregation is now enabled by default\.
+ Fixed an issue where logs would not be pushed to Amazon S3 logs bucket for the cluster when YARN log aggregation was enabled\.
+ YARN container sizes now have a new minimum of 32 across all node types\.
+ Fixed an issue with Ganglia that caused excessive disk I/O on the master node in large clusters\.
+ Fixed an issue that prevented applications logs from being pushed to Amazon S3 when a cluster is shutting down\.
+ Fixed an issue in EMRFS CLI that caused certain commands to fail\.
+ Fixed an issue with Zeppelin that prevented dependencies from being loaded in the underlying SparkContext\.
+ Fixed an issue that resulted from issuing a resize attempting to add instances\. 
+ Fixed an issue in Hive where CREATE TABLE AS SELECT makes excessive list calls to Amazon S3\. 
+ Fixed an issue where large clusters would not provision properly when Hue, Oozie, and Ganglia are installed\.
+ Fixed an issue in s3\-dist\-cp where it would return a zero exit code even if it failed with an error\.

**Release 4\.3\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.1\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.3\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.7\.1\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.7\.1\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.7\.1\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.7\.1\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.7\.1\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.7\.1\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.7\.1\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.7\.1\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.7\.1\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hive\-client | 1\.0\.0\-amzn\-2 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-5 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.130 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.130 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.6\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.6\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.6\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.6\.0 | Apache Spark libraries needed by YARN slaves\. | 
| webserver | 2\.4 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.5\-incubating\-amzn\-1 | Web\-based notebook that enables interactive data analytics\. | 

**Release 4\.3\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.3\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 

------
#### [ 4\.2\.0 ]

**Amazon EMR Release 4\.2\.0**
+ [Application Versions](#emr-420-app-versions)
+ [Release Notes](#emr-420-relnotes)
+ [Component Versions](#emr-420-components)
+ [Configuration Classifications](#emr-420-class)

**Release 4\.2\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), and [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.3.0.png)

**Release 4\.2\.0 Release Notes**

The following release notes include information for the Amazon EMR 4\.2\.0 release\.

Release date: November 18, 2015

**Features**
+ Added Ganglia support
+ Upgraded to Spark 1\.5\.2
+ Upgraded to Presto 0\.125
+ Upgraded Oozie to 4\.2\.0
+ Upgraded Zeppelin to 0\.5\.5
+ Upgraded the AWS SDK for Java to 1\.10\.27

**Known Issues Resolved from the Previous Releases**
+ Fixed an issue with the EMRFS CLI where it did not use the default metadata table name\.
+ Fixed an issue encountered when using ORC\-backed tables in Amazon S3\.
+ Fixed an issue encountered with a Python version mismatch in the Spark configuration\.
+ Fixed an issue when a YARN node status fails to report because of DNS issues for clusters in a VPC\.
+ Fixed an issue encountered when YARN decommissioned nodes, resulting in hung applications or the inability to schedule new applications\.
+ Fixed an issue encountered when clusters terminated with status TIMED\_OUT\_STARTING\.
+ Fixed an issue encountered when including the EMRFS Scala dependency in other builds\. The Scala dependency has been removed\.

**Release 4\.2\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.0\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.2\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.6\.0 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.6\.0 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.5\.10 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.6\.0\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.6\.0\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.6\.0\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.6\.0\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.6\.0\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.6\.0\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.6\.0\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.6\.0\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.6\.0\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hive\-client | 1\.0\.0\-amzn\-1 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-5 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 4\.2\.0 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.125 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.125 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.5\.2 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.5\.2 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.5\.2 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.5\.2 | Apache Spark libraries needed by YARN slaves\. | 
| webserver | 2\.4 | Apache HTTP server\. | 
| zeppelin\-server | 0\.5\.5\-incubating\-amzn\-0 | Web\-based notebook that enables interactive data analytics\. | 

**Release 4\.2\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.2\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 

------
#### [ 4\.1\.0 ]

**Amazon EMR Release 4\.1\.0**
+ [Application Versions](#emr-410-app-versions)
+ [Release Notes](#emr-410-relnotes)
+ [Component Versions](#emr-410-components)
+ [Configuration Classifications](#emr-410-class)

**Release 4\.1\.0 Application Versions**

The following applications are supported in this release: [Hadoop](http://hadoop.apache.org/docs/current/), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [Mahout](http://mahout.apache.org/), [Oozie\-Sandbox](http://oozie.apache.org/), [Pig](http://pig.apache.org/), [Presto\-Sandbox](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), and [Zeppelin\-Sandbox](https://zeppelin.incubator.apache.org/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.3.0.png)

**Release 4\.1\.0 Release Notes**

Not available\.

**Release 4\.1\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.1\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.0\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.1\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| hadoop\-client | 2\.6\.0\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.6\.0\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.6\.0\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.6\.0\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.6\.0\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.6\.0\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.6\.0\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.6\.0\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.6\.0\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hive\-client | 1\.0\.0\-amzn\-1 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-1 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-1 | Service for accepting Hive queries as web requests\. | 
| hue\-server | 3\.7\.1\-amzn\-4 | Web application for analyzing data using Hadoop ecosystem applications | 
| mahout\-client | 0\.11\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| oozie\-client | 4\.0\.1 | Oozie command\-line client\. | 
| oozie\-server | 4\.0\.1 | Service for accepting Oozie workflow requests\. | 
| presto\-coordinator | 0\.119 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.119 | Service for executing pieces of a query\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.5\.0 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.5\.0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.5\.0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.5\.0 | Apache Spark libraries needed by YARN slaves\. | 
| zeppelin\-server | 0\.6\.0\-incubating\-SNAPSHOT | Web\-based notebook that enables interactive data analytics\. | 

**Release 4\.1\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.1\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
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
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| presto\-log | Change values in Presto's log\.properties file\. | 
| presto\-config | Change values in Presto's config\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 

------
#### [ 4\.0\.0 ]

**Amazon EMR Release 4\.0\.0**
+ [Application Versions](#emr-400-app-versions)
+ [Release Notes](#emr-400-relnotes)
+ [Component Versions](#emr-400-components)
+ [Configuration Classifications](#emr-400-class)

**Release 4\.0\.0 Application Versions**

The following applications are supported in this release: [Hadoop](http://hadoop.apache.org/docs/current/), [Hive](http://hive.apache.org/), [Mahout](http://mahout.apache.org/), [Pig](http://pig.apache.org/), and [Spark](https://spark.apache.org/docs/latest/)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-4.3.0.png)

**Release 4\.0\.0 Release Notes**

Not available\.

**Release 4\.0\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components need changes from community versions for Amazon EMR\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. For example, if a big\-data community component named `myapp-component` of version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-3`\.


| Component | Version | Description | 
| --- | --- | --- | 
| emr\-ddb | 3\.0\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.0\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.0\.0 | Distributed copy application optimized for Amazon S3\. | 
| emrfs | 2\.0\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| hadoop\-client | 2\.6\.0\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.6\.0\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-namenode | 2\.6\.0\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-httpfs\-server | 2\.6\.0\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-mapred | 2\.6\.0\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.6\.0\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.6\.0\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hive\-client | 1\.0\.0\-amzn\-0 | Hive command line client\. | 
| hive\-metastore\-server | 1\.0\.0\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server | 1\.0\.0\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| mahout\-client | 0\.10\.0 | Library for machine learning\. | 
| mysql\-server | 5\.5 | MySQL database server\. | 
| pig\-client | 0\.14\.0\-amzn\-0 | Pig command\-line client\. | 
| spark\-client | 1\.4\.1 | Spark command\-line clients\. | 
| spark\-history\-server | 1\.4\.1 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 1\.4\.1 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 1\.4\.1 | Apache Spark libraries needed by YARN slaves\. | 

**Release 4\.0\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-4\.0\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hive\-env | Change values in the Hive environment\. | 
| hive\-exec\-log4j | Change values in Hive's hive\-exec\-log4j\.properties file\. | 
| hive\-log4j | Change values in Hive's hive\-log4j\.properties file\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | 
| httpfs\-env | Change values in the HTTPFS environment\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 

------