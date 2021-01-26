# Amazon EMR 6\.x Release Versions<a name="emr-release-6x"></a>

Each tab below lists application versions, release notes, component versions, and configuration classifications available in each Amazon EMR 6\.x release version\.

Amazon EMR 6\.x series supports Apache Hadoop 3\. For a comprehensive diagram of application versions in every release, see [Application Versions in Amazon EMR 6\.x Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-6x.png)\.

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

------
#### [ 6\.2\.0 \(Latest\) ]<a name="emr-620-release"></a>

**Amazon EMR Release 6\.2\.0**
+ [Application Versions](#emr-620-app-versions)
+ [Release Notes](#emr-620-relnotes)
+ [Component Versions](#emr-620-components)
+ [Configuration Classifications](#emr-620-class)

**6\.2\.0 Application Versions**

The following applications are supported in this release: [JupyterEnterpriseGateway](https://jupyter-enterprise-gateway.readthedocs.io/en/latest/), [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [PrestoSQL](https://prestosql.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 6\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-6x.png)
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-6.2.0.png)

**6\.2\.0 Release Notes**

The following release notes include information for Amazon EMR release version 6\.2\.0\. Changes are relative to 6\.1\.0\.

Initial release date: Dec 09, 2020

Last updated date: Jan 08, 2021

**Supported Applications**
+ AWS SDK for Java version 1\.11\.828
+ emr\-record\-server version 1\.7\.0
+ Flink version 1\.11\.2
+ Ganglia version 3\.7\.2
+ Hadoop version 3\.2\.1\-amzn\-1
+ HBase version 2\.2\.6
+ HBase\-operator\-tools 1\.0\.0
+ HCatalog version 3\.1\.2\-amzn\-0
+ Hive version 3\.1\.2\-amzn\-3
+ Hudi version 0\.6\.0\-amzn\-1
+ Hue version 4\.8\.0
+ JupyterHub version 1\.1\.0
+ Livy version 0\.7\.0
+ MXNet version 1\.7\.0
+ Oozie version 5\.2\.0
+ Phoenix version 5\.0\.0
+ Pig version 0\.17\.0
+ Presto version 0\.238\.3\-amzn\-1
+ PrestoSQL version 343
+ Spark version 3\.0\.1
+ spark\-rapids 0\.2\.0
+ TensorFlow version 2\.3\.1
+ Zeppelin version 0\.9\.0\-preview1
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.16\.0

**New Features**
+ HBase: Removed rename in commit phase and added persistent HFile tracking\. See [Persistent HFile Tracking](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-hfile-tracking) in the *Amazon EMR Release Guide*\.
+ HBase: Backported [Create a config that forces to cache blocks on compaction](https://issues.apache.org/jira/browse/HBASE-23066)\.
+ PrestoDB: Improvements to Dynamic Partition Pruning\. Rule\-based Join Reorder works on non\-partitioned data\.

**Changes, Enhancements, and Resolved Issues**
+ Spark: Performance improvements in Spark runtime\.

**Known Issues**
+ Amazon EMR 6\.2\.0 Maven artifacts are not published\. They will be published with a future release of Amazon EMR\.
+ Persistent HFile tracking using the HBase storefile system table does not support the HBase region replication feature\. For more information about HBase region replication, see [Timeline\-consistent High Available Reads](http://hbase.apache.org/book.html#arch.timelineconsistent.reads)\.
+ Amazon EMR 6\.x and EMR 5\.x Hive bucketing version differences

  EMR 5\.x uses OOS Apacke Hive 2, while in EMR 6\.x uses OOS Apache Hive 3\. The open source Hive2 uses Bucketing version 1, while open source Hive3 uses Bucketing version 2\. This bucketing version difference between Hive 2 \(EMR 5\.x\) and Hive 3 \(EMR 6\.x\) means Hive bucketing hashing functions differently\. See the example below\.

  The following table is an example created in EMR 6\.x and EMR 5\.x, respectively\.

  ```
  -- Using following LOCATION in EMR 6.x
  CREATE TABLE test_bucketing (id INT, desc STRING)
  PARTITIONED BY (day STRING)
  CLUSTERED BY(id) INTO 128 BUCKETS
  LOCATION 's3://your-own-s3-bucket/emr-6-bucketing/';
  
  -- Using following LOCATION in EMR 5.x 
  LOCATION 's3://your-own-s3-bucket/emr-5-bucketing/';
  ```

  Inserting the same data in both EMR 6\.x and EMR 5\.x\.

  ```
  INSERT INTO test_bucketing PARTITION (day='01') VALUES(66, 'some_data');
  INSERT INTO test_bucketing PARTITION (day='01') VALUES(200, 'some_data');
  ```

  Checking the S3 location, shows the bucketing file name is different, because the hashing function is different between EMR 6\.x \(Hive 3\) and EMR 5\.x \(Hive 2\)\.

  ```
  [hadoop@ip-10-0-0-122 ~]$ aws s3 ls s3://your-own-s3-bucket/emr-6-bucketing/day=01/
  2020-10-21 20:35:16         13 000025_0
  2020-10-21 20:35:22         14 000121_0
  [hadoop@ip-10-0-0-122 ~]$ aws s3 ls s3://your-own-s3-bucket/emr-5-bucketing/day=01/
  2020-10-21 20:32:07         13 000066_0
  2020-10-21 20:32:51         14 000072_0
  ```

  You can also see the version difference by running the following command in Hive CLI in EMR 6\.x\. Note that it returns bucketing version 2\.

  ```
  hive> DESCRIBE FORMATTED test_bucketing;
  ...
  Table Parameters:
      bucketing_version       2
  ...
  ```

**6\.2\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.4\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.16\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 3\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.5\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-notebook\-env | 1\.0\.0 | Conda env for emr notebook which includes jupyter enterprise gateway | 
| emr\-s3\-dist\-cp | 2\.16\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 2\.0\.0 | EMR S3Select Connector | 
| emrfs | 2\.44\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.11\.2 | Apache Flink command line client scripts and applications\. | 
| flink\-jobmanager\-config | 1\.11\.2 | Managing resources on EMR nodes for Apache Flink JobManager\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 3\.2\.1\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 3\.2\.1\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 3\.2\.1\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 3\.2\.1\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-hdfs\-journalnode | 3\.2\.1\-amzn\-2 | HDFS service for managing the Hadoop filesystem journal on HA clusters\. | 
| hadoop\-httpfs\-server | 3\.2\.1\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 3\.2\.1\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 3\.2\.1\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 3\.2\.1\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 3\.2\.1\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 3\.2\.1\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 2\.2\.6\-amzn\-0 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 2\.2\.6\-amzn\-0 | Service for serving one or more HBase regions\. | 
| hbase\-client | 2\.2\.6\-amzn\-0 | HBase command\-line client\. | 
| hbase\-rest\-server | 2\.2\.6\-amzn\-0 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 2\.2\.6\-amzn\-0 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 3\.1\.2\-amzn\-3 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 3\.1\.2\-amzn\-3 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 3\.1\.2\-amzn\-3 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 3\.1\.2\-amzn\-3 | Hive command line client\. | 
| hive\-hbase | 3\.1\.2\-amzn\-3 | Hive\-hbase client\. | 
| hive\-metastore\-server | 3\.1\.2\-amzn\-3 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 3\.1\.2\-amzn\-3 | Service for accepting Hive queries as web requests\. | 
| hudi | 0\.6\.0\-amzn\-1 | Incremental processing framework to power data pipline at low latency and high efficiency\. | 
| hudi\-presto | 0\.6\.0\-amzn\-1 | Bundle library for running Presto with Hudi\. | 
| hudi\-prestosql | 0\.6\.0\-amzn\-1 | Bundle library for running PrestoSQL with Hudi\. | 
| hudi\-spark | 0\.6\.0\-amzn\-1 | Bundle library for running Spark with Hudi\. | 
| hue\-server | 4\.8\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 1\.1\.0 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.7\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mxnet | 1\.7\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mariadb\-server | 5\.5\.64\+ | MariaDB database server\. | 
| nvidia\-cuda | 10\.1\.243 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.2\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 4\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 5\.0\.0\-HBase\-2\.0 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 5\.0\.0\-HBase\-2\.0 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.238\.3\-amzn\-1 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.238\.3\-amzn\-1 | Service for executing pieces of a query\. | 
| presto\-client | 0\.238\.3\-amzn\-1 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| prestosql\-coordinator | 343 | Service for accepting queries and managing query execution among prestosql\-workers\. | 
| prestosql\-worker | 343 | Service for executing pieces of a query\. | 
| prestosql\-client | 343 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.3 | The R Project for Statistical Computing | 
| ranger\-kms\-server | 2\.0\.0 | Apache Ranger Key Management System | 
| spark\-client | 3\.0\.1\-amzn\-0 | Spark command\-line clients\. | 
| spark\-history\-server | 3\.0\.1\-amzn\-0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 3\.0\.1\-amzn\-0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 3\.0\.1\-amzn\-0 | Apache Spark libraries needed by YARN slaves\. | 
| spark\-rapids | 0\.2\.0 | Nvidia Spark RAPIDS plugin that accelerates Apache Spark with GPUs\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 2\.3\.1 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.2 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.41\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.9\.0\-preview1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.14 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.14 | ZooKeeper command line client\. | 

**6\.2\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-6\.2\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-executor | Change values in Hadoop YARN's container\-executor\.cfg file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| docker\-conf | Change docker related settings\. | 
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
| hdfs\-env | Change values in the HDFS environment\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive | Amazon EMR\-curated settings for Apache Hive\. | 
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
| hudi\-env | Change values in the Hudi environment\. | 
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
| prestosql\-log | Change values in Presto's log\.properties file\. | 
| prestosql\-config | Change values in Presto's config\.properties file\. | 
| prestosql\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| prestosql\-env | Change values in Presto's presto\-env\.sh file\. | 
| prestosql\-node | Change values in PrestoSQL's node\.properties file\. | 
| prestosql\-connector\-blackhole | Change values in PrestoSQL's blackhole\.properties file\. | 
| prestosql\-connector\-cassandra | Change values in PrestoSQL's cassandra\.properties file\. | 
| prestosql\-connector\-hive | Change values in PrestoSQL's hive\.properties file\. | 
| prestosql\-connector\-jmx | Change values in PrestoSQL's jmx\.properties file\. | 
| prestosql\-connector\-kafka | Change values in PrestoSQL's kafka\.properties file\. | 
| prestosql\-connector\-localfile | Change values in PrestoSQL's localfile\.properties file\. | 
| prestosql\-connector\-memory | Change values in PrestoSQL's memory\.properties file\. | 
| prestosql\-connector\-mongodb | Change values in PrestoSQL's mongodb\.properties file\. | 
| prestosql\-connector\-mysql | Change values in PrestoSQL's mysql\.properties file\. | 
| prestosql\-connector\-postgresql | Change values in PrestoSQL's postgresql\.properties file\. | 
| prestosql\-connector\-raptor | Change values in PrestoSQL's raptor\.properties file\. | 
| prestosql\-connector\-redis | Change values in PrestoSQL's redis\.properties file\. | 
| prestosql\-connector\-redshift | Change values in PrestoSQL's redshift\.properties file\. | 
| prestosql\-connector\-tpch | Change values in PrestoSQL's tpch\.properties file\. | 
| prestosql\-connector\-tpcds | Change values in PrestoSQL's tpcds\.properties file\. | 
| ranger\-kms\-dbks\-site | Change values in dbks\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-site | Change values in ranger\-kms\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-env | Change values in the Ranger KMS environment\. | 
| ranger\-kms\-log4j | Change values in kms\-log4j\.properties file of Ranger KMS\. | 
| ranger\-kms\-db\-ca | Change values for CA file on S3 for MySQL SSL connection with Ranger KMS\. | 
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
#### [ 6\.1\.0 ]<a name="emr-610-release"></a>

**Amazon EMR Release 6\.1\.0**
+ [Application Versions](#emr-610-app-versions)
+ [Release Notes](#emr-610-relnotes)
+ [Component Versions](#emr-610-components)
+ [Configuration Classifications](#emr-610-class)

**6\.1\.0 Application Versions**

The following applications are supported in this release: [Flink](https://flink.apache.org/), [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Pig](http://pig.apache.org/), [Presto](https://prestodb.io/), [PrestoSQL](https://prestosql.io/), [Spark](https://spark.apache.org/docs/latest/), [Sqoop](http://sqoop.apache.org/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 6\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-6x.png)
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-6.1.0.png)

**6\.1\.0 Release Notes**

The following release notes include information for Amazon EMR release version 6\.1\.0\. Changes are relative to 6\.0\.0\.

Initial release date: Sept 04, 2020

Last updated date: Oct 15, 2020

**Supported Applications**
+ AWS SDK for Java version 1\.11\.828
+ Flink version 1\.11\.0
+ Ganglia version 3\.7\.2
+ Hadoop version 3\.2\.1\-amzn\-1
+ HBase version 2\.2\.5
+ HBase\-operator\-tools 1\.0\.0
+ HCatalog version 3\.1\.2\-amzn\-0
+ Hive version 3\.1\.2\-amzn\-1
+ Hudi version 0\.5\.2\-incubating
+ Hue version 4\.7\.1
+ JupyterHub version 1\.1\.0
+ Livy version 0\.7\.0
+ MXNet version 1\.6\.0
+ Oozie version 5\.2\.0
+ Phoenix version 5\.0\.0
+ Presto version 0\.232
+ PrestoSQL version 338
+ Spark version 3\.0\.0
+ TensorFlow version 2\.1\.0
+ Zeppelin version 0\.9\.0\-preview1
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.14\.0

**New Features**
+ ARM instance types are supported starting with Amazon EMR version 5\.30\.0 and Amazon EMR version 6\.1\.0\.
+ M6g general purpose instance types are supported starting with Amazon EMR versions 6\.1\.0 and 5\.31\.0\. For more information, see [Supported Instance Types](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-supported-instance-types.html) in the *Amazon EMR Management Guide*\.
+ The EC2 placement group feature is supported starting with Amazon EMR version 5\.23\.0 as an option for multiple master node clusters\. Currently, only master node types are supported by the placement group feature, and the `SPREAD` strategy is applied to those master nodes\. The `SPREAD` strategy places a small group of instances across separate underlying hardware to guard against the loss of multiple master nodes in the event of a hardware failure\. For more information, see [EMR Integration with EC2 Placement Group](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-placementgroup.html) in the *Amazon EMR Management Guide*\.
+ Managed Scaling – With Amazon EMR version 6\.1\.0, you can enable EMR managed scaling to automatically increase or decrease the number of instances or units in your cluster based on workload\. EMR continuously evaluates cluster metrics to make scaling decisions that optimize your clusters for cost and speed\. Managed Scaling is also available on Amazon EMR version 5\.30\.0 and later, except 6\.0\.0\. For more information, see [Scaling Cluster Resources](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scale-on-demand.html) in the *Amazon EMR Management Guide*\.
+ PrestoSQL version 338 is supported with EMR 6\.1\.0\. For more information, see [Presto](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-presto.html)\.
  + PrestoSQL is supported on EMR 6\.1\.0 and later versions only, not on EMR 6\.0\.0 or EMR 5\.x\.
  + The application name, `Presto` continues to be used to install PrestoDB on clusters\. To install PrestoSQL on clusters, use the application name `PrestoSQL`\.
  + You can install either PrestoDB or PrestoSQL, but you cannot install both on a single cluster\. If both PrestoDB and PrestoSQL are specified when attempting to create a cluster, a validation error occurs and the cluster creation request fails\.
  + PrestoSQL is supported on both single\-master and muti\-master clusters\. On multi\-master clusters, an external Hive metastore is required to run PrestoSQL or PrestoDB\. See [Supported Applications in an EMR Cluster with Multiple Master Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-applications.html#emr-plan-ha-applications-list)\.
+ ECR auto authentication support on Apache Hadoop and Apache Spark with Docker: Spark users can use ï»¿Dockerï»¿ images from ï»¿Docker Hubï»¿ and ï»¿Amazon Elastic Container Registry \(Amazon ECR\)ï»¿ to define environment and library dependencies\.

  [Configure Docker](emr/latest/ManagementGuide/emr-plan-docker.html) and [Run Spark Applications with Docker Using Amazon EMR 6\.x](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-docker.html)\.
+ EMR supports Apache Hive ACID transactions: Amazon EMR 6\.1\.0 adds support for Hive ACID transactions so it complies with the ACID properties of a database\. With this feature, you can run INSERT, UPDATE, DELETE, and MERGE operations in Hive managed tables with data in Amazon Simple Storage Service \(Amazon S3\)\. This is a key feature for use cases like streaming ingestion, data restatement, bulk updates using MERGE, and slowly changing dimensions\. For more information, including configuration examples and use cases, see [Amazon EMR supports Apache Hive ACID transactions](https://aws.amazon.com/blogs/big-data/amazon-emr-supports-apache-hive-acid-transactions)\.

**Changes, Enhancements, and Resolved Issues**
+ Apache Flink is not supported on EMR 6\.0\.0, but it is supported on EMR 6\.1\.0 with Flink 1\.11\.0\. This is the first version of Flink to officially support Hadoop 3\. See [Apache Flink 1\.11\.0 Release Announcement](https://flink.apache.org/news/2020/07/06/release-1.11.0.html)\.
+ Ganglia has been removed from default EMR 6\.1\.0 package bundles\.

**Known Issues**
+ If you set custom garbage collection configuration with `spark.driver.extraJavaOptions` and `spark.executor.extraJavaOptions`, this will result in driver/executor launch failure with EMR 6\.1 due to conflicting garbage collection configuration\. With EMR Release 6\.1\.0, you should specify custom Spark garbage collection configuration for drivers and executors with the properties `spark.driver.defaultJavaOptions` and `spark.executor.defaultJavaOptions` instead\. Read more in [Apache Spark Runtime Environment](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) and [Configuring Spark Garbage Collection on Amazon EMR 6\.1\.0](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-configure.html#spark-gc-config)\.
+ Using Pig with Oozie \(and within Hue, since Hue uses Oozie actions to run Pig scripts\), generates an error that a native\-lzo library cannot be loaded\. This error message is informational and does not block Pig from running\.
+ Hudi Concurrency Support: Currently Hudi doesnâ€™t support concurrent writes to a single Hudi table\. In addition, Hudi rolls back any changes being done by in\-progress writers before allowing a new writer to start\. Concurrent writes can interfere with this mechanism and introduce race conditions, which can lead to data corruption\. You should ensure that as part of your data processing workflow, there is only a single Hudi writer operating against a Hudi table at any time\. Hudi does support multiple concurrent readers operating against the same Hudi table\.
+ Known issue in clusters with multiple master nodes and Kerberos authentication

  If you run clusters with multiple master nodes and Kerberos authentication in EMR releases 5\.20\.0 and later, you may encounter problems with cluster operations such as scale down or step submission, after the cluster has been running for some time\. The time period depends on the Kerberos ticket validity period that you defined\. The scale\-down problem impacts both automatic scale\-down and explicit scale down requests that you submitted\. Additional cluster operations can also be impacted\. 

  Workaround:
  + SSH as `hadoop` user to the lead master node of the EMR cluster with multiple master nodes\.
  +  Run the following command to renew Kerberos ticket for `hadoop` user\. 

    ```
    kinit -kt <keytab_file> <principal>
    ```

    Typically, the keytab file is located at `/etc/hadoop.keytab` and the principal is in the form of `hadoop/<hostname>@<REALM>`\.
**Note**  
This workaround will be effective for the time period the Kerberos ticket is valid\. This duration is 10 hours by default, but can configured by your Kerberos settings\. You must re\-run the above command once the Kerberos ticket expires\.

**6\.1\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.3\.0 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.14\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 3\.1\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.5\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.14\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 2\.0\.0 | EMR S3Select Connector | 
| emrfs | 2\.42\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.11\.0 | Apache Flink command line client scripts and applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 3\.2\.1\-amzn\-1 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 3\.2\.1\-amzn\-1 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 3\.2\.1\-amzn\-1 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 3\.2\.1\-amzn\-1 | HDFS service for tracking file names and block locations\. | 
| hadoop\-hdfs\-journalnode | 3\.2\.1\-amzn\-1 | HDFS service for managing the Hadoop filesystem journal on HA clusters\. | 
| hadoop\-httpfs\-server | 3\.2\.1\-amzn\-1 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 3\.2\.1\-amzn\-1 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 3\.2\.1\-amzn\-1 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 3\.2\.1\-amzn\-1 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 3\.2\.1\-amzn\-1 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 3\.2\.1\-amzn\-1 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 2\.2\.5 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 2\.2\.5 | Service for serving one or more HBase regions\. | 
| hbase\-client | 2\.2\.5 | HBase command\-line client\. | 
| hbase\-rest\-server | 2\.2\.5 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 2\.2\.5 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 3\.1\.2\-amzn\-2 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 3\.1\.2\-amzn\-2 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 3\.1\.2\-amzn\-2 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 3\.1\.2\-amzn\-2 | Hive command line client\. | 
| hive\-hbase | 3\.1\.2\-amzn\-2 | Hive\-hbase client\. | 
| hive\-metastore\-server | 3\.1\.2\-amzn\-2 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 3\.1\.2\-amzn\-2 | Service for accepting Hive queries as web requests\. | 
| hudi | 0\.5\.2\-incubating\-amzn\-2 | Incremental processing framework to power data pipline at low latency and high efficiency\. | 
| hudi\-presto | 0\.5\.2\-incubating\-amzn\-2 | Bundle library for running Presto with Hudi\. | 
| hudi\-prestosql | 0\.5\.2\-incubating\-amzn\-2 | Bundle library for running PrestoSQL with Hudi\. | 
| hudi\-spark | 0\.5\.2\-incubating\-amzn\-2 | Bundle library for running Spark with Hudi\. | 
| hue\-server | 4\.7\.1 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 1\.1\.0 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.7\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mxnet | 1\.6\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mariadb\-server | 5\.5\.64\+ | MariaDB database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.2\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.2\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 4\.3\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 5\.0\.0\-HBase\-2\.0 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 5\.0\.0\-HBase\-2\.0 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.232 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.232 | Service for executing pieces of a query\. | 
| presto\-client | 0\.232 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| prestosql\-coordinator | 338 | Service for accepting queries and managing query execution among prestosql\-workers\. | 
| prestosql\-worker | 338 | Service for executing pieces of a query\. | 
| prestosql\-client | 338 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 3\.4\.3 | The R Project for Statistical Computing | 
| ranger\-kms\-server | 2\.0\.0 | Apache Ranger Key Management System | 
| spark\-client | 3\.0\.0\-amzn\-0 | Spark command\-line clients\. | 
| spark\-history\-server | 3\.0\.0\-amzn\-0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 3\.0\.0\-amzn\-0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 3\.0\.0\-amzn\-0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 2\.1\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.2 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.41\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.9\.0\-preview1 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.14 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.14 | ZooKeeper command line client\. | 

**6\.1\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-6\.1\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-executor | Change values in Hadoop YARN's container\-executor\.cfg file\. | 
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
| hdfs\-env | Change values in the HDFS environment\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive | Amazon EMR\-curated settings for Apache Hive\. | 
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
| hudi\-env | Change values in the Hudi environment\. | 
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
| prestosql\-log | Change values in Presto's log\.properties file\. | 
| prestosql\-config | Change values in Presto's config\.properties file\. | 
| prestosql\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | 
| prestosql\-env | Change values in Presto's presto\-env\.sh file\. | 
| prestosql\-node | Change values in PrestoSQL's node\.properties file\. | 
| prestosql\-connector\-blackhole | Change values in PrestoSQL's blackhole\.properties file\. | 
| prestosql\-connector\-cassandra | Change values in PrestoSQL's cassandra\.properties file\. | 
| prestosql\-connector\-hive | Change values in PrestoSQL's hive\.properties file\. | 
| prestosql\-connector\-jmx | Change values in PrestoSQL's jmx\.properties file\. | 
| prestosql\-connector\-kafka | Change values in PrestoSQL's kafka\.properties file\. | 
| prestosql\-connector\-localfile | Change values in PrestoSQL's localfile\.properties file\. | 
| prestosql\-connector\-memory | Change values in PrestoSQL's memory\.properties file\. | 
| prestosql\-connector\-mongodb | Change values in PrestoSQL's mongodb\.properties file\. | 
| prestosql\-connector\-mysql | Change values in PrestoSQL's mysql\.properties file\. | 
| prestosql\-connector\-postgresql | Change values in PrestoSQL's postgresql\.properties file\. | 
| prestosql\-connector\-raptor | Change values in PrestoSQL's raptor\.properties file\. | 
| prestosql\-connector\-redis | Change values in PrestoSQL's redis\.properties file\. | 
| prestosql\-connector\-redshift | Change values in PrestoSQL's redshift\.properties file\. | 
| prestosql\-connector\-tpch | Change values in PrestoSQL's tpch\.properties file\. | 
| prestosql\-connector\-tpcds | Change values in PrestoSQL's tpcds\.properties file\. | 
| ranger\-kms\-dbks\-site | Change values in dbks\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-site | Change values in ranger\-kms\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-env | Change values in the Ranger KMS environment\. | 
| ranger\-kms\-log4j | Change values in kms\-log4j\.properties file of Ranger KMS\. | 
| ranger\-kms\-db\-ca | Change values for CA file on S3 for MySQL SSL connection with Ranger KMS\. | 
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
#### [ 6\.0\.0 ]<a name="emr-600-release"></a>

**Amazon EMR Release 6\.0\.0**
+ [Application Versions](#emr-600-app-versions)
+ [Release Notes](#emr-600-relnotes)
+ [Component Versions](#emr-600-components)
+ [Configuration Classifications](#emr-600-class)

**6\.0\.0 Application Versions**

The following applications are supported in this release: [Ganglia](http://ganglia.info), [Hadoop](http://hadoop.apache.org/docs/current/), [HBase](http://hbase.apache.org/), [HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [Hive](http://hive.apache.org/), [Hue](http://gethue.com/), [JupyterHub](https://jupyterhub.readthedocs.io/en/latest/#), [Livy](https://livy.incubator.apache.org/), [MXNet](https://mxnet.incubator.apache.org/), [Oozie](http://oozie.apache.org/), [Phoenix](https://phoenix.apache.org/), [Presto](https://prestodb.io/), [Spark](https://spark.apache.org/docs/latest/), [TensorFlow](https://www.tensorflow.org/), [Tez](https://tez.apache.org/), [Zeppelin](https://zeppelin.incubator.apache.org/), and [ZooKeeper](https://zookeeper.apache.org)\.

The diagram below depicts the application versions available in this release of Amazon EMR and the application versions in the preceding four Amazon EMR releases\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following diagrams:
+ [Application Versions for 6\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-6x.png)
+ [Application Versions for 5\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions for 4\.x Series Amazon EMR Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-4x.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-6.0.0.png)

**6\.0\.0 Release Notes**

The following release notes include information for Amazon EMR release version 6\.0\.0\.

Initial release date: March 10, 2020

**Supported Applications**
+ AWS SDK for Java version 1\.11\.711
+ Ganglia version 3\.7\.2
+ Hadoop version 3\.2\.1
+ HBase version 2\.2\.3
+ HCatalog version 3\.1\.2
+ Hive version 3\.1\.2
+ Hudi version 0\.5\.0\-incubating
+ Hue version 4\.4\.0
+ JupyterHub version 1\.0\.0
+ Livy version 0\.6\.0
+ MXNet version 1\.5\.1
+ Oozie version 5\.1\.0
+ Phoenix version 5\.0\.0
+ Presto version 0\.230
+ Spark version 2\.4\.4
+ TensorFlow version 1\.14\.0
+ Zeppelin version 0\.9\.0\-SNAPSHOT
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.14\.0

**Note**  
Flink, Sqoop, Pig, and Mahout are not available in Amazon EMR version 6\.0\.0\. 

**New Features**
+ YARN Docker Runtime Support \- YARN applications, such as Spark jobs, can now run in the context of a Docker container\. This allows you to easily define dependencies in a Docker image without the need to install custom libraries on your Amazon EMR cluster\. For more information, see [Configure Docker Integration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html) and [Run Spark applications with Docker using Amazon EMR 6\.0\.0](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-docker.html)\.
+ Hive LLAP Support \- Hive now supports the LLAP execution mode for improved query performance\. For more information, see [Using Hive LLAP](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive-llap.html)\.

**Changes, Enhancements, and Resolved Issues**
+ Amazon Linux
  + Amazon Linux 2 is the operating system for the EMR 6\.x release series\.
  + `systemd` is used for service management instead of `upstart` used in Amazon Linux 1\.
+ Java Development Kit \(JDK\)
  + Coretto JDK 8 is the default JDK for the EMR 6\.x release series\.
+ Scala
  + Scala 2\.12 is used with Apache Spark and Apache Livy\.
+ Python 3
  + Python 3 is now the default version of Python in EMR\.
+ YARN node labels
  + Beginning with Amazon EMR 6\.x release series, the YARN node labels feature is disabled by default\. The application master processes can run on both core and task nodes by default\. You can enable the YARN node labels feature by configuring following properties: `yarn.node-labels.enabled` and `yarn.node-labels.am.default-node-label-expression`\. For more information, see [Understanding Master, Core, and Task Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-master-core-task-nodes.html)\.

**Known Issues**
+ Spark interactive shell, including PySpark, SparkR, and spark\-shell, does not support using Docker with additional libraries\.
+ To use Python 3 with Amazon EMR version 6\.0\.0, you must add `PATH` to `yarn.nodemanager.env-whitelist`\.
+ The Live Long and Process \(LLAP\) functionality is not supported when you use the AWS Glue Data Catalog as the metastore for Hive\.
+ When using Amazon EMR 6\.0\.0 with Spark and Docker integration, you need to configure the instances in your cluster with the same instance type and the same amount of EBS volumes to avoid failure when submitting a Spark job with Docker runtime\.
+ In Amazon EMR 6\.0\.0, HBase on Amazon S3 storage mode is impacted by the [HBASE\-24286](https://issues.apache.org/jira/browse/HBASE-24286)\. issue\. HBase master cannot initialize when the cluster is created using existing S3 data\.
+ Known issue in clusters with multiple master nodes and Kerberos authentication

  If you run clusters with multiple master nodes and Kerberos authentication in EMR releases 5\.20\.0 and later, you may encounter problems with cluster operations such as scale down or step submission, after the cluster has been running for some time\. The time period depends on the Kerberos ticket validity period that you defined\. The scale\-down problem impacts both automatic scale\-down and explicit scale down requests that you submitted\. Additional cluster operations can also be impacted\. 

  Workaround:
  + SSH as `hadoop` user to the lead master node of the EMR cluster with multiple master nodes\.
  +  Run the following command to renew Kerberos ticket for `hadoop` user\. 

    ```
    kinit -kt <keytab_file> <principal>
    ```

    Typically, the keytab file is located at `/etc/hadoop.keytab` and the principal is in the form of `hadoop/<hostname>@<REALM>`\.
**Note**  
This workaround will be effective for the time period the Kerberos ticket is valid\. This duration is 10 hours by default, but can configured by your Kerberos settings\. You must re\-run the above command once the Kerberos ticket expires\.

**6\.0\.0 Component Versions**

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.2\.6 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.14\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 3\.0\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.5\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-s3\-dist\-cp | 2\.14\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.5\.0 | EMR S3Select Connector | 
| emrfs | 2\.39\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 3\.2\.1\-amzn\-0 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 3\.2\.1\-amzn\-0 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 3\.2\.1\-amzn\-0 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 3\.2\.1\-amzn\-0 | HDFS service for tracking file names and block locations\. | 
| hadoop\-hdfs\-journalnode | 3\.2\.1\-amzn\-0 | HDFS service for managing the Hadoop filesystem journal on HA clusters\. | 
| hadoop\-httpfs\-server | 3\.2\.1\-amzn\-0 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 3\.2\.1\-amzn\-0 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 3\.2\.1\-amzn\-0 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 3\.2\.1\-amzn\-0 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 3\.2\.1\-amzn\-0 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 3\.2\.1\-amzn\-0 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 2\.2\.3 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 2\.2\.3 | Service for serving one or more HBase regions\. | 
| hbase\-client | 2\.2\.3 | HBase command\-line client\. | 
| hbase\-rest\-server | 2\.2\.3 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 2\.2\.3 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 3\.1\.2\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 3\.1\.2\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 3\.1\.2\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 3\.1\.2\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 3\.1\.2\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 3\.1\.2\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 3\.1\.2\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hudi | 0\.5\.0\-incubating\-amzn\-1 | Incremental processing framework to power data pipline at low latency and high efficiency\. | 
| hudi\-presto | 0\.5\.0\-incubating\-amzn\-1 | Bundle library for running Presto with Hudi\. | 
| hue\-server | 4\.4\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 1\.0\.0 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.6\.0\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.12\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mxnet | 1\.5\.1 | A flexible, scalable, and efficient library for deep learning\. | 
| mariadb\-server | 5\.5\.64\+ | MariaDB database server\. | 
| nvidia\-cuda | 9\.2\.88 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.1\.0 | Oozie command\-line client\. | 
| oozie\-server | 5\.1\.0 | Service for accepting Oozie workflow requests\. | 
| opencv | 3\.4\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 5\.0\.0\-HBase\-2\.0 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 5\.0\.0\-HBase\-2\.0 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.230 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.230 | Service for executing pieces of a query\. | 
| presto\-client | 0\.230 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| r | 3\.4\.3 | The R Project for Statistical Computing | 
| spark\-client | 2\.4\.4 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.4 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.4 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.4 | Apache Spark libraries needed by YARN slaves\. | 
| tensorflow | 1\.14\.0 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.2 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.41\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.9\.0\-SNAPSHOT | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.14 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.14 | ZooKeeper command line client\. | 

**6\.0\.0 Configuration Classifications**

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configuring Applications](emr-configure-apps.md)\.


**emr\-6\.0\.0 Classifications**  

| Classifications | Description | 
| --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | 
| container\-executor | Change values in Hadoop YARN's container\-executor\.cfg file\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | 
| emrfs\-site | Change EMRFS settings\. | 
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
| hdfs\-env | Change values in the HDFS environment\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | 
| hive | Amazon EMR\-curated settings for Apache Hive\. | 
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
| ranger\-kms\-dbks\-site | Change values in dbks\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-site | Change values in ranger\-kms\-site\.xml file of Ranger KMS\. | 
| ranger\-kms\-env | Change values in the Ranger KMS environment\. | 
| ranger\-kms\-log4j | Change values in kms\-log4j\.properties file of Ranger KMS\. | 
| ranger\-kms\-db\-ca | Change values for CA file on S3 for MySQL SSL connection with Ranger KMS\. | 
| recordserver\-env | Change values in the EMR RecordServer environment\. | 
| recordserver\-conf | Change values in EMR RecordServer's erver\.properties file\. | 
| recordserver\-log4j | Change values in EMR RecordServer's log4j\.properties file\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | 
| spark\-env | Change values in the Spark environment\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | 
| yarn\-env | Change values in the YARN environment\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | 

------