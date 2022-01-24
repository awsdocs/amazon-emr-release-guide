# Amazon EMR release 6\.2\.0<a name="emr-620-release"></a>
+ [Application versions](#emr-620-app-versions)
+ [Release notes](#emr-620-relnotes)
+ [Component versions](#emr-620-components)
+ [Configuration classifications](#emr-620-class)

## Application versions<a name="emr-620-app-versions"></a>

The following applications are supported in this release: [https://flink.apache.org/](https://flink.apache.org/), [http://ganglia.info](http://ganglia.info), [http://hbase.apache.org/](http://hbase.apache.org/), [https://cwiki.apache.org/confluence/display/Hive/HCatalog](https://cwiki.apache.org/confluence/display/Hive/HCatalog), [http://hadoop.apache.org/docs/current/](http://hadoop.apache.org/docs/current/), [http://hive.apache.org/](http://hive.apache.org/), [https://hudi.apache.org](https://hudi.apache.org), [http://gethue.com/](http://gethue.com/), [https://jupyter.org/enterprise_gateway/](https://jupyter.org/enterprise_gateway/), [https://jupyterhub.readthedocs.io/en/latest/#](https://jupyterhub.readthedocs.io/en/latest/#), [https://livy.incubator.apache.org/](https://livy.incubator.apache.org/), [https://mxnet.incubator.apache.org/](https://mxnet.incubator.apache.org/), [http://oozie.apache.org/](http://oozie.apache.org/), [https://phoenix.apache.org/](https://phoenix.apache.org/), [http://pig.apache.org/](http://pig.apache.org/), [https://prestodb.io/](https://prestodb.io/), [https://prestosql.io/](https://prestosql.io/), [https://spark.apache.org/docs/latest/](https://spark.apache.org/docs/latest/), [http://sqoop.apache.org/](http://sqoop.apache.org/), [https://www.tensorflow.org/](https://www.tensorflow.org/), [https://tez.apache.org/](https://tez.apache.org/), [https://zeppelin.incubator.apache.org/](https://zeppelin.incubator.apache.org/), and [https://zookeeper.apache.org](https://zookeeper.apache.org)\.

The table below lists the application versions available in this release of Amazon EMR and the application versions in the preceding three Amazon EMR releases \(when applicable\)\.

For a comprehensive history of application versions for each release of Amazon EMR, see the following topics:
+ [Application versions in Amazon EMR 6\.x releases](emr-release-app-versions-6.x.md)
+ [Application versions in Amazon EMR 5\.x releases](emr-release-app-versions-5.x.md)
+ [Application versions in Amazon EMR 4\.x releases](emr-release-app-versions-4.x.md)


**Application version information**  

|  | emr\-6\.2\.0 | emr\-6\.1\.1 | emr\-6\.1\.0 | emr\-6\.0\.1 | 
| --- | --- | --- | --- | --- | 
| AWS SDK for Java | 1\.11\.880 | 1\.11\.828 | 1\.11\.828 | 1\.11\.711 | 
| Flink | 1\.11\.2 | 1\.11\.0 | 1\.11\.0 |  \-  | 
| Ganglia | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 3\.7\.2 | 
| HBase | 2\.2\.6\-amzn\-0 | 2\.2\.5 | 2\.2\.5 | 2\.2\.3 | 
| HCatalog | 3\.1\.2 | 3\.1\.2 | 3\.1\.2 | 3\.1\.2 | 
| Hadoop | 3\.2\.1 | 3\.2\.1 | 3\.2\.1 | 3\.2\.1 | 
| Hive | 3\.1\.2 | 3\.1\.2 | 3\.1\.2 | 3\.1\.2 | 
| Hudi | 0\.6\.0\-amzn\-1 | 0\.5\.2\-incubating\-amzn\-2 | 0\.5\.2\-incubating\-amzn\-2 | 0\.5\.0\-incubating\-amzn\-1 | 
| Hue | 4\.8\.0 | 4\.7\.1 | 4\.7\.1 | 4\.4\.0 | 
| Iceberg |  \-  |  \-  |  \-  |  \-  | 
| JupyterEnterpriseGateway | 2\.1\.0 |  \-  |  \-  |  \-  | 
| JupyterHub | 1\.1\.0 | 1\.1\.0 | 1\.1\.0 | 1\.0\.0 | 
| Livy | 0\.7\.0 | 0\.7\.0 | 0\.7\.0 | 0\.6\.0 | 
| MXNet | 1\.7\.0 | 1\.6\.0 | 1\.6\.0 | 1\.5\.1 | 
| Mahout |  \-  |  \-  |  \-  |  \-  | 
| Oozie | 5\.2\.0 | 5\.2\.0 | 5\.2\.0 | 5\.1\.0 | 
| Phoenix | 5\.0\.0 | 5\.0\.0 | 5\.0\.0 | 5\.0\.0 | 
| Pig | 0\.17\.0 | 0\.17\.0 | 0\.17\.0 |  \-  | 
| Presto | 0\.238\.3 | 0\.232 | 0\.232 | 0\.230 | 
| Spark | 3\.0\.1 | 3\.0\.0 | 3\.0\.0 | 2\.4\.4 | 
| Sqoop | 1\.4\.7 | 1\.4\.7 | 1\.4\.7 |  \-  | 
| TensorFlow | 2\.3\.1 | 2\.1\.0 | 2\.1\.0 | 1\.14\.0 | 
| Tez | 0\.9\.2 | 0\.9\.2 | 0\.9\.2 | 0\.9\.2 | 
| Trino \(PrestoSQL\) | 343 | 338 | 338 |  \-  | 
| Zeppelin | 0\.9\.0 | 0\.9\.0 | 0\.9\.0 | 0\.9\.0 | 
| ZooKeeper | 3\.4\.14 | 3\.4\.14 | 3\.4\.14 | 3\.4\.14 | 

## Release notes<a name="emr-620-relnotes"></a>

The following release notes include information for Amazon EMR release version 6\.2\.0\. Changes are relative to 6\.1\.0\.

Initial release date: Dec 09, 2020

Last updated date: Oct 04, 2021

**Supported applications**
+ AWS SDK for Java version 1\.11\.828
+ emr\-record\-server version 1\.7\.0
+ Flink version 1\.11\.2
+ Ganglia version 3\.7\.2
+ Hadoop version 3\.2\.1\-amzn\-1
+ HBase version 2\.2\.6\-amzn\-0
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
+ Spark version 3\.0\.1\-amzn\-0
+ spark\-rapids 0\.2\.0
+ TensorFlow version 2\.3\.1
+ Zeppelin version 0\.9\.0\-preview1
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.16\.0

**New features**
+ HBase: Removed rename in commit phase and added persistent HFile tracking\. See [Persistent HFile Tracking](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-hfile-tracking) in the *Amazon EMR Release Guide*\.
+ HBase: Backported [Create a config that forces to cache blocks on compaction](https://issues.apache.org/jira/browse/HBASE-23066)\.
+ PrestoDB: Improvements to Dynamic Partition Pruning\. Rule\-based Join Reorder works on non\-partitioned data\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.
+ Instance Metadata Service \(IMDS\) V2 support status: For Amazon EMR 6\.2 or later, Amazon EMR components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. If you disable IMDSv1 in earlier Amazon EMR 6\.x releases, it causes cluster startup failure\.

**Changes, enhancements, and resolved issues**
+ Amazon EMR version 6\.2\.1 fixed issues with Managed Scaling unable to complete or causing application failures\.
+ Spark: Performance improvements in Spark runtime\.

**Known issues**
+ Amazon EMR 6\.2 has incorrect permissions set on the /etc/cron\.d/libinstance\-controller\-java file in EMR 6\.2\.0\. Permissions on the file are 645 \(\-rw\-r\-\-r\-x\), when they should be 644 \(\-rw\-r\-\-r\-\-\)\. As a result, Amazon EMR version 6\.2 does not log instance\-state logs, and the /emr/instance\-logs directory is empty\. This issue is fixed in Amazon EMR 6\.3\.0 and later\.

  To work around this issue, run the following script as a bootstrap action at cluster launch\. 

  ```
  #!/bin/bash
  sudo chmod 644 /etc/cron.d/libinstance-controller-java
  ```
+ For Amazon EMR 6\.2\.0 and 6\.3\.0 private subnet clusters, you cannot access the Ganglia web UI\. You will get an "access denied \(403\)" error\. Other web UIs, such as Spark, Hue, JupyterHub, Zeppelin, Livy, and Tez are working normally\. Ganglia web UI access on public subnet clusters are also working normally\. To resolve this issue, restart httpd service on the master node with `sudo systemctl restart httpd`\. This issue is fixed in Amazon EMR 6\.4\.0\.
+ There is an issue in Amazon EMR 6\.2\.0 where httpd continuously fails, causing Ganglia to be unavailable\. You get a "cannot connect to the server" error\. To fix a cluster that is already running with this issue, SSH to the cluster master node and add the line `Listen 80` to the file `httpd.conf` located at `/etc/httpd/conf/httpd.conf`\. This issue is fixed in Amazon EMR 6\.3\.0\.
+ HTTPD fails on EMR 6\.2\.0 clusters when you use a security configuration\. This makes the Ganglia web application user interface unavailable\. To access the Ganglia web application user interface, add `Listen 80` to the `/etc/httpd/conf/httpd.conf` file on the master node of your cluster\. For information about connecting to your cluster, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html)\.

  EMR Notebooks also fail to establish a connection with EMR 6\.2\.0 clusters when you use a security configuration\. The notebook will fail to list kernels and submit Spark jobs\. We recommend that you use EMR Notebooks with another version of Amazon EMR instead\.
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for "Max open files" when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

  The following workaround for this issue lets you to explicitly set the instance\-controller ulimit to a maximum of 65536 files\.

**Explicitly set a ulimit from the command line**

  1. Edit `/etc/systemd/system/instance-controller.service` to add the following parameters to Service section\.

     `LimitNOFILE=65536`

     `LimitNPROC=65536`

  1. Restart InstanceController

     `$ sudo systemctl daemon-reload`

     `$ sudo systemctl restart instance-controller`

  **Set a ulimit using bootstrap action \(BA\)**

  You can also use a bootstrap action \(BA\) script to configure the instance\-controller ulimit to 65536 files at cluster creation\.

  ```
  #!/bin/bash
  for user in hadoop spark hive; do
  sudo tee /etc/security/limits.d/$user.conf << EOF
  $user - nofile 65536
  $user - nproc 65536
  EOF
  done
  for proc in instancecontroller logpusher; do
  sudo mkdir -p /etc/systemd/system/$proc.service.d/
  sudo tee /etc/systemd/system/$proc.service.d/override.conf << EOF
  [Service]
  LimitNOFILE=65536
  LimitNPROC=65536
  EOF
  pid=$(pgrep -f aws157.$proc.Main)
  sudo prlimit --pid $pid --nofile=65535:65535 --nproc=65535:65535
  done
  sudo systemctl daemon-reload
  ```
+ 
**Important**  
Amazon EMR 6\.1\.0 and 6\.2\.0 include a performance issue that can critically affect all Hudi insert, upsert, and delete operations\. If you plan to use Hudi with Amazon EMR 6\.1\.0 or 6\.2\.0, you should contact AWS support to obtain a patched Hudi RPM\.
+ 
**Important**  
Amazon EMR clusters that are running Amazon Linux or Amazon Linux 2 AMIs \(Amazon Linux Machine Images\) use default Amazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If new Amazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an Amazon EMR version is released, Amazon EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latest Amazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
+ Amazon EMR 6\.2\.0 Maven artifacts are not published\. They will be published with a future release of Amazon EMR\.
+ Persistent HFile tracking using the HBase storefile system table does not support the HBase region replication feature\. For more information about HBase region replication, see [Timeline\-consistent High Available Reads](http://hbase.apache.org/book.html#arch.timelineconsistent.reads)\.
+ Amazon EMR 6\.x and EMR 5\.x Hive bucketing version differences

  EMR 5\.x uses OOS Apache Hive 2, while in EMR 6\.x uses OOS Apache Hive 3\. The open source Hive2 uses Bucketing version 1, while open source Hive3 uses Bucketing version 2\. This bucketing version difference between Hive 2 \(EMR 5\.x\) and Hive 3 \(EMR 6\.x\) means Hive bucketing hashing functions differently\. See the example below\.

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

## Component versions<a name="emr-620-components"></a>

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

## Configuration classifications<a name="emr-620-class"></a>

Configuration classifications allow you to customize applications\. These often correspond to a configuration XML file for the application, such as `hive-site.xml`\. For more information, see [Configure applications](emr-configure-apps.md)\.

Reconfiguration actions occur when you specify a configuration for instance groups in a running cluster\. EMR only initiates reconfiguration actions for the classifications that you modify\. For more information, see [Reconfigure an instance group in a running cluster](emr-configure-apps-running-cluster.md)\.


**emr\-6\.2\.0 classifications**  

| Classifications | Description | Reconfiguration Actions | 
| --- | --- | --- | 
| capacity\-scheduler | Change values in Hadoop's capacity\-scheduler\.xml file\. | Restarts the ResourceManager service\. | 
| container\-executor | Change values in Hadoop YARN's container\-executor\.cfg file\. | Not available\. | 
| container\-log4j | Change values in Hadoop YARN's container\-log4j\.properties file\. | Not available\. | 
| core\-site | Change values in Hadoop's core\-site\.xml file\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Hadoop KMS, Ranger KMS, HiveServer2, Hive MetaStore, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| docker\-conf | Change docker related settings\. | Not available\. | 
| emrfs\-site | Change EMRFS settings\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts HBaseRegionserver, HBaseMaster, HBaseThrift, HBaseRest, HiveServer2, Hive MetaStore, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| flink\-conf | Change flink\-conf\.yaml settings\. | Not available\. | 
| flink\-log4j | Change Flink log4j\.properties settings\. | Not available\. | 
| flink\-log4j\-yarn\-session | Change Flink log4j\-yarn\-session\.properties settings\. | Not available\. | 
| flink\-log4j\-cli | Change Flink log4j\-cli\.properties settings\. | Not available\. | 
| hadoop\-env | Change values in the Hadoop environment for all Hadoop components\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts PhoenixQueryserver, HiveServer2, Hive MetaStore, and MapReduce\-HistoryServer\. | 
| hadoop\-log4j | Change values in Hadoop's log4j\.properties file\. | Restarts the Hadoop HDFS services SecondaryNamenode, Datanode, and Journalnode\. Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Hadoop KMS, Hadoop Httpfs, and MapReduce\-HistoryServer\. | 
| hadoop\-ssl\-server | Change hadoop ssl server configuration | Not available\. | 
| hadoop\-ssl\-client | Change hadoop ssl client configuration | Not available\. | 
| hbase | Amazon EMR\-curated settings for Apache HBase\. | Custom EMR specific property\. Sets emrfs\-site and hbase\-site configs\. See those for their associated restarts\. | 
| hbase\-env | Change values in HBase's environment\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-log4j | Change values in HBase's hbase\-log4j\.properties file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-metrics | Change values in HBase's hadoop\-metrics2\-hbase\.properties file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. | 
| hbase\-policy | Change values in HBase's hbase\-policy\.xml file\. | Not available\. | 
| hbase\-site | Change values in HBase's hbase\-site\.xml file\. | Restarts the HBase services RegionServer, HBaseMaster, ThriftServer, RestServer\. Additionally restarts Phoenix QueryServer\. | 
| hdfs\-encryption\-zones | Configure HDFS encryption zones\. | This classification should not be reconfigured\. | 
| hdfs\-env | Change values in the HDFS environment\. | Restarts Hadoop HDFS ZKFC\. | 
| hdfs\-site | Change values in HDFS's hdfs\-site\.xml\. | Restarts the Hadoop HDFS services Namenode, SecondaryNamenode, Datanode, ZKFC, and Journalnode\. Additionally restarts Hadoop Httpfs\. | 
| hcatalog\-env | Change values in HCatalog's environment\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-server\-jndi | Change values in HCatalog's jndi\.properties\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-server\-proto\-hive\-site | Change values in HCatalog's proto\-hive\-site\.xml\. | Restarts Hive HCatalog Server\. | 
| hcatalog\-webhcat\-env | Change values in HCatalog WebHCat's environment\. | Restarts Hive WebHCat server\. | 
| hcatalog\-webhcat\-log4j2 | Change values in HCatalog WebHCat's log4j2\.properties\. | Restarts Hive WebHCat server\. | 
| hcatalog\-webhcat\-site | Change values in HCatalog WebHCat's webhcat\-site\.xml file\. | Restarts Hive WebHCat server\. | 
| hive | Amazon EMR\-curated settings for Apache Hive\. | Sets configurations to launch Hive LLAP service\. | 
| hive\-beeline\-log4j2 | Change values in Hive's beeline\-log4j2\.properties file\. | Not available\. | 
| hive\-parquet\-logging | Change values in Hive's parquet\-logging\.properties file\. | Not available\. | 
| hive\-env | Change values in the Hive environment\. | Restarts HiveServer2, HiveMetastore, and Hive HCatalog\-Server\. Runs Hive schemaTool CLI commands to verify hive\-metastore\. | 
| hive\-exec\-log4j2 | Change values in Hive's hive\-exec\-log4j2\.properties file\. | Not available\. | 
| hive\-llap\-daemon\-log4j2 | Change values in Hive's llap\-daemon\-log4j2\.properties file\. | Not available\. | 
| hive\-log4j2 | Change values in Hive's hive\-log4j2\.properties file\. | Not available\. | 
| hive\-site | Change values in Hive's hive\-site\.xml file | Restarts HiveServer2, HiveMetastore, and Hive HCatalog\-Server\. Runs Hive schemaTool CLI commands to verify hive\-metastore\. Also restarts Oozie and Zeppelin\. | 
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
| presto\-log | Change values in Presto's log\.properties file\. | Restarts Presto\-Server \(for PrestoDB\) | 
| presto\-config | Change values in Presto's config\.properties file\. | Restarts Presto\-Server \(for PrestoDB\) | 
| presto\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | Not available\. | 
| presto\-env | Change values in Presto's presto\-env\.sh file\. | Restarts Presto\-Server \(for PrestoDB\) | 
| presto\-node | Change values in Presto's node\.properties file\. | Not available\. | 
| presto\-connector\-blackhole | Change values in Presto's blackhole\.properties file\. | Not available\. | 
| presto\-connector\-cassandra | Change values in Presto's cassandra\.properties file\. | Not available\. | 
| presto\-connector\-hive | Change values in Presto's hive\.properties file\. | Restarts Presto\-Server \(for PrestoDB\) | 
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
| prestosql\-log | Change values in Presto's log\.properties file\. | Restarts Presto\-Server \(for PrestoSQL\) | 
| prestosql\-config | Change values in Presto's config\.properties file\. | Restarts Presto\-Server \(for PrestoSQL\) | 
| prestosql\-password\-authenticator | Change values in Presto's password\-authenticator\.properties file\. | Restarts Presto\-Server \(for PrestoSQL\) | 
| prestosql\-env | Change values in Presto's presto\-env\.sh file\. | Restarts Presto\-Server \(for PrestoSQL\) | 
| prestosql\-node | Change values in PrestoSQL's node\.properties file\. | Not available\. | 
| prestosql\-connector\-blackhole | Change values in PrestoSQL's blackhole\.properties file\. | Not available\. | 
| prestosql\-connector\-cassandra | Change values in PrestoSQL's cassandra\.properties file\. | Not available\. | 
| prestosql\-connector\-hive | Change values in PrestoSQL's hive\.properties file\. | Restarts Presto\-Server \(for PrestoSQL\) | 
| prestosql\-connector\-jmx | Change values in PrestoSQL's jmx\.properties file\. | Not available\. | 
| prestosql\-connector\-kafka | Change values in PrestoSQL's kafka\.properties file\. | Not available\. | 
| prestosql\-connector\-localfile | Change values in PrestoSQL's localfile\.properties file\. | Not available\. | 
| prestosql\-connector\-memory | Change values in PrestoSQL's memory\.properties file\. | Not available\. | 
| prestosql\-connector\-mongodb | Change values in PrestoSQL's mongodb\.properties file\. | Not available\. | 
| prestosql\-connector\-mysql | Change values in PrestoSQL's mysql\.properties file\. | Not available\. | 
| prestosql\-connector\-postgresql | Change values in PrestoSQL's postgresql\.properties file\. | Not available\. | 
| prestosql\-connector\-raptor | Change values in PrestoSQL's raptor\.properties file\. | Not available\. | 
| prestosql\-connector\-redis | Change values in PrestoSQL's redis\.properties file\. | Not available\. | 
| prestosql\-connector\-redshift | Change values in PrestoSQL's redshift\.properties file\. | Not available\. | 
| prestosql\-connector\-tpch | Change values in PrestoSQL's tpch\.properties file\. | Not available\. | 
| prestosql\-connector\-tpcds | Change values in PrestoSQL's tpcds\.properties file\. | Not available\. | 
| ranger\-kms\-dbks\-site | Change values in dbks\-site\.xml file of Ranger KMS\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-site | Change values in ranger\-kms\-site\.xml file of Ranger KMS\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-env | Change values in the Ranger KMS environment\. | Restarts Ranger KMS Server\. | 
| ranger\-kms\-log4j | Change values in kms\-log4j\.properties file of Ranger KMS\. | Not available\. | 
| ranger\-kms\-db\-ca | Change values for CA file on S3 for MySQL SSL connection with Ranger KMS\. | Not available\. | 
| spark | Amazon EMR\-curated settings for Apache Spark\. | This property modifies spark\-defaults\. See actions there\. | 
| spark\-defaults | Change values in Spark's spark\-defaults\.conf file\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-env | Change values in the Spark environment\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-hive\-site | Change values in Spark's hive\-site\.xml file | Not available\. | 
| spark\-log4j | Change values in Spark's log4j\.properties file\. | Restarts Spark history server and Spark thrift server\. | 
| spark\-metrics | Change values in Spark's metrics\.properties file\. | Restarts Spark history server and Spark thrift server\. | 
| sqoop\-env | Change values in Sqoop's environment\. | Not available\. | 
| sqoop\-oraoop\-site | Change values in Sqoop OraOop's oraoop\-site\.xml file\. | Not available\. | 
| sqoop\-site | Change values in Sqoop's sqoop\-site\.xml file\. | Not available\. | 
| tez\-site | Change values in Tez's tez\-site\.xml file\. | Restart Oozie\. | 
| yarn\-env | Change values in the YARN environment\. | Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts MapReduce\-HistoryServer\. | 
| yarn\-site | Change values in YARN's yarn\-site\.xml file\. | Restarts the Hadoop YARN services ResourceManager, NodeManager, ProxyServer, and TimelineServer\. Additionally restarts Livy Server and MapReduce\-HistoryServer\. | 
| zeppelin\-env | Change values in the Zeppelin environment\. | Restarts Zeppelin\. | 
| zookeeper\-config | Change values in ZooKeeper's zoo\.cfg file\. | Restarts Zookeeper server\. | 
| zookeeper\-log4j | Change values in ZooKeeper's log4j\.properties file\. | Restarts Zookeeper server\. | 