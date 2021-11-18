# What's new?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR 6\.x series and 5\.x series\. These release notes are also available on the [Release 6\.4\.0 Tab](emr-640-release.md) and [Release 5\.33\.0 Tab](emr-5330-release.md), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR what's new history](emr-whatsnew-history.md)\.

**Note**  
Twenty\-five previous Amazon EMR release versions now use AWS Signature Version 4 to authenticate requests to Amazon S3\. The use of AWS Signature version 2 is being phased out and new S3 buckets created after June 24, 2020 will not support Signature Version 2 signed requests\. Existing buckets will continue to support Signature Version 2\. We recommend migrating to an Amazon EMR release that supports Signature Version 4 so you can continue accessing new S3 buckets and avoid any potential interruption to your workloads\.  
The following EMR releases are now available that supports Signature Version 4: emr\-4\.7\.4, emr\-4\.8\.5, emr\-4\.9\.6, emr\-4\.10\.1, emr\-5\.1\.1, emr\-5\.2\.3, emr\-5\.3\.2, emr\-5\.4\.1, emr\-5\.5\.4, emr\-5\.6\.1, emr\-5\.7\.1, emr\-5\.8\.3, emr\-5\.9\.1, emr\-5\.10\.1, emr\-5\.11\.4, emr\-5\.12\.3, emr\-5\.13\.1, emr\-5\.14\.2, emr\-5\.15\.1, emr\-5\.16\.1, emr\-5\.17\.2, emr\-5\.18\.1, emr\-5\.19\.1, emr\-5\.20\.1, and emr\-5\.21\.2\. EMR version 5\.22\.0 and later already support Signature Version 4\.  
You do not need to change your application code to use Signature Version 4 if you are using Amazon EMR applications, such as Apache Spark, Apache Hive, Presto, etc\. If you are using custom applications, which are not included with Amazon EMR, you may need to update your code to use Signature Version 4\. For more information about what updates may be required, see [Moving from Signature Version 2 to Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html#UsingAWSSDK-move-to-Sig4)\.

## Release 6\.4\.0 \(latest version of Amazon EMR 6\.x series\)<a name="emr-640-whatsnew"></a>

New Amazon EMR release versions are made available in different Regions over a period of several days, beginning with the first Region on the initial release date\. The latest release version may not be available in your Region during this period\.

The following release notes include information for Amazon EMR release version 6\.4\.0\. Changes are relative to 6\.3\.0\.

Initial release date: Sept 20, 2021

**Supported applications**
+ AWS SDK for Java version 1\.12\.31
+ CloudWatch Sink version 2\.2\.0
+ DynamoDB Connector version 4\.16\.0
+ EMRFS version 2\.47\.0
+ Amazon EMR Goodies version 3\.2\.0
+ Amazon EMR Kinesis Connector version 3\.5\.0
+ Amazon EMR Record Server version 2\.1\.0
+ Amazon EMR Scripts version 2\.5\.0
+ Flink version 1\.13\.1
+ Ganglia version 3\.7\.2
+ AWS Glue Hive Metastore Client version 3\.3\.0
+ Hadoop version 3\.2\.1\-amzn\-4
+ HBase version 2\.4\.4\-amzn\-0
+ HBase\-operator\-tools 1\.1\.0
+ HCatalog version 3\.1\.2\-amzn\-5
+ Hive version 3\.1\.2\-amzn\-5
+ Hudi version 0\.8\.0\-amzn\-0
+ Hue version 4\.9\.0
+ Java JDK version Corretto\-8\.302\.08\.1 \(build 1\.8\.0\_302\-b08\)
+ JupyterHub version 1\.4\.1
+ Livy version 0\.7\.1\-incubating
+ MXNet version 1\.8\.0
+ Oozie version 5\.2\.1
+ Phoenix version 5\.1\.2
+ Pig version 0\.17\.0
+ Presto version 0\.254\.1\-amzn\-0
+ Trino version 359
+ Apache Ranger KMS \(multi\-master transparent encryption\) version 2\.0\.0
+ ranger\-plugins 2\.0\.1\-amzn\-0
+ ranger\-s3\-plugin 1\.2\.0
+ SageMaker Spark SDK version 1\.4\.1
+ Scala version 2\.12\.10 \(OpenJDK 64\-Bit Server VM, Java 1\.8\.0\_282\)
+ Spark version 3\.1\.2\-amzn\-0
+ spark\-rapids 0\.4\.1
+ Sqoop version 1\.4\.7
+ TensorFlow version 2\.4\.1
+ tez version 0\.9\.2
+ Zeppelin version 0\.9\.0
+ Zookeeper version 3\.5\.7
+ Connectors and drivers: DynamoDB Connector 4\.16\.0

**New features**
+ On Apache Ranger\-enabled Amazon EMR clusters, you can use Apache Spark SQL to insert data into or update the Apache Hive metastore tables using `INSERT INTO`, `INSERT OVERWRITE`, and `ALTER TABLE`\. When using ALTER TABLE with Spark SQL, a partition location must be the child directory of a table location\. Amazon EMR does not currently support inserting data into a partition where the partition location is different from the table location\.
+ PrestoSQL has been [renamed to Trino\.](https://trino.io/blog/2020/12/27/announcing-trino.html) 
+ Hive: Execution of simple SELECT queries with LIMIT clause are accelerated by stopping the query execution as soon as the number of records mentioned in LIMIT clause is fetched\. Simple SELECT queries are queries that do not have GROUP BY / ORDER by clause or queries that do not have a reducer stage\. For example, `SELECT * from <TABLE> WHERE <Condition> LIMIT <Number>`\. 

**Hudi Concurrency Control**
+ Hudi now supports Optimistic Concurrency Control \(OCC\), which can be leveraged with write operations like UPSERT and INSERT to allow changes from multiple writers to the same Hudi table\. This is file\-level OCC, so any two commits \(or writers\) can write to the same table, if their changes do not conflict\. For more information, see the [Hudi concurrency control](https://hudi.apache.org/docs/concurrency_control/)\. 
+ Amazon EMR clusters have Zookeeper installed, which can be leveraged as the lock provider for OCC\. To make it easier to use this feature, Amazon EMR clusters have the following properties pre\-configured:

  ```
  hoodie.write.lock.provider=org.apache.hudi.client.transaction.lock.ZookeeperBasedLockProvider
  hoodie.write.lock.zookeeper.url=<EMR Zookeeper URL>
  hoodie.write.lock.zookeeper.port=<EMR Zookeeper Port>
  hoodie.write.lock.zookeeper.base_path=/hudi
  ```

  To enable OCC, you need to configure the following properties either with their Hudi job options or at the cluster\-level using the Amazon EMR configurations API:

  ```
  hoodie.write.concurrency.mode=optimistic_concurrency_control
  hoodie.cleaner.policy.failed.writes=LAZY (Performs cleaning of failed writes lazily instead of inline with every write)
  hoodie.write.lock.zookeeper.lock_key=<Key to uniquely identify the Hudi table> (Table Name is a good option)
  ```

**Hudi Monitoring: Amazon CloudWatch integration to report Hudi Metrics**
+ Amazon EMR supports publishing Hudi Metrics to Amazon CloudWatch\. It is enabled by setting the following required configurations:

  ```
  hoodie.metrics.on=true
  hoodie.metrics.reporter.type=CLOUDWATCH
  ```
+ The following are optional Hudi configurations that you can change:    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew.html)

**Amazon EMR Hudi configurations support and improvements**
+ Customers can now leverage EMR Configurations API and Reconfiguration feature to configure Hudi configurations at cluster level\. A new file based configuration support has been introduced via /etc/hudi/conf/hudi\-defaults\.conf along the lines of other applications like Spark, Hive etc\. EMR configures few defaults to improve user experience:

  — `hoodie.datasource.hive_sync.jdbcurl ` is configured to the cluster Hive server URL and no longer needs to be specified\. This is particularly useful when running a job in Spark cluster mode, where you previously had to specify the Amazon EMR master IP\. 

  — HBase specific configurations, which are useful for using HBase index with Hudi\.

  — Zookeeper lock provider specific configuration, as discussed under concurrency control, which makes it easier to use Optimistic Concurrency Control \(OCC\)\.
+ Additional changes have been introduced to reduce the number of configurations that you need to pass, and to infer automatically where possible:

  — The `partitionBy ` keyword can be used to specify the partition column\. 

  — When enabling Hive Sync, it is no longer mandatory to pass `HIVE_TABLE_OPT_KEY, HIVE_PARTITION_FIELDS_OPT_KEY, HIVE_PARTITION_EXTRACTOR_CLASS_OPT_KEY`\. Those values can be inferred from the Hudi table name and partition field\. 

  — `KEYGENERATOR_CLASS_OPT_KEY` is not mandatory to pass, and can be inferred from simpler cases of `SimpleKeyGenerator` and `ComplexKeyGenerator`\. 

**Hudi Caveats**
+ Hudi does not support vectorized execution in Hive for Merge on Read \(MoR\) and Bootstrap tables\. For example, `count(*)` fails with Hudi realtime table when `hive.vectorized.execution.enabled` is set to true\. As a workaround, you can disable vectorized reading by setting `hive.vectorized.execution.enabled` to `false`\. 
+ Multi\-writer support is not compatible with the Hudi bootstrap feature\.
+ Flink Streamer and Flink SQL are experimental features in this release\. These features are not recommended for use in production deployments\.

**Changes, enhancements, and resolved issues**
+ **Configuring a cluster to fix Apache YARN Timeline Server version 1 and 1\.5 performance issues**

  Apache YARN Timeline Server version 1 and 1\.5 can cause performance issues with very active, large EMR clusters, particularly with `yarn.resourcemanager.system-metrics-publisher.enabled=true`, which is the default setting in EMR\. An open source YARN Timeline Server v2 solves the performance issue related to YARN Timeline Server scalability\.

  Other workarounds for this issue include:
  + Configuring yarn\.resourcemanager\.system\-metrics\-publisher\.enabled=false in yarn\-site\.xml\.
  + Enabling the fix for this issue when creating a cluster, as described below\.

  The following Amazon EMR release versions contain a fix for this YARN Timeline Server performance issue\.

  EMR 5\.30\.2, 5\.31\.1, 5\.32\.1, 5\.33\.1, 5\.34\.x, 6\.0\.1, 6\.1\.1, 6\.2\.1, 6\.3\.1, 6\.4\.x

  To enable the fix on any of the above specified Amazon EMR releases, set these properties to `true` in a configurations JSON file that is passed in using the [`aws emr create-cluster` command parameter](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-create-cluster.html): `--configurations file://./configurations.json`\. Or enable the fix using the [reconfiguration console UI](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

  Example of the configurations\.json file contents:

  ```
  [
  {
  "Classification": "yarn-site",
  "Properties": {
  "yarn.resourcemanager.system-metrics-publisher.timeline-server-v1.enable-batch": "true",
  "yarn.resourcemanager.system-metrics-publisher.enabled": "true"
  },
  "Configurations": []
  }
  ]
  ```
+ WebHDFS and HttpFS server are disabled by default\. You can re\-enable WebHDFS using the Hadoop configuration, `dfs.webhdfs.enabled`\. HttpFS server can be started by using `sudo systemctl start hadoop-httpfs`\.
+ HTTPS is now enabled by default for Amazon Linux repositories\. If you are using an Amazon S3 VPCE policy to restrict access to specific buckets, you must add the new Amazon Linux bucket ARN `arn:aws:s3:::amazonlinux-2-repos-$region/*` to your policy \(replace `$region` with the region where the endpoint is\)\. For more information, see this topic in the AWS discussion forums\. [Announcement: Amazon Linux 2 now supports the ability to use HTTPS while connecting to package repositories ](https://forums.aws.amazon.com/ann.jspa?annID=8528)\. 
+ Hive: Write query performance is improved by enabling the use of a scratch directory on HDFS for the last job\. The temporary data for final job is written to HDFS instead of Amazon S3 and performance is improved because the data is moved from HDFS to the final table location \(Amazon S3\) instead of between Amazon S3 devices\.
+ Hive: Query compilation time improvement up to 2\.5x with Glue metastore Partition Pruning\.
+ By default, when built\-in UDFs are passed by Hive to the Hive Metastore Server, only a subset of those built\-in UDFs are passed to the Glue Metastore since Glue supports only limited expression operators\. If you set `hive.glue.partition.pruning.client=true`, then all partition pruning happens on the client side\. If the you set `hive.glue.partition.pruning.server=true`, then all partition pruning happens on the server side\. 

**Known issues**
+ Hue queries do not work in Amazon EMR 6\.4\.0 because Apache Hadoop HttpFS server is disabled by default\. To use Hue on Amazon EMR 6\.4\.0, either manually start HttpFS server on the Amazon EMR master node using `sudo systemctl start hadoop-httpfs`, or [use an Amazon EMR step](https://docs.aws.amazon.com/emr/latest/ManagementGuide/add-step-cli.html)\.
+ The Amazon EMR Notebooks feature used with Livy user impersonation does not work because HttpFS is disabled by default\. In this case, the EMR notebook cannot connect to the cluster that has Livy impersonation enabled\. The workaround is to start HttpFS server before connecting the EMR notebook to the cluster using `sudo systemctl start hadoop-httpfs`\.
+ In Amazon EMR version 6\.4\.0, Phoenix does not support the Phoenix connectors component\.

## Release 5\.33\.0 \(latest version of Amazon EMR 5\.x series\)<a name="emr-5330-whatsnew"></a>

New Amazon EMR release versions are made available in different Regions over a period of several days, beginning with the first Region on the initial release date\. The latest release version may not be available in your Region during this period\.

The following release notes include information for Amazon EMR release version 5\.33\.0\. Changes are relative to 5\.32\.0\.

Initial release date: April 19, 2021

Last updated date: August 9, 2021

**Upgrades**
+ Upgraded Amazon Glue connector to version 1\.15\.0
+ Upgraded to version 1\.11\.970
+ Upgraded EMRFS to version 2\.46\.0
+ Upgraded EMR Goodies to version 2\.14\.0
+ Upgraded EMR Record Server to version 1\.9\.0
+ Upgraded EMR S3 Dist CP to version 2\.18\.0
+ Upgraded EMR Secret Agent to version 1\.8\.0
+ Upgraded Flink to version 1\.12\.1
+ Upgraded Hadoop to version 2\.10\.1\-amzn\-1
+ Upgraded Hive to version 2\.3\.7\-amzn\-4
+ Upgraded Hudi to version 0\.7\.0
+ Upgraded Hue to version 4\.9\.0
+ Upgraded OpenCV to version 4\.5\.0
+ Upgraded Presto to version 0\.245\.1\-amzn\-0
+ Upgraded R to version 4\.0\.2
+ Upgraded Spark to version 2\.4\.7\-amzn\-1
+ Upgraded TensorFlow to version 2\.4\.1
+ Upgraded Zeppelin to version 0\.9\.0

**Changes, enhancements, and resolved issues**
+ **Configuring a cluster to fix Apache YARN Timeline Server version 1 and 1\.5 performance issues**

  Apache YARN Timeline Server version 1 and 1\.5 can cause performance issues with very active, large EMR clusters, particularly with `yarn.resourcemanager.system-metrics-publisher.enabled=true`, which is the default setting in EMR\. An open source YARN Timeline Server v2 solves the performance issue related to YARN Timeline Server scalability\.

  Other workarounds for this issue include:
  + Configuring yarn\.resourcemanager\.system\-metrics\-publisher\.enabled=false in yarn\-site\.xml\.
  + Enabling the fix for this issue when creating a cluster, as described below\.

  The following Amazon EMR release versions contain a fix for this YARN Timeline Server performance issue\.

  EMR 5\.30\.2, 5\.31\.1, 5\.32\.1, 5\.33\.1, 5\.34\.x, 6\.0\.1, 6\.1\.1, 6\.2\.1, 6\.3\.1, 6\.4\.x

  To enable the fix on any of the above specified Amazon EMR releases, set these properties to `true` in a configurations JSON file that is passed in using the [`aws emr create-cluster` command parameter](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-create-cluster.html): `--configurations file://./configurations.json`\. Or enable the fix using the [reconfiguration console UI](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

  Example of the configurations\.json file contents:

  ```
  [
  {
  "Classification": "yarn-site",
  "Properties": {
  "yarn.resourcemanager.system-metrics-publisher.timeline-server-v1.enable-batch": "true",
  "yarn.resourcemanager.system-metrics-publisher.enabled": "true"
  },
  "Configurations": []
  }
  ]
  ```
+ Amazon EMR version 5\.33\.1 fixed issues with Managed Scaling unable to complete or causing application failures\.
+ Spark runtime is now faster when fetching partition locations from Hive Metastore for Spark insert queries\.
+ Upgraded component versions\. For a list of component versions, see [About Amazon EMR Releases](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-components.html) in this guide\.
+ Installed the AWS Java SDK Bundle on each new cluster\. This is a single jar containing all service SDKs and their dependencies, instead of individual component jars\. For more information, see [Java SDK Bundled Dependency](http://aws.amazon.com/blogs/developer/java-sdk-bundle/)\.
+ Fixed Managed Scaling issues in earlier Amazon EMR releases and made improvements so application failure rates are significantly reduced\.

**New features**
+ Amazon EMR supports Amazon S3 Access Points, a feature of Amazon S3 that allows you to easily manage access for shared data lakes\. Using your Amazon S3 Access Point alias, you can simplify your data access at scale on Amazon EMR\. You can use Amazon S3 Access Points with all versions of Amazon EMR at no additional cost in all AWS regions where Amazon EMR is available\. To learn more about Amazon S3 Access Points and Access Point aliases, see [Using a bucket\-style alias for your access point](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-points-alias.html) in the *Amazon S3 User Guide*\.
+ Amazon EMR\-5\.33 supports new Amazon EC2 instance types: c5a, c5ad, c6gn, c6gd, m6gd, d3, d3en, m5zn, r5b, r6gd\. See [Supported Instance Types](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-supported-instance-types.html)\.

**Known issues**
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
Amazon EMR clusters that are running Amazon Linux or Amazon Linux 2 AMIs \(Amazon Linux Machine Images\) use default Amazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If new Amazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an Amazon EMR version is released, Amazon EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latest Amazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
+ Console support to create a security configuration that specifies the AWS Ranger integration option is currently not supported in the GovCloud Region\. Security configuration can be done using the CLI\. See [Create the EMR Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger-security-config.html) in the *Amazon EMR Management Guide*\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.