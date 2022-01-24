# Amazon EMR release 5\.34\.0<a name="emr-5340-release"></a>
+ [Application versions](#emr-5340-app-versions)
+ [Release notes](#emr-5340-relnotes)
+ [Component versions](#emr-5340-components)
+ [Configuration classifications](#emr-5340-class)

## Application versions<a name="emr-5340-app-versions"></a>

The following applications are supported in this release: [https://flink.apache.org/](https://flink.apache.org/), [http://ganglia.info](http://ganglia.info), [http://hbase.apache.org/](http://hbase.apache.org/), [https://cwiki.apache.org/confluence/display/Hive/HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [https://hudi.apache.org](https://hudi.apache.org), [http://gethue.com/](http://gethue.com/), [https://jupyter.org/enterprise_gateway/](https://jupyter.org/enterprise_gateway/), [https://jupyterhub.readthedocs.io/en/latest/#](https://jupyterhub.readthedocs.io/en/latest/#), [https://livy.incubator.apache.org/](https://livy.incubator.apache.org/), [https://mxnet.incubator.apache.org/](https://mxnet.incubator.apache.org/), [http://mahout.apache.org/](http://mahout.apache.org/), [http://oozie.apache.org/](http://oozie.apache.org/), [https://phoenix.apache.org/](https://phoenix.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), [https://prestodb.io/](https://prestodb.io/), [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/), [http://sqoop.apache.org/](http://sqoop.apache.org/), [https://www.tensorflow.org/](https://www.tensorflow.org/), [https://tez.apache.org/](https://tez.apache.org/), [https://zeppelin.incubator.apache.org/](https://zeppelin.incubator.apache.org/), and [https://zookeeper.apache.org](https://zookeeper.apache.org)\.

The table below lists the application versions available in this release of Amazon EMR and the application versions in the preceding three Amazon EMR releases \(when applicable\)\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following topics:
+ [Application versions in Amazon EMR 6\.x releases](emr-release-app-versions-6.x.md)
+ [Application versions in Amazon EMR 5\.x releases](emr-release-app-versions-5.x.md)
+ [Application versions in Amazon EMR 4\.x releases](emr-release-app-versions-4.x.md)


**Application version information**  

|  | emr\-5\.34\.0 | emr\-5\.33\.1 | emr\-5\.33\.0 | emr\-5\.32\.1 | 
| --- | --- | --- | --- | --- | 
| AWS SDK for Java | 1\.11\.970 | 1\.11\.970 | 1\.11\.970 | 1\.11\.890 | 
| Flink | 1\.13\.1 | 1\.12\.1 | 1\.12\.1 | 1\.11\.2 | 
| Ganglia | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 
| HBase | 1\.4\.13 | 1\.4\.13 | 1\.4\.13 | 1\.4\.13 | 
| HCatalog | 2\.3\.8 | 2\.3\.7 | 2\.3\.7 | 2\.3\.7 | 
| Hadoop | 2\.10\.1 | 2\.10\.1 | 2\.10\.1 | 2\.10\.1 | 
| Hive | 2\.3\.8 | 2\.3\.7 | 2\.3\.7 | 2\.3\.7 | 
| Hudi | 0\.9\.0\-amzn\-0 | 0\.7\.0\-amzn\-1 | 0\.7\.0\-amzn\-1 | 0\.6\.0\-amzn\-0 | 
| Hue | 4\.9\.0 | 4\.9\.0 | 4\.9\.0 | 4\.8\.0 | 
| Iceberg |  \-  |  \-  |  \-  |  \-  | 
| JupyterEnterpriseGateway | 2\.1\.0 | 2\.1\.0 | 2\.1\.0 | 2\.1\.0 | 
| JupyterHub | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 
| Livy | 0\.7\.1 | 0\.7\.0 | 0\.7\.0 | 0\.7\.0 | 
| MXNet | 1\.8\.0 | 1\.7\.0 | 1\.7\.0 | 1\.7\.0 | 
| Mahout | 0\.13\.0 | 0\.13\.0 | 0\.13\.0 | 0\.13\.0 | 
| Oozie | 5\.2\.1 | 5\.2\.0 | 5\.2\.0 | 5\.2\.0 | 
| Phoenix | 4\.14\.3 | 4\.14\.3 | 4\.14\.3 | 4\.14\.3 | 
| Pig | 0\.17\.0 | 0\.17\.0 | 0\.17\.0 | 0\.17\.0 | 
| Presto | 0\.261 | 0\.245\.1 | 0\.245\.1 | 0\.240\.1 | 
| Spark | 2\.4\.8 | 2\.4\.7 | 2\.4\.7 | 2\.4\.7 | 
| Sqoop | 1\.4\.7 | 1\.4\.7 | 1\.4\.7 | 1\.4\.7 | 
| TensorFlow | 2\.4\.1 | 2\.4\.1 | 2\.4\.1 | 2\.3\.1 | 
| Tez | 0\.9\.2 | 0\.9\.2 | 0\.9\.2 | 0\.9\.2 | 
| Trino \(PrestoSQL\) |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin | 0\.10\.0 | 0\.9\.0 | 0\.9\.0 | 0\.8\.2 | 
| ZooKeeper | 3\.4\.14 | 3\.4\.14 | 3\.4\.14 | 3\.4\.14 | 

## Release notes<a name="emr-5340-relnotes"></a>

The following release notes include information for Amazon EMR release version 5\.34\.0\. Changes are relative to 5\.33\.1\.

Initial release date: January 20, 2022

**New Features**
+ \[Hudi\] Improvements to simplify Hudi configuration\. Disabled optimistic concurrency control by default\.

**Changes, Enhancements, and Resolved Issues**
+ Zeppelin upgraded to version 0\.10\.0\.
+ Livy Fix \- upgraded to 0\.7\.1
+ Spark performance improvement \- heterogeneous executors are disabled when certain Spark configuration values are overridden in EMR 5\.34\.0\.
+ WebHDFS and HttpFS server are disabled by default\. You can re\-enable WebHDFS using the Hadoop configuration, `dfs.webhdfs.enabled`\. HttpFS server can be started by using `sudo systemctl start hadoop-httpfs`\.

**Known Issues**
+ The Amazon EMR Notebooks feature used with Livy user impersonation does not work because HttpFS is disabled by default\. In this case, the EMR notebook cannot connect to the cluster that has Livy impersonation enabled\. The workaround is to start HttpFS server before connecting the EMR notebook to the cluster using `sudo systemctl start hadoop-httpfs`\.
+ Hue queries do not work in Amazon EMR 6\.4\.0 because Apache Hadoop HttpFS server is disabled by default\. To use Hue on Amazon EMR 6\.4\.0, either manually start HttpFS server on the Amazon EMR master node using `sudo systemctl start hadoop-httpfs`, or [use an Amazon EMR step](https://docs.aws.amazon.com/emr/latest/ManagementGuide/add-step-cli.html)\.
+ The Amazon EMR Notebooks feature used with Livy user impersonation does not work because HttpFS is disabled by default\. In this case, the EMR notebook cannot connect to the cluster that has Livy impersonation enabled\. The workaround is to start HttpFS server before connecting the EMR notebook to the cluster using `sudo systemctl start hadoop-httpfs`\.

## Component versions<a name="emr-5340-components"></a>

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


| Component | Version | Description | 
| --- | --- | --- | 
| aws\-sagemaker\-spark\-sdk | 1\.4\.1 | Amazon SageMaker Spark SDK | 
| emr\-ddb | 4\.16\.0 | Amazon DynamoDB connector for Hadoop ecosystem applications\. | 
| emr\-goodies | 2\.14\.0 | Extra convenience libraries for the Hadoop ecosystem\. | 
| emr\-kinesis | 3\.5\.0 | Amazon Kinesis connector for Hadoop ecosystem applications\. | 
| emr\-notebook\-env | 1\.4\.0 | Conda env for emr notebook which includes jupyter enterprise gateway | 
| emr\-s3\-dist\-cp | 2\.18\.0 | Distributed copy application optimized for Amazon S3\. | 
| emr\-s3\-select | 1\.7\.0 | EMR S3Select Connector | 
| emrfs | 2\.48\.0 | Amazon S3 connector for Hadoop ecosystem applications\. | 
| flink\-client | 1\.13\.1 | Apache Flink command line client scripts and applications\. | 
| flink\-jobmanager\-config | 1\.13\.1 | Managing resources on EMR nodes for Apache Flink JobManager\. | 
| ganglia\-monitor | 3\.7\.2 | Embedded Ganglia agent for Hadoop ecosystem applications along with the Ganglia monitoring agent\. | 
| ganglia\-metadata\-collector | 3\.7\.2 | Ganglia metadata collector for aggregating metrics from Ganglia monitoring agents\. | 
| ganglia\-web | 3\.7\.1 | Web application for viewing metrics collected by the Ganglia metadata collector\. | 
| hadoop\-client | 2\.10\.1\-amzn\-2 | Hadoop command\-line clients such as 'hdfs', 'hadoop', or 'yarn'\. | 
| hadoop\-hdfs\-datanode | 2\.10\.1\-amzn\-2 | HDFS node\-level service for storing blocks\. | 
| hadoop\-hdfs\-library | 2\.10\.1\-amzn\-2 | HDFS command\-line client and library | 
| hadoop\-hdfs\-namenode | 2\.10\.1\-amzn\-2 | HDFS service for tracking file names and block locations\. | 
| hadoop\-hdfs\-journalnode | 2\.10\.1\-amzn\-2 | HDFS service for managing the Hadoop filesystem journal on HA clusters\. | 
| hadoop\-httpfs\-server | 2\.10\.1\-amzn\-2 | HTTP endpoint for HDFS operations\. | 
| hadoop\-kms\-server | 2\.10\.1\-amzn\-2 | Cryptographic key management server based on Hadoop's KeyProvider API\. | 
| hadoop\-mapred | 2\.10\.1\-amzn\-2 | MapReduce execution engine libraries for running a MapReduce application\. | 
| hadoop\-yarn\-nodemanager | 2\.10\.1\-amzn\-2 | YARN service for managing containers on an individual node\. | 
| hadoop\-yarn\-resourcemanager | 2\.10\.1\-amzn\-2 | YARN service for allocating and managing cluster resources and distributed applications\. | 
| hadoop\-yarn\-timeline\-server | 2\.10\.1\-amzn\-2 | Service for retrieving current and historical information for YARN applications\. | 
| hbase\-hmaster | 1\.4\.13 | Service for an HBase cluster responsible for coordination of Regions and execution of administrative commands\. | 
| hbase\-region\-server | 1\.4\.13 | Service for serving one or more HBase regions\. | 
| hbase\-client | 1\.4\.13 | HBase command\-line client\. | 
| hbase\-rest\-server | 1\.4\.13 | Service providing a RESTful HTTP endpoint for HBase\. | 
| hbase\-thrift\-server | 1\.4\.13 | Service providing a Thrift endpoint to HBase\. | 
| hcatalog\-client | 2\.3\.8\-amzn\-0 | The 'hcat' command line client for manipulating hcatalog\-server\. | 
| hcatalog\-server | 2\.3\.8\-amzn\-0 | Service providing HCatalog, a table and storage management layer for distributed applications\. | 
| hcatalog\-webhcat\-server | 2\.3\.8\-amzn\-0 | HTTP endpoint providing a REST interface to HCatalog\. | 
| hive\-client | 2\.3\.8\-amzn\-0 | Hive command line client\. | 
| hive\-hbase | 2\.3\.8\-amzn\-0 | Hive\-hbase client\. | 
| hive\-metastore\-server | 2\.3\.8\-amzn\-0 | Service for accessing the Hive metastore, a semantic repository storing metadata for SQL on Hadoop operations\. | 
| hive\-server2 | 2\.3\.8\-amzn\-0 | Service for accepting Hive queries as web requests\. | 
| hudi | 0\.9\.0\-amzn\-0 | Incremental processing framework to power data pipeline at low latency and high efficiency\. | 
| hudi\-spark | 0\.9\.0\-amzn\-0 | Bundle library for running Spark with Hudi\. | 
| hudi\-presto | 0\.9\.0\-amzn\-0 | Bundle library for running Presto with Hudi\. | 
| hue\-server | 4\.9\.0 | Web application for analyzing data using Hadoop ecosystem applications | 
| jupyterhub | 1\.4\.1 | Multi\-user server for Jupyter notebooks | 
| livy\-server | 0\.7\.1\-incubating | REST interface for interacting with Apache Spark | 
| nginx | 1\.13\.1 | nginx \[engine x\] is an HTTP and reverse proxy server | 
| mahout\-client | 0\.13\.0 | Library for machine learning\. | 
| mxnet | 1\.8\.0 | A flexible, scalable, and efficient library for deep learning\. | 
| mariadb\-server | 5\.5\.68 | MySQL database server\. | 
| nvidia\-cuda | 10\.1\.243 | Nvidia drivers and Cuda toolkit | 
| oozie\-client | 5\.2\.1 | Oozie command\-line client\. | 
| oozie\-server | 5\.2\.1 | Service for accepting Oozie workflow requests\. | 
| opencv | 4\.5\.0 | Open Source Computer Vision Library\. | 
| phoenix\-library | 4\.14\.3\-HBase\-1\.4 | The phoenix libraries for server and client | 
| phoenix\-query\-server | 4\.14\.3\-HBase\-1\.4 | A light weight server providing JDBC access as well as Protocol Buffers and JSON format access to the Avatica API  | 
| presto\-coordinator | 0\.261\-amzn\-0 | Service for accepting queries and managing query execution among presto\-workers\. | 
| presto\-worker | 0\.261\-amzn\-0 | Service for executing pieces of a query\. | 
| presto\-client | 0\.261\-amzn\-0 | Presto command\-line client which is installed on an HA cluster's stand\-by masters where Presto server is not started\. | 
| pig\-client | 0\.17\.0 | Pig command\-line client\. | 
| r | 4\.0\.2 | The R Project for Statistical Computing | 
| ranger\-kms\-server | 1\.2\.0 | Apache Ranger Key Management System | 
| spark\-client | 2\.4\.8\-amzn\-0 | Spark command\-line clients\. | 
| spark\-history\-server | 2\.4\.8\-amzn\-0 | Web UI for viewing logged events for the lifetime of a completed Spark application\. | 
| spark\-on\-yarn | 2\.4\.8\-amzn\-0 | In\-memory execution engine for YARN\. | 
| spark\-yarn\-slave | 2\.4\.8\-amzn\-0 | Apache Spark libraries needed by YARN slaves\. | 
| sqoop\-client | 1\.4\.7 | Apache Sqoop command\-line client\. | 
| tensorflow | 2\.4\.1 | TensorFlow open source software library for high performance numerical computation\. | 
| tez\-on\-yarn | 0\.9\.2 | The tez YARN application and libraries\. | 
| webserver | 2\.4\.25\+ | Apache HTTP server\. | 
| zeppelin\-server | 0\.10\.0 | Web\-based notebook that enables interactive data analytics\. | 
| zookeeper\-server | 3\.4\.14 | Centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services\. | 
| zookeeper\-client | 3\.4\.14 | ZooKeeper command line client\. | 

## Configuration classifications<a name="emr-5340-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.

Reconfiguration actions occur when you specify a configuration for instance groups in a running cluster\. EMR only initiates reconfiguration actions for the classifications that you modify\. For more information, see [Reconfigure an instance group in a running cluster](emr-configure-apps-running-cluster.md)\.


**emr\-5\.34\.0 classifications**  

| Classifications | Description | Reconfiguration Actions | 
| --- | --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | Restarts the ResourceManager service\. | 
| container\-executor | Change values in Hadoop YARN's container\-executor\.cfg file\. | Not available\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | Not available\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Hadoop KMS, Ranger KMS, HiveServer2, Hive MetaStore, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| docker\-conf | Change docker related settings\. | Not available\. | 
| emrfs\-site | Change EMRFS settings\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts HBaseRegionserver, HBaseMaster, HBaseThrift, HBaseRest, HiveServer2, Hive MetaStore, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | Restarts Flink history server\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | Restarts Flink history server\. | 
| flink\-log4j\-session | Change Flink log4j\-session\.properties settings for Kubernetes/Yarn session\. | Not available\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | Restarts Flink history server\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts PhoenixQueryserver, HiveServer2, Hive MetaStore, and MapReduce\-HistoryServer\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Hadoop KMS, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | Not available\. | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | Not available\. | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | Custom EMR specific property\. Sets emrfs\-site and hbase\-site configs\. See those for their associated restarts\. | 
| hbase\-env | Change values in HBase's environment\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | Not available\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. Additionally restarts Phoenix QueryServer\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | Should not be reconfigured\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Additionally restarts Hadoop Httpfs\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | Restarts Hive WebHCat Server\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | Restarts Hive WebHCat Server\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | Restarts Hive WebHCat Server\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | Not available\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | Not available\. | 
| hive\-env | Change values in the Hive environment\. | Restarts HiveServer2 and HiveMetastore\. Runs Hive schemaTool CLI commands to verify hive\-metastore\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | Restarts HiveServer2 and HiveMetastore\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | Not available\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | Not available\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | Restarts HiveServer2 and HiveMetastore\. Runs Hive schemaTool CLI commands to verify hive\-metastore\. Also restarts Oozie and Zeppelin\. | 
| hiveserver2\-site | Change values in Hive Server2's hiveserver2\-site\.xml file | Not available\. | 
| hue\-ini | Change values in Hue's ini file | Restarts Hue\. Also activates Hue config override CLI commands to pick up new configurations\. | 
| httpfs\-env | Change values in the HTTPFS environment\. | Restarts Hadoop Httpfs service\. | 
| httpfs\-site | Change values in Hadoop's httpfs\-site\.xml file\. | Restarts Hadoop Httpfs service\. | 
| hadoop\-kms\-acls | Change values in Hadoop's kms\-acls\.xml file\. | Not available\. | 
| hadoop\-kms\-env | Change values in the Hadoop KMS environment\. | Restarts Hadoop\-KMS service\. | 
| hadoop\-kms\-log4j | Change values in Hadoop's kms\-log4j\.properties file\. | Not available\. | 
| hadoop\-kms\-site | Change values in Hadoop's kms\-site\.xml file\. | Restarts Hadoop\-KMS and Ranger\-KMS service\. | 
| hudi\-env | Change values in the Hudi environment\. | Not available\. | 
| jupyter\-notebook\-conf | Change values in Jupyter Notebook's jupyter\_notebook\_config\.py file\. | Not available\. | 
| jupyter\-hub\-conf | Change values in JupyterHubs's jupyterhub\_config\.py file\. | Not available\. | 
| jupyter\-s3\-conf | Configure Jupyter Notebook S3 persistence\. | Not available\. | 
| jupyter\-sparkmagic\-conf | Change values in Sparkmagic's config\.json file\. | Not available\. | 
| livy\-conf | Change values in Livy's livy\.conf file\. | Restarts Livy Server\. | 
| livy\-env | Change values in the Livy environment\. | Restarts Livy Server\. | 
| livy\-log4j | Change Livy log4j\.properties settings\. | Restarts Livy Server\. | 
| mapred\-env | Change values in the MapReduce application's environment\. | Restarts Hadoop MapReduce\-HistoryServer\. | 
| mapred\-site | Change values in the MapReduce application's mapred\-site\.xml file\. | Restarts Hadoop MapReduce\-HistoryServer\. | 
| oozie\-env | Change values in Oozie's environment\. | Restarts Oozie\. | 
| oozie\-log4j | Change values in Oozie's oozie\-log4j\.properties file\. | Restarts Oozie\. | 
| oozie\-site | Change values in Oozie's oozie\-site\.xml file\. | Restarts Oozie\. | 
| phoenix\-hbase\-metrics | Change values in Phoenix's hadoop\-metrics2\-hbase\.properties file\. | Not available\. | 
| phoenix\-hbase\-site | Change values in Phoenix's hbase\-site\.xml file\. | Not available\. | 
| phoenix\-log4j | Change values in Phoenix's log4j\.properties file\. | Restarts Phoenix\-QueryServer\. | 
| phoenix\-metrics | Change values in Phoenix's hadoop\-metrics2\-phoenix\.properties file\. | Not available\. | 
| pig\-env | Change values in the Pig environment\. | Not available\. | 
| pig\-properties | Change values in Pig's pig\.properties file\. | Restarts Oozie\. | 
| pig\-log4j | Change values in Pig's log4j\.properties file\. | Not available\. | 
| presto\-log | Change values in Presto's log\.properties file\. | Restarts Presto\-Server\. | 
| presto\-config | Change values in Presto's config\.properties file\. | Restarts Presto\-Server\. | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | Not available\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | Restarts Presto\-Server\. | 
| presto\-node | Change values in Presto's node\.properties file\. | Not available\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | Not available\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | Not available\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | Restarts Presto\-Server\. | 
| presto\-connector\-jmx | Change values in Presto's jmx\.properties file\. | Not available\. | 
| presto\-connector\-kafka | Change values in Presto's kafka\.properties file\. | Not available\. | 
| presto\-connector\-localfile | Change values in Presto's localfile\.properties file\. | Not available\. | 
| presto\-connector\-memory | Change values in Presto's memory\.properties file\. | Not available\. | 
| presto\-connector\-mongodb | Change values in Presto's mongodb\.properties file\. | Not available\. | 
| presto\-connector\-mysql | Change values in Presto's mysql\.properties file\. | Not available\. | 
| presto\-connector\-postgresql | Change values in Presto's postgresql\.properties file\. | Not available\. | 
| presto\-connector\-raptor | Change values in Presto's raptor\.properties file\. | Not available\. | 
| presto\-connector\-redis | Change values in Presto's redis\.properties file\. | Not available\. | 
| presto\-connector\-redshift | Change values in Presto's redshift\.properties file\. | Not available\. | 
| presto\-connector\-tpch | Change values in Presto's tpch\.properties file\. | Not available\. | 
| presto\-connector\-tpcds | Change values in Presto's tpcds\.properties file\. | Not available\. | 
| ranger\-kms\-dbks\-site | Change values in dbks\-site\.xml file of Ranger KMS\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-site | Change values in ranger\-kms\-site\.xml file of Ranger KMS\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-env | Change values in the Ranger KMS environment\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-log4j | Change values in kms\-log4j\.properties file of Ranger KMS\. | Not available\. | 
| ranger\-kms\-db\-ca | Change values for CA file on S3 for MySQL SSL connection with Ranger KMS\. | Not available\. | 
| recordserver\-env | Change values in the EMR RecordServer environment\. | Restarts EMR record server\. | 
| recordserver\-conf | Change values in EMR RecordServer's erver\.properties file\. | Restarts EMR record server\. | 
| recordserver\-log4j | Change values in EMR RecordServer's log4j\.properties file\. | Restarts EMR record server\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | This property modifies spark\-defaults\. See actions there\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-env | Change values in the Spark environment\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | Not available\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | Restarts Spark history server and Spark thrift server\. | 
| sqoop\-env | Change values in Sqoop's environment\. | Not available\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | Not available\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | Not available\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | Restarts Oozie\. | 
| yarn\-env | Change values in the YARN environment\. | Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts MapReduce\-HistoryServer\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Livy Server and MapReduce\-HistoryServer\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | Restarts Zeppelin\. | 
| zeppelin\-site | Change configuration settings in zeppelin\-site\.xml\. | Restarts Zeppelin\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | Restarts Zookeeper server\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | Restarts Zookeeper server\. | 