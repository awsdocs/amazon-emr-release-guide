# Amazon EMR release 4\.4\.0<a name="emr-440-release"></a>
+ [Application versions](#emr-440-app-versions)
+ [Release notes](#emr-440-relnotes)
+ [Component versions](#emr-440-components)
+ [Configuration classifications](#emr-440-class)

## Application versions<a name="emr-440-app-versions"></a>

The following applications are supported in this release: [http://ganglia.info](http://ganglia.info), [https://cwiki.apache.org/confluence/display/Hive/HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [http://gethue.com/](http://gethue.com/), [http://mahout.apache.org/](http://mahout.apache.org/), [http://oozie.apache.org/](http://oozie.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), [https://prestodb.io/](https://prestodb.io/), [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/), [http://sqoop.apache.org/](http://sqoop.apache.org/), and [https://zeppelin.incubator.apache.org/](https://zeppelin.incubator.apache.org/)\.

The table below lists the application versions available in this release of Amazon EMR and the application versions in the preceding three Amazon EMR releases \(when applicable\)\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following topics:
+ [Application versions in Amazon EMR 6\.x releases](emr-release-app-versions-6.x.md)
+ [Application versions in Amazon EMR 5\.x releases](emr-release-app-versions-5.x.md)
+ [Application versions in Amazon EMR 4\.x releases](emr-release-app-versions-4.x.md)


**Application version information**  

|  | emr\-4\.4\.0 | emr\-4\.3\.0 | emr\-4\.2\.0 | emr\-4\.1\.0 | 
| --- | --- | --- | --- | --- | 
| AWS SDK for Java | 1\.10\.27 | 1\.10\.27 | 1\.10\.27 | Not available | 
| Flink |  \-  |  \-  |  \-  |  \-  | 
| Ganglia | 3\.7\.2 | 3\.7\.2 | 3\.6\.0 |  \-  | 
| HBase |  \-  |  \-  |  \-  |  \-  | 
| HCatalog | 1\.0\.0 |  \-  |  \-  |  \-  | 
| Hadoop | 2\.7\.1 | 2\.7\.1 | 2\.6\.0 | 2\.6\.0 | 
| Hive | 1\.0\.0 | 1\.0\.0 | 1\.0\.0 | 1\.0\.0 | 
| Hudi |  \-  |  \-  |  \-  |  \-  | 
| Hue | 3\.7\.1 | 3\.7\.1 | 3\.7\.1 | 3\.7\.1 | 
| JupyterEnterpriseGateway |  \-  |  \-  |  \-  |  \-  | 
| JupyterHub |  \-  |  \-  |  \-  |  \-  | 
| Livy |  \-  |  \-  |  \-  |  \-  | 
| MXNet |  \-  |  \-  |  \-  |  \-  | 
| Mahout | 0\.11\.1 | 0\.11\.0 | 0\.11\.0 | 0\.11\.0 | 
| Oozie |  \-  |  \-  |  \-  |  \-  | 
| Oozie\-Sandbox | 4\.2\.0 | 4\.2\.0 | 4\.2\.0 | 4\.0\.1 | 
| Phoenix |  \-  |  \-  |  \-  |  \-  | 
| Pig | 0\.14\.0 | 0\.14\.0 | 0\.14\.0 | 0\.14\.0 | 
| Presto |  \-  |  \-  |  \-  |  \-  | 
| Presto\-Sandbox | 0\.136 | 0\.130 | 0\.125 | 0\.119 | 
| PrestoSQL |  \-  |  \-  |  \-  |  \-  | 
| Spark | 1\.6\.0 | 1\.6\.0 | 1\.5\.2 | 1\.5\.0 | 
| Sqoop |  \-  |  \-  |  \-  |  \-  | 
| Sqoop\-Sandbox | 1\.4\.6 |  \-  |  \-  |  \-  | 
| TensorFlow |  \-  |  \-  |  \-  |  \-  | 
| Tez |  \-  |  \-  |  \-  |  \-  | 
| Trino |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin |  \-  |  \-  |  \-  |  \-  | 
| Zeppelin\-Sandbox | 0\.5\.6 | 0\.5\.5 | 0\.5\.5 | 0\.6\.0\-SNAPSHOT | 
| ZooKeeper |  \-  |  \-  |  \-  |  \-  | 
| ZooKeeper\-Sandbox |  \-  |  \-  |  \-  |  \-  | 

## Release notes<a name="emr-440-relnotes"></a>

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

**Known issues resolved from previous releases**
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

## Component versions<a name="emr-440-components"></a>

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


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

## Configuration classifications<a name="emr-440-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.


**emr\-4\.4\.0 classifications**  

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