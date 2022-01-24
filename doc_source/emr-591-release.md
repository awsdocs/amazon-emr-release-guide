# Amazon EMR release 5\.9\.1<a name="emr-591-release"></a>
+ [Application versions](#emr-591-app-versions)
+ [Release notes](#emr-591-relnotes)
+ [Component versions](#emr-591-components)
+ [Configuration classifications](#emr-591-class)

## Application versions<a name="emr-591-app-versions"></a>

The following applications are supported in this release: [https://flink.apache.org/](https://flink.apache.org/), [http://ganglia.info](http://ganglia.info), [http://hbase.apache.org/](http://hbase.apache.org/), [https://cwiki.apache.org/confluence/display/Hive/HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [http://gethue.com/](http://gethue.com/), [https://livy.incubator.apache.org/](https://livy.incubator.apache.org/), [http://mahout.apache.org/](http://mahout.apache.org/), [http://oozie.apache.org/](http://oozie.apache.org/), [https://phoenix.apache.org/](https://phoenix.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), [https://prestodb.io/](https://prestodb.io/), [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/), [http://sqoop.apache.org/](http://sqoop.apache.org/), [https://tez.apache.org/](https://tez.apache.org/), [https://zeppelin.incubator.apache.org/](https://zeppelin.incubator.apache.org/), and [https://zookeeper.apache.org](https://zookeeper.apache.org)\.

The table below lists the application versions available in this release of Amazon EMR and the application versions in the preceding three Amazon EMR releases \(when applicable\)\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following topics:
+ [Application versions in Amazon EMR 6\.x releases](emr-release-app-versions-6.x.md)
+ [Application versions in Amazon EMR 5\.x releases](emr-release-app-versions-5.x.md)
+ [Application versions in Amazon EMR 4\.x releases](emr-release-app-versions-4.x.md)


**Application version information**  

|  | emr\-5\.9\.1 | emr\-5\.9\.0 | emr\-5\.8\.3 | emr\-5\.8\.2 | 
| --- | --- | --- | --- | --- | 
| AWS SDK for Java | 1\.11\.183 | 1\.11\.183 | 1\.11\.160 | 1\.11\.160 | 
| Flink | 1\.3\.2 | 1\.3\.2 | 1\.3\.1 | 1\.3\.1 | 
| Ganglia | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 
| HBase | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 1\.3\.1 | 
| HCatalog | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | 
| Hadoop | 2\.7\.3 | 2\.7\.3 | 2\.7\.3 | 2\.7\.3 | 
| Hive | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | 2\.3\.0 | 
| Hudi |  \-  |  \-  |  \-  |  \-  | 
| Hue | 4\.0\.1 | 4\.0\.1 | 3\.12\.0 | 3\.12\.0 | 
| Iceberg |  \-  |  \-  |  \-  |  \-  | 
| JupyterEnterpriseGateway |  \-  |  \-  |  \-  |  \-  | 
| JupyterHub |  \-  |  \-  |  \-  |  \-  | 
| Livy | 0\.4\.0 | 0\.4\.0 |  \-  |  \-  | 
| MXNet |  \-  |  \-  |  \-  |  \-  | 
| Mahout | 0\.13\.0 | 0\.13\.0 | 0\.13\.0 | 0\.13\.0 | 
| Oozie | 4\.3\.0 | 4\.3\.0 | 4\.3\.0 | 4\.3\.0 | 
| Phoenix | 4\.11\.0 | 4\.11\.0 | 4\.11\.0 | 4\.11\.0 | 
| Pig | 0\.17\.0 | 0\.17\.0 | 0\.16\.0 | 0\.16\.0 | 
| Presto | 0\.184 | 0\.184 | 0\.170 | 0\.170 | 
| Spark | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 2\.2\.0 | 
| Sqoop | 1\.4\.6 | 1\.4\.6 | 1\.4\.6 | 1\.4\.6 | 
| TensorFlow |  \-  |  \-  |  \-  |  \-  | 
| Tez | 0\.8\.4 | 0\.8\.4 | 0\.8\.4 | 0\.8\.4 | 
| Trino \(PrestoSQL\) |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin | 0\.7\.2 | 0\.7\.2 | 0\.7\.2 | 0\.7\.2 | 
| ZooKeeper | 3\.4\.10 | 3\.4\.10 | 3\.4\.10 | 3\.4\.10 | 

## Release notes<a name="emr-591-relnotes"></a>

This is a patch release to add AWS Signature Version 4 authentication for requests to Amazon S3\. All applications and components are the same as the previous Amazon EMR release version\.

**Important**  
In this release version, Amazon EMR uses AWS Signature Version 4 exclusively to authenticate requests to Amazon S3\. For more information, see [Whats New](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew.html)\.

## Component versions<a name="emr-591-components"></a>

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


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

## Configuration classifications<a name="emr-591-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.


**emr\-5\.9\.1 classifications**  

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