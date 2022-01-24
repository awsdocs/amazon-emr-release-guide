# Amazon EMR release 4\.0\.0<a name="emr-400-release"></a>
+ [Application versions](#emr-400-app-versions)
+ [Release notes](#emr-400-relnotes)
+ [Component versions](#emr-400-components)
+ [Configuration classifications](#emr-400-class)

## Application versions<a name="emr-400-app-versions"></a>

The following applications are supported in this release: [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [http://mahout.apache.org/](http://mahout.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), and [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/)\.

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

## Release notes<a name="emr-400-relnotes"></a>

## Component versions<a name="emr-400-components"></a>

The components that Amazon EMR installs with this release are listed below\. Some are installed as part of big\-data application packages\. Others are unique to Amazon EMR and installed for system processes and features\. These typically start with `emr` or `aws`\. Big\-data application packages in the most recent Amazon EMR release are usually the latest version found in the community\. We make community releases available in Amazon EMR as quickly as possible\.

Some components in Amazon EMR differ from community versions\. These components have a version label in the form `CommunityVersion-amzn-EmrVersion`\. The `EmrVersion` starts at 0\. For example, if open source community component named `myapp-component` with version 2\.2 has been modified three times for inclusion in different Amazon EMR release versions, its release version is listed as `2.2-amzn-2`\.


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

## Configuration classifications<a name="emr-400-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.


**emr\-4\.0\.0 classifications**  

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