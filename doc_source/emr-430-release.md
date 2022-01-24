# Amazon EMR release 4\.3\.0<a name="emr-430-release"></a>
+ [Application versions](#emr-430-app-versions)
+ [Release notes](#emr-430-relnotes)
+ [Component versions](#emr-430-components)
+ [Configuration classifications](#emr-430-class)

## Application versions<a name="emr-430-app-versions"></a>

The following applications are supported in this release: [http://ganglia.info](http://ganglia.info), [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [http://gethue.com/](http://gethue.com/), [http://mahout.apache.org/](http://mahout.apache.org/), [http://oozie.apache.org/](http://oozie.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), [https://prestodb.io/](https://prestodb.io/), [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/), and [https://zeppelin.incubator.apache.org/](https://zeppelin.incubator.apache.org/)\.

The table below lists the application versions available in this release of Amazon EMR and the application versions in the preceding three Amazon EMR releases \(when applicable\)\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following topics:
+ [Application versions in Amazon EMR 6\.x releases](emr-release-app-versions-6.x.md)
+ [Application versions in Amazon EMR 5\.x releases](emr-release-app-versions-5.x.md)
+ [Application versions in Amazon EMR 4\.x releases](emr-release-app-versions-4.x.md)


**Application version information**  

|  | emr\-4\.3\.0 | emr\-4\.2\.0 | emr\-4\.1\.0 | emr\-4\.0\.0 | 
| --- | --- | --- | --- | --- | 
| AWS SDK for Java | 1\.10\.27 | 1\.10\.27 | Not available | Not available | 
| Flink |  \-  |  \-  |  \-  |  \-  | 
| Ganglia | 3\.7\.2 | 3\.6\.0 |  \-  |  \-  | 
| HBase |  \-  |  \-  |  \-  |  \-  | 
| HCatalog |  \-  |  \-  |  \-  |  \-  | 
| Hadoop | 2\.7\.1 | 2\.6\.0 | 2\.6\.0 | 2\.6\.0 | 
| Hive | 1\.0\.0 | 1\.0\.0 | 1\.0\.0 | 1\.0\.0 | 
| Hudi |  \-  |  \-  |  \-  |  \-  | 
| Hue | 3\.7\.1 | 3\.7\.1 | 3\.7\.1 |  \-  | 
| Iceberg |  \-  |  \-  |  \-  |  \-  | 
| JupyterEnterpriseGateway |  \-  |  \-  |  \-  |  \-  | 
| JupyterHub |  \-  |  \-  |  \-  |  \-  | 
| Livy |  \-  |  \-  |  \-  |  \-  | 
| MXNet |  \-  |  \-  |  \-  |  \-  | 
| Mahout | 0\.11\.0 | 0\.11\.0 | 0\.11\.0 | 0\.10\.0 | 
| Oozie |  \-  |  \-  |  \-  |  \-  | 
| Oozie\-Sandbox | 4\.2\.0 | 4\.2\.0 | 4\.0\.1 |  \-  | 
| Phoenix |  \-  |  \-  |  \-  |  \-  | 
| Pig | 0\.14\.0 | 0\.14\.0 | 0\.14\.0 | 0\.14\.0 | 
| Presto |  \-  |  \-  |  \-  |  \-  | 
| Presto\-Sandbox | 0\.130 | 0\.125 | 0\.119 |  \-  | 
| Spark | 1\.6\.0 | 1\.5\.2 | 1\.5\.0 | 1\.4\.1 | 
| Sqoop |  \-  |  \-  |  \-  |  \-  | 
| Sqoop\-Sandbox |  \-  |  \-  |  \-  |  \-  | 
| TensorFlow |  \-  |  \-  |  \-  |  \-  | 
| Tez |  \-  |  \-  |  \-  |  \-  | 
| Trino \(PrestoSQL\) |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin\-Sandbox | 0\.5\.5 | 0\.5\.5 | 0\.6\.0\-SNAPSHOT |  \-  | 
| ZooKeeper |  \-  |  \-  |  \-  |  \-  | 
| ZooKeeper\-Sandbox |  \-  |  \-  |  \-  |  \-  | 

## Release notes<a name="emr-430-relnotes"></a>

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

**Known issues resolved from previous releases**
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

## Component versions<a name="emr-430-components"></a>

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


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

## Configuration classifications<a name="emr-430-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.


**emr\-4\.3\.0 classifications**  

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