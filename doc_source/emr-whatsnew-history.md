# Amazon EMR What's New History<a name="emr-whatsnew-history"></a>

Release notes for all Amazon EMR release versions are available below\. For comprehensive release information for each release, see [Amazon EMR 5\.x Release Versions](emr-release-5x.md) and [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

## Release 5\.33\.0<a name="emr-5330-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.33\.0\. Changes are relative to 5\.32\.0\.

Initial release date: Apr 19, 2021

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

**Changes, Enhancements, and Resolved Issues**
+ Upgraded component versions\.
+ For a list of component versions, see [About Amazon EMR Releases](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-components.html) in this guide\.

**New Features**
+ Amazon EMR\-5\.33 supports new Amazon EC2 instance types: c5a, c5ad, c6gn, c6gd, m6gd, d3, d3en, m5zn, r5b, r6gd\. See [Supported Instance Types](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-supported-instance-types.html)\.

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
Amazon EMR clusters that are runningAmazon Linux orAmazon Linux 2 AMIs \(Amazon Linux Machine Images\) use defaultAmazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If newAmazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an EMR version is released, EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latestAmazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
+ Console support to create a security configuration that specifies the AWS Ranger integration option is currently not supported in the GovCloud region\. Security configuration can be done using the CLI\. See [Create the EMR Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger-security-config.html) in the *Amazon EMR Management Guide*\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.

## Release 5\.32\.0<a name="emr-5320-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.32\.0\. Changes are relative to 5\.31\.0\.

Initial release date: Jan 8, 2021

**Upgrades**
+ Upgraded Amazon Glue connector to version 1\.14\.0
+ Upgraded Amazon SageMaker Spark SDK to version 1\.4\.1
+ Upgraded to version 1\.11\.890
+ Upgraded EMR DynamoDB Connector version 4\.16\.0
+ Upgraded EMRFS to version 2\.45\.0
+ Upgraded EMR Log Analytics Metrics to version 1\.18\.0
+ Upgraded EMR MetricsAndEventsApiGateway Client to version 1\.5\.0
+ Upgraded EMR Record Server to version 1\.8\.0
+ Upgraded EMR S3 Dist CP to version 2\.17\.0
+ Upgraded EMR Secret Agent to version 1\.7\.0
+ Upgraded Flink to version 1\.11\.2
+ Upgraded Hadoop to version 2\.10\.1\-amzn\-0
+ Upgraded Hive to version 2\.3\.7\-amzn\-3
+ Upgraded Hue to version 4\.8\.0
+ Upgraded Mxnet to version 1\.7\.0
+ Upgraded OpenCV to version 4\.4\.0
+ Upgraded Presto to version 0\.240\.1\-amzn\-0
+ Upgraded Spark to version 2\.4\.7\-amzn\-0
+ Upgraded TensorFlow to version 2\.3\.1

**Changes, Enhancements, and Resolved Issues**
+ Upgraded component versions\.
+ For a list of component versions, see [About Amazon EMR Releases](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-components.html) in this guide\.

**New Features**
+ Instance Metadata Service \(IMDS\) V2 support status: Amazon EMR 5\.23\.1, 5\.27\.1 and 5\.32 or later components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. For other 5\.x EMR releases, disabling IMDSv1 causes cluster startup failure\.
+ Beginning with Amazon EMR 5\.32\.0, you can launch a cluster that natively integrates with Apache Ranger\. Apache Ranger is an open\-source framework to enable, monitor, and manage comprehensive data security across the Hadoop platform\. For more information, see [Apache Ranger](https://ranger.apache.org/)\. With native integration, you can bring your own Apache Ranger to enforce fine\-grained data access control on Amazon EMR\. See [Integrate Amazon EMR with Apache Ranger](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger.html) in the *Amazon EMR Release Guide*\.
+ Amazon EMR Release 5\.32\.0 supports Amazon EMR on EKS\. For more details on getting started with EMR on EKS, see [What is Amazon EMR on EKS](https://docs.aws.amazon.com/emr/latest/EMR-on-EKS-DevelopmentGuide/emr-eks.html)\.
+ Amazon EMR Release 5\.32\.0 supports Amazon EMR Studio \(Preview\)\. For more details on getting started with EMR Studio, see [Amazon EMR Studio \(Preview\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-studio.html)\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
Amazon EMR clusters that are runningAmazon Linux orAmazon Linux 2 AMIs \(Amazon Linux Machine Images\) use defaultAmazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If newAmazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an EMR version is released, EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latestAmazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
+ Console support to create a security configuration that specifies the AWS Ranger integration option is currently not supported in the GovCloud region\. Security configuration can be done using the CLI\. See [Create the EMR Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger-security-config.html) in the *Amazon EMR Management Guide*\.
+ When AtRestEncryption or HDFS encryption is enabled on a cluster that uses EMR 5\.31\.0 or 5\.32\.0, Hive queries result in the following runtime exception\. 

  ```
  TaskAttempt 3 failed, info=[Error: Error while running task ( failure ) : attempt_1604112648850_0001_1_01_000000_3:java.lang.RuntimeException: java.lang.RuntimeException: Hive Runtime Error while closing operators: java.io.IOException: java.util.ServiceConfigurationError: org.apache.hadoop.security.token.TokenIdentifier: Provider org.apache.hadoop.hbase.security.token.AuthenticationTokenIdentifier not found
  ```

## Release 6\.2\.0<a name="emr-620-whatsnew"></a>

The following release notes include information for Amazon EMR release version 6\.2\.0\. Changes are relative to 6\.1\.0\.

Initial release date: Dec 09, 2020

Last updated date: Mar 24, 2021

**Supported Applications**
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

**New Features**
+ HBase: Removed rename in commit phase and added persistent HFile tracking\. See [Persistent HFile Tracking](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-hfile-tracking) in the *Amazon EMR Release Guide*\.
+ HBase: Backported [Create a config that forces to cache blocks on compaction](https://issues.apache.org/jira/browse/HBASE-23066)\.
+ PrestoDB: Improvements to Dynamic Partition Pruning\. Rule\-based Join Reorder works on non\-partitioned data\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.
+ Instance Metadata Service \(IMDS\) V2 support status: For Amazon EMR 6\.2 or later, Amazon EMR components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. If you disable IMDSv1 in earlier Amazon EMR 6\.x releases, it causes cluster startup failure\.

**Changes, Enhancements, and Resolved Issues**
+ Spark: Performance improvements in Spark runtime\.

**Known Issues**
+ HTTPD fails on EMR 6\.2\.0 clusters when you use a security configuration\. This makes the Ganglia web application user interface unavailable\. To access the Ganglia web application user interface, add `Listen 80` to the `/etc/httpd/conf/httpd.conf` file on the master node of your cluster\. For information about connecting to your cluster, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html)\.

  EMR Notebooks also fail to establish a connection with EMR 6\.2\.0 clusters when you use a security configuration\. The notebook will fail to list kernels and submit Spark jobs\. We recommend that you use EMR Notebooks with another version of Amazon EMR instead\.
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
Amazon EMR clusters that are runningAmazon Linux orAmazon Linux 2 AMIs \(Amazon Linux Machine Images\) use defaultAmazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If newAmazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an EMR version is released, EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latestAmazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
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

## Release 5\.31\.0<a name="emr-5310-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.31\.0\. Changes are relative to 5\.30\.1\.

Initial release date: Oct 9, 2020

Last updated date: Oct 15, 2020

**Upgrades**
+ Upgraded Amazon Glue connector to version 1\.13\.0
+ Upgraded Amazon SageMaker Spark SDK to version 1\.4\.0
+ Upgraded Amazon Kinesis connector to version 3\.5\.9 
+ Upgraded to version 1\.11\.852
+ Upgraded Bigtop\-tomcat to version 8\.5\.56
+ Upgraded EMR FS to version 2\.43\.0
+ Upgraded EMR MetricsAndEventsApiGateway Client to version 1\.4\.0
+ Upgraded EMR S3 Dist CP to version 2\.15\.0
+ Upgraded EMR S3 Select to version 1\.6\.0
+ Upgraded Flink to version 1\.11\.0
+ Upgraded Hadoop to version 2\.10\.0
+ Upgraded Hive to version 2\.3\.7
+ Upgraded Hudi to version 0\.6\.0
+ Upgraded Hue to version 4\.7\.1
+ Upgraded JupyterHub to version 1\.1\.0
+ Upgraded Mxnet to version 1\.6\.0
+ Upgraded OpenCV to version 4\.3\.0
+ Upgraded Presto to version 0\.238\.3
+ Upgraded TensorFlow to version 2\.1\.0

**Changes, Enhancements, and Resolved Issues**
+ [Hive column statistics](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ColumnStatistics) are supported for Amazon EMR versions 5\.31\.0 and later\.
+ Upgraded component versions\.
+ EMRFS S3EC V2 Support in Amazon EMR 5\.31\.0\. In S3 Java SDK releases 1\.11\.837 and later, encryption client Version 2 \(S3EC V2\) has been introduced with various security enhancements\. For more information, see the following:
  + S3 blog post: [Updates to the Amazon S3 Encryption Client](https://aws.amazon.com/blogs/developer/updates-to-the-amazon-s3-encryption-client/)\.
  +  Developer Guide: [Migrate Encryption and Decryption Clients to V2](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/s3-encryption-migration.html#s3-cse-update-code)\.
  + EMR Management Guide: [Amazon S3 Client\-Side Encryption](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-encryption-cse.html)\.

  Encryption Client V1 is still available in the SDK for backward compatibility\.

**New Features**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
+ With Amazon EMR 5\.31\.0, you can launch a cluster that integrates with Lake Formation\. This integration provides fine\-grained, column\-level data filtering to databases and tables in the AWS Glue Data Catalog\. It also enables federated single sign\-on to EMR Notebooks or Apache Zeppelin from an enterprise identity system\. For more information, see [Integrating Amazon EMR with AWS Lake Formation](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-lake-formation.html) in the *Amazon EMR Management Guide*\.

  Amazon EMR with Lake Formation is currently available in 16 AWS Regions: US East \(Ohio and N\. Virginia\), US West \(N\. California and Oregon\), Asia Pacific \(Mumbai, Seoul, Singapore, Sydney, and Tokyo\), Canada \(Central\), Europe \(Frankfurt, Ireland, London, Paris, and Stockholm\), South America \(São Paulo\)\.

**Known Issues**
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
+ When AtRestEncryption or HDFS encryption is enabled on a cluster that uses EMR 5\.31\.0 or 5\.32\.0, Hive queries result in the following runtime exception\. 

  ```
  TaskAttempt 3 failed, info=[Error: Error while running task ( failure ) : attempt_1604112648850_0001_1_01_000000_3:java.lang.RuntimeException: java.lang.RuntimeException: Hive Runtime Error while closing operators: java.io.IOException: java.util.ServiceConfigurationError: org.apache.hadoop.security.token.TokenIdentifier: Provider org.apache.hadoop.hbase.security.token.AuthenticationTokenIdentifier not found
  ```

## Release 6\.1\.0<a name="emr-610-whatsnew"></a>

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
+ Spark version 3\.0\.0\-amzn\-0
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
+ ECR auto authentication support on Apache Hadoop and Apache Spark with Docker: Spark users can use Docker images from Docker Hub and Amazon Elastic Container Registry \(Amazon ECR\) to define environment and library dependencies\.

  [Configure Docker](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html) and [Run Spark Applications with Docker Using Amazon EMR 6\.x](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-docker.html)\.
+ EMR supports Apache Hive ACID transactions: Amazon EMR 6\.1\.0 adds support for Hive ACID transactions so it complies with the ACID properties of a database\. With this feature, you can run INSERT, UPDATE, DELETE, and MERGE operations in Hive managed tables with data in Amazon Simple Storage Service \(Amazon S3\)\. This is a key feature for use cases like streaming ingestion, data restatement, bulk updates using MERGE, and slowly changing dimensions\. For more information, including configuration examples and use cases, see [Amazon EMR supports Apache Hive ACID transactions](https://aws.amazon.com/blogs/big-data/amazon-emr-supports-apache-hive-acid-transactions)\.

**Changes, Enhancements, and Resolved Issues**
+ Apache Flink is not supported on EMR 6\.0\.0, but it is supported on EMR 6\.1\.0 with Flink 1\.11\.0\. This is the first version of Flink to officially support Hadoop 3\. See [Apache Flink 1\.11\.0 Release Announcement](https://flink.apache.org/news/2020/07/06/release-1.11.0.html)\.
+ Ganglia has been removed from default EMR 6\.1\.0 package bundles\.

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
+ If you set custom garbage collection configuration with `spark.driver.extraJavaOptions` and `spark.executor.extraJavaOptions`, this will result in driver/executor launch failure with EMR 6\.1 due to conflicting garbage collection configuration\. With EMR Release 6\.1\.0, you should specify custom Spark garbage collection configuration for drivers and executors with the properties `spark.driver.defaultJavaOptions` and `spark.executor.defaultJavaOptions` instead\. Read more in [Apache Spark Runtime Environment](https://spark.apache.org/docs/latest/configuration.html#runtime-environment) and [Configuring Spark Garbage Collection on Amazon EMR 6\.1\.0](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-configure.html#spark-gc-config)\.
+ Using Pig with Oozie \(and within Hue, since Hue uses Oozie actions to run Pig scripts\), generates an error that a native\-lzo library cannot be loaded\. This error message is informational and does not block Pig from running\.
+ Hudi Concurrency Support: Currently Hudi doesn't support concurrent writes to a single Hudi table\. In addition, Hudi rolls back any changes being done by in\-progress writers before allowing a new writer to start\. Concurrent writes can interfere with this mechanism and introduce race conditions, which can lead to data corruption\. You should ensure that as part of your data processing workflow, there is only a single Hudi writer operating against a Hudi table at any time\. Hudi does support multiple concurrent readers operating against the same Hudi table\.
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
+ There is an issue in Amazon EMR 6\.1\.0 that affects clusters running Presto\. After an extended period of time \(days\), the cluster may throw errors such as, “su: failed to execute /bin/bash: Resource temporarily unavailable” or “shell request failed on channel 0”\. This issue is caused by an internal Amazon EMR process \(InstanceController\) that is spawning too many Light Weight Processes \(LWP\), which eventually causes the Hadoop user to exceed their nproc limit\. This prevents the user from opening additional processes\. The solution for this issue is to upgrade to EMR 6\.2\.0\.

## Release 6\.0\.0<a name="emr-600-whatsnew"></a>

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
  + `systemd` is used for service management instead of `upstart` used inAmazon Linux 1\.
+ Java Development Kit \(JDK\)
  + Coretto JDK 8 is the default JDK for the EMR 6\.x release series\.
+ Scala
  + Scala 2\.12 is used with Apache Spark and Apache Livy\.
+ Python 3
  + Python 3 is now the default version of Python in EMR\.
+ YARN node labels
  + Beginning with Amazon EMR 6\.x release series, the YARN node labels feature is disabled by default\. The application master processes can run on both core and task nodes by default\. You can enable the YARN node labels feature by configuring following properties: `yarn.node-labels.enabled` and `yarn.node-labels.am.default-node-label-expression`\. For more information, see [Understanding Master, Core, and Task Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-master-core-task-nodes.html)\.

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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

## Release 5\.30\.1<a name="emr-5301-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.30\.1\. Changes are relative to 5\.30\.0\.

Initial release date: June 30, 2020

Last updated date: August 24, 2020

**Changes, Enhancements, and Resolved Issues**
+ Fixed issue where instance controller process spawned infinite number of processes\.
+ Fixed issue where Hue was unable to run an Hive query, showing a "database is locked" message and preventing the execution of queries\.
+ Fixed a Spark issue to enable more tasks to run concurrently on the EMR cluster\.
+ Fixed a Jupyter notebook issue causing a "too many files open error" in the Jupyter server\.
+ Fixed an issue with cluster start times\.

**New Features**
+ Tez UI and YARN timeline server persistent application interfaces are available with Amazon EMR versions 6\.x, and EMR version 5\.30\.1 and later\. One\-click link access to persistent application history lets you quickly access job history without setting up a web proxy through an SSH connection\. Logs for active and terminated clusters are available for 30 days after the application ends\. For more information, see [View Persistent Application User Interfaces](https://docs.aws.amazon.com/emr/latest/ManagementGuide/app-history-spark-UI.html) in the *Amazon EMR Management Guide*\.
+ EMR Notebook execution APIs are available to execute EMR notebooks via a script or command line\. The ability to start, stop, list, and describe EMR notebook executions without the AWS console enables you programmatically control an EMR notebook\. Using a parameterized notebook cell, you can pass different parameter values to a notebook without having to create a copy of the notebook for each new set of paramter values\. See [EMR API Actions\.](https://docs.aws.amazon.com/emr/latest/APIReference/API_Operations.html) For sample code, see [Sample commands to execute EMR Notebooks programmatically\.](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-headless.html)

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
+ **EMR Notebooks**

  The feature that allows you to install kernels and additional Python libraries on the cluster master node is disabled by default on EMR version 5\.30\.1\. For more information about this feature, see [Installing Kernels and Python Libraries on a Cluster Master Node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-installing-libraries-and-kernels.html)\.

  To enable the feature, do the following:

  1. Make sure that the permissions policy attached to the service role for EMR Notebooks allows the following action:

     `elasticmapreduce:ListSteps`

     For more information, see [Service Role for EMR Notebooks](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-service-role.html)\.

  1. Use the AWS CLI to run a step on the cluster that sets up EMR Notebooks as shown in the following example\. Replace *us\-east\-1* with the Region in which your cluster resides\. For more information, see [Adding Steps to a Cluster Using the AWS CLI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/add-step-cli.html)\.

     ```
     aws emr add-steps  --cluster-id MyClusterID --steps Type=CUSTOM_JAR,Name=EMRNotebooksSetup,ActionOnFailure=CONTINUE,Jar=s3://us-east-1.elasticmapreduce/libs/script-runner/script-runner.jar,Args=["s3://awssupportdatasvcs.com/bootstrap-actions/EMRNotebooksSetup/emr-notebooks-setup.sh"]
     ```
+ **Managed scaling**

  Managed scaling operations on 5\.30\.0 and 5\.30\.1 clusters without Presto installed may cause application failures or cause a uniform instance group or instance fleet to stay in the `ARRESTED` state, particularly when a scale down operation is followed quickly by a scale up operation\.

  As a workaround, choose Presto as an application to install when you create a cluster, even if your job does not require Presto\.
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

## Release 5\.30\.0<a name="emr-5300-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.30\.0\. Changes are relative to 5\.29\.0\.

Initial release date: May 13, 2020

Last updated date: June 25, 2020

**Upgrades**
+ Upgraded AWS SDK for Java to version 1\.11\.759
+ Upgraded Amazon SageMaker Spark SDK to version 1\.3\.0
+ Upgraded EMR Record Server to version 1\.6\.0
+ Upgraded Flink to version 1\.10\.0
+ Upgraded Ganglia to version 3\.7\.2
+ Upgraded HBase to version 1\.4\.13
+ Upgraded Hudi to version 0\.5\.2\-incubating
+ Upgraded Hue to version 4\.6\.0
+ Upgraded JupyterHub to version 1\.1\.0
+ Upgraded Livy to version 0\.7\.0\-incubating
+ Upgraded Oozie to version 5\.2\.0
+ Upgraded Presto to version 0\.232
+ Upgraded Spark to version 2\.4\.5
+ Upgraded Connectors and drivers: Amazon Glue Connector 1\.12\.0; Amazon Kinesis Connector 3\.5\.0; EMR DynamoDB Connector 4\.14\.0

**New Features**
+ **EMR Notebooks** – When used with EMR clusters created using 5\.30\.0, EMR notebook kernels run on cluster\. This improves notebook performance and allows you to install and customize kernels\. You can also install Python libraries on the cluster master node\. For more information, see [Installing and Using Kernels and Libraries](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-installing-libraries-and-kernels.html) in the *EMR Management Guide*\.
+ **Managed Scaling** – With Amazon EMR version 5\.30\.0 and later, you can enable EMR managed scaling to automatically increase or decrease the number of instances or units in your cluster based on workload\. EMR continuously evaluates cluster metrics to make scaling decisions that optimize your clusters for cost and speed\. For more information, see [Scaling Cluster Resources](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-scale-on-demand.html) in the *Amazon EMR Management Guide*\.
+ **Encrypt log files stored in Amazon S3** – With Amazon EMR version 5\.30\.0 and later, you can encrypt log files stored in Amazon S3 with an AWS KMS customer managed key\. For more information, see [Encrypt log files stored in Amazon S3](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-debugging.html#emr-log-encryption) in the *Amazon EMR Management Guide*\.
+ **Amazon Linux 2 support** – In EMR version 5\.30\.0 and later, EMR usesAmazon Linux 2 OS\. New custom AMIs \(Amazon Machine Image\) must be based on theAmazon Linux 2 AMI\. For more information, see [Using a Custom AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html)\.
+ **Presto Graceful Auto Scale** – EMR clusters using 5\.30\.0 can be set with an auto scaling timeout period that gives Presto tasks time to finish running before their node is decommissioned\. For more information, see [Using Presto Auto Scaling with Graceful Decommission](presto-graceful-autoscale.md)\.
+ **Fleet Instance creation with new allocation strategy option** – A new allocation strategy option is available in EMR version 5\.12\.1 and later\. It offers faster cluster provisioning, more accurate spot allocation, and less spot instance interruption\. Updates to non\-default EMR service roles are required\. See [Configure Instance Fleets](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-instance-fleet.html)\.
+ **sudo systemctl stop and sudo systemctl start commands** – In EMR version 5\.30\.0 and later, which useAmazon Linux 2 OS, EMR uses `sudo systemctl stop` and `sudo systemctl start` commands to restart services\. For more information, see [How do I restart a service in Amazon EMR?](https://aws.amazon.com/premiumsupport/knowledge-center/restart-service-emr/)\.

**Changes, Enhancements, and Resolved Issues**
+ EMR version 5\.30\.0 doesn't install Ganglia by default\. You can explicitly select Ganglia to install when you create a cluster\.
+ Spark performance optimizations\.
+ Presto performance optimizations\.
+ Python 3 is the default for Amazon EMR version 5\.30\.0 and later\.
+ The default managed security group for service access in private subnets has been updated with new rules\. If you use a custom security group for service access, you must include the same rules as the default managed security group\. For more information, see [Amazon EMR\-Managed Security Group for Service Access \(Private Subnets\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-man-sec-groups.html#emr-sg-elasticmapreduce-sa-private)\. If you use a custom service role for Amazon EMR, you must grant permission to `ec2:describeSecurityGroups` so that EMR can validate if the security groups are correctly created\. If you use the `EMR_DefaultRole`, this permission is already included in the default managed policy\.

**Known Issues**
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions ofAmazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latestAmazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
+ **Managed scaling**

  Managed scaling operations on 5\.30\.0 and 5\.30\.1 clusters without Presto installed may cause application failures or cause a uniform instance group or instance fleet to stay in the `ARRESTED` state, particularly when a scale down operation is followed quickly by a scale up operation\.

  As a workaround, choose Presto as an application to install when you create a cluster, even if your job does not require Presto\.
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

## Release 5\.29\.0<a name="emr-5290-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.29\.0\. Changes are relative to 5\.28\.1\.

Initial release date: Jan 17, 2020

**Upgrades**
+ Upgraded to version 1\.11\.682
+ Upgraded Hive to version 2\.3\.6
+ Upgraded Flink to version 1\.9\.1
+ Upgraded EmrFS to version 2\.38\.0
+ Upgraded EMR DynamoDB Connector to version 4\.13\.0

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Spark performance optimizations\.
+ EMRFS
  + Management Guide updates to emrfs\-site\.xml default settings for consistent view\.

**Known Issues**
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

## Release 5\.28\.1<a name="emr-5281-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.28\.1\. Changes are relative to 5\.28\.0\.

Initial release date: Jan 10, 2020

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Fixed Spark compatibility issues\.
+ CloudWatch Metrics
  + Fixed Amazon CloudWatch Metrics publishing on an EMR cluster with multiple master nodes\.
+ Disabled log message
  + Disabled false log message, "\.\.\.using old version \(<4\.5\.8\) of Apache http client\."

**Known Issues**
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

## Release 5\.28\.0<a name="emr-5280-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.28\.0\. Changes are relative to 5\.27\.0\.

Initial release date: Nov 12, 2019

**Upgrades**
+ Upgraded Flink to version 1\.9\.0
+ Upgraded Hive to version 2\.3\.6
+ Upgraded MXNet to version 1\.5\.1
+ Upgraded Phoenix to version 4\.14\.3
+ Upgraded Presto to version 0\.227
+ Upgraded Zeppelin to version 0\.8\.2

**New Features**
+ [Apache Hudi](https://hudi.apache.org/) is now available for Amazon EMR to install when you create a cluster\. For more information, see [Hudi](emr-hudi.md)\.
+ \(Nov 25, 2019\) You can now choose to run multiple steps in parallel to improve cluster utilization and save cost\. You can also cancel both pending and running steps\. For more information, see [Work with Steps Using the AWS CLI and Console](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-work-with-steps.html)\.
+ \(Dec 3, 2019\) You can now create and run EMR clusters on AWS Outposts\. AWS Outposts enables native AWS services, infrastructure, and operating models in on\-premises facilities\. In AWS Outposts environments, you can use the same AWS APIs, tools, and infrastructure that you use in the AWS cloud\. For more information, see [EMR Clusters on AWS Outposts](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-outposts.html)\.
+ \(Mar 11, 2020\) Beginning with Amazon EMR version 5\.28\.0, you can create and run Amazon EMR clusters on an AWS Local Zones subnet as a logical extension of an AWS Region that supports Local Zones\. A Local Zone enables Amazon EMR features and a subset of AWS services, like compute and storage services, to be located closer to users, providing very low latency access to applications running locally\. For a list of available Local Zones, see [AWS Local Zones](https://aws.amazon.com/about-aws/global-infrastructure/localzones/)\. For information about accessing available AWS Local Zones, see [Regions, Availability Zones, and Local Zones](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/using-regions-availability-zones.html)\.

  Local Zones donâ€™t currently support Amazon EMR Notebooks and do not support connections directly to Amazon EMR using interface VPC endpoint \(AWS PrivateLink\)\.

**Changes, Enhancements, and Resolved Issues**
+ Expanded Application Support for High Availability Clusters
  + For more information, see [Supported Applications in an EMR Cluster with Multiple Master Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-applications.html#emr-plan-ha-applications-list) in the *Amazon EMR Management Guide*\.
+ Spark
  + Performance optimizations
+ Hive
  + Performance optimizations
+ Presto
  + Performance optimizations

**Known Issues**
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

## Release 5\.27\.0<a name="emr-5270-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.27\.0\. Changes are relative to 5\.26\.0\.

Initial release date: Sep 23, 2019

**Upgrades**
+ AWS SDK for Java 1\.11\.615
+ Flink 1\.8\.1
+ JupyterHub 1\.0\.0
+ Spark 2\.4\.4
+ Tensorflow 1\.14\.0
+ Connectors and drivers:
  + DynamoDB Connector 4\.12\.0

**New Features**
+ \(Oct 24, 2019\) The following new features in EMR notebooks are available with all Amazon EMR releases\.
  + Instance Metadata Service \(IMDS\) V2 support status: Amazon EMR 5\.23\.1, 5\.27\.1 and 5\.32 or later components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. For other 5\.x EMR releases, disabling IMDSv1 causes cluster startup failure\.
  + You can now associate Git repositories with EMR notebooks to store your notebooks in a version controlled environment\. You can share code with peers and reuse existing Jupyter notebooks through remote Git repositories\. For more information, see [Associate Git Repositories with Amazon EMR Notebooks](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-git-repo.html) in the *Amazon EMR Management Guide*\.
  + The [nbdime utility](https://github.com/jupyter/nbdime)Â is now available in EMR notebooks to simplify comparing and merging notebooks\. Â 
  + EMR notebooks now support JupyterLab\. JupyterLab is a web\-based interactive development environment fully compatible with Jupyter notebooks\. You can now choose to open your notebook in either JupyterLab or Jupyter notebook editor\.Â 
+ \(Oct 30, 2019\) With Amazon EMR versions 5\.25\.0 and later, you can connect to Spark history server UI from the cluster **Summary** page or the **Application history** tab in the console\. Instead of setting up a web proxy through an SSH connection, you can quickly access the Spark history server UI to view application metrics and access relevant log files for active and terminated clusters\. For more information, see [Off\-cluster access to persistent application user interfaces](https://docs.aws.amazon.com/emr/latest/ManagementGuide/app-history-spark-UI.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ EMR cluster with multiple master nodes
  + You can install and run Flink on an EMR cluster with multiple master nodes\. For more information, see [Supported Applications and Features](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-applications.html)\.
  + You can configure HDFS transparent encryption on an EMR cluster with multiple master nodes\. For more information, see [HDFS Transparent Encryption on EMR Clusters with Multiple Master Nodes](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-encryption-tdehdfs.html#emr-hadoop-kms-multi-master)\.
  + You can now modify the configuration of applications running on an EMR cluster with multiple master nodes\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.
+ Amazon EMR\-DynamoDB Connector
  + Amazon EMR\-DynamoDB Connector now supports the following DynamoDB data types: boolean, list, map, item, null\. For more information, see [Set Up a Hive Table to Run Hive Commands](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/EMR_Interactive_Hive.html)\.

**Known Issues**
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

## Release 5\.26\.0<a name="emr-5260-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.26\.0\. Changes are relative to 5\.25\.0\.

Initial release date: Aug 8, 2019

Last updated date: Aug 19, 2019

**Upgrades**
+ AWS SDK for Java 1\.11\.595
+ HBase 1\.4\.10
+ Phoenix 4\.14\.2
+ Connectors and drivers:
  + DynamoDB Connector 4\.11\.0
  + MariaDB Connector 2\.4\.2
  + Amazon Redshift JDBC Driver 1\.2\.32\.1056

**New Features**
+ \(Beta\) With Amazon EMR 5\.26\.0, you can launch a cluster that integrates with Lake Formation\. This integration provides fine\-grained, column\-level access to databases and tables in the AWS Glue Data Catalog\. It also enables federated single sign\-on to EMR Notebooks or Apache Zeppelin from an enterprise identity system\. For more information, see [Integrating Amazon EMR with AWS Lake Formation \(Beta\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-lake-formation.html)\.
+ \(Aug 19, 2019\) Amazon EMR block public access is now available with all Amazon EMR releases that support security groups\. Block public access is an account\-wide setting applied to each AWS Region\. Block public access prevents a cluster from launching when any security group associated with the cluster has a rule that allows inbound traffic from IPv4 0\.0\.0\.0/0 or IPv6 ::/0 \(public access\) on a port, unless a port is specified as an exception\. Port 22 is an exception by default\. For more information, see [Using Amazon EMR Block Public Access](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-block-public-access.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ EMR Notebooks
  + With EMR 5\.26\.0 and later, EMR Notebooks supports notebook\-scoped Python libraries in addition to the default Python libraries\. You can install notebook\-scoped libraries from within the notebook editor without having to re\-create a cluster or re\-attach a notebook to a cluster\. Notebook\-scoped libraries are created in a Python virtual environment, so they apply only to the current notebook session\. This allows you to isolate notebook dependencies\. For more information, see [Using Notebook Scoped Libraries](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-notebooks-scoped-libraries.html) in the *Amazon EMR Management Guide*\.
+ EMRFS
  + You can enable an ETag verification feature \(Beta\) by setting `fs.s3.consistent.metadata.etag.verification.enabled` to `true`\. With this feature, EMRFS uses Amazon S3 ETags to verify that objects being read are the latest available version\. This feature is helpful for read\-after\-update use cases in which files on Amazon S3 are overwritten while retaining the same name\. This ETag verification capability currently does not work with S3 Select\. For more information, see [Configure Consistent View](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emrfs-configure-consistent-view.html)\.
+ Spark
  + The following optimizations are now enabled by default: dynamic partition pruning, DISTINCT before INTERSECT, improvements in SQL plan statistics inference for JOIN followed by DISTINCT queries, flattening scalar subqueries, optimized join reorder, and bloom filter join\. For more information, see [Optimizing Spark Performance](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-performance.html)\.
  + Improved whole stage code generation for Sort Merge Join\.
  + Improved query fragment and subquery reuse\.
  + Improvements to pre\-allocate executors on Spark start up\.
  + Bloom filter joins are no longer applied when the smaller side of the join includes a broadcast hint\.
+ Tez
  + Resolved an issue with Tez\. Tez UI now works on an EMR cluster with multiple master nodes\.

**Known Issues**
+ The improved whole stage code generation capabilities for Sort Merge Join can increase memory pressure when enabled\. This optimization improves performance, but may result in job retries or failures if the `spark.yarn.executor.memoryOverheadFactor` is not tuned to provide enough memory\. To disable this feature, set `spark.sql.sortMergeJoinExec.extendedCodegen.enabled` to false\.
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

## Release 5\.25\.0<a name="emr-5250-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.25\.0\. Changes are relative to 5\.24\.1\.

Initial release date: July 17, 2019

Last updated date: Oct 30, 2019

**Amazon EMR 5\.25\.0**

**Upgrades**
+ AWS SDK for Java 1\.11\.566
+ Hive 2\.3\.5
+ Presto 0\.220
+ Spark 2\.4\.3
+ TensorFlow 1\.13\.1
+ Tez 0\.9\.2
+ Zookeeper 3\.4\.14

**New Features**
+ \(Oct 30, 2019\) Beginning with Amazon EMR version 5\.25\.0, you can connect to Spark history server UI from the cluster **Summary** page or the **Application history** tab in the console\. Instead of setting up a web proxy through an SSH connection, you can quickly access the Spark history server UI to view application metrics and access relevant log files for active and terminated clusters\. For more information, see [Off\-cluster access to persistent application user interfaces](https://docs.aws.amazon.com/emr/latest/ManagementGuide/app-history-spark-UI.html) in the *Amazon EMR Management Guide*\.

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Improved the performance of some joins by using Bloom filters to pre\-filter inputs\. The optimization is disabled by default and can be enabled by setting the Spark configuration parameter `spark.sql.bloomFilterJoin.enabled` to `true`\.
  + Improved the performance of grouping by string type columns\.
  + Improved the default Spark executor memory and cores configuration of R4 instance types for clusters without HBase installed\.
  + Resolved a previous issue with the dynamic partition pruning feature where the pruned table has to be on the left side of the join\.
  + Improved DISTINCT before INTERSECT optimization to apply to additional cases involving aliases\.
  + Improved SQL plan statistics inference for JOIN followed by DISTINCT queries\. This improvement is disabled by default and can be enabled by setting the Spark configuration parameter `spark.sql.statsImprovements.enabled` to `true`\. This optimization is required by the Distinct before Intersect feature and will be enabled automatically when `spark.sql.optimizer.distinctBeforeIntersect.enabled` is set to `true`\.
  + Optimized join order based on table size and filters\. This optimization is disabled by default and can be enabled by setting the Spark configuration parameter `spark.sql.optimizer.sizeBasedJoinReorder.enabled` to `true`\.

  For more information, see [Optimizing Spark Performance](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-performance.html)\.
+ EMRFS
  + The EMRFS setting, `fs.s3.buckets.create.enabled`, is now disabled by default\. With testing, we found that disabling this setting improves performance and prevents unintentional creation of S3 buckets\. If your application relies on this functionality, you can enable it by setting the property `fs.s3.buckets.create.enabled` to `true` in the `emrfs-site` configuration classification\. For information, see [Supplying a Configuration when Creating a Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-create-cluster.html)\.
+ Local Disk Encryption and S3 Encryption Improvements in Security Configurations \(August 5, 2019\)
  + Separated Amazon S3 encryption settings from local disk encryption settings in security configuration setup\.
  + Added an option to enable EBS encryption with release 5\.24\.0 and later\. Selecting this option encrypts the root device volume in addition to storage volumes\. Previous versions required using a custom AMI to encrypt the root device volume\.
  + For more information, see [Encryption Options](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-data-encryption-options.html) in the *Amazon EMR Management Guide*\.

**Known Issues**
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

## Release 5\.24\.1<a name="emr-5241-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.24\.1\. Changes are relative to 5\.24\.0\.

Initial release date: June 26, 2019

**Changes, Enhancements, and Resolved Issues**
+ Updated the defaultAmazon Linux AMI for EMR to include important Linux kernel security updates, including the TCP SACK Denial of Service Issue \([AWS\-2019\-005](http://aws.amazon.com/security/security-bulletins/AWS-2019-005/)\)\.

**Known Issues**
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

## Release 5\.24\.0<a name="emr-5240-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.24\.0\. Changes are relative to 5\.23\.0\.

Initial release date: June 11, 2019

Last updated date: August 5, 2019

**Upgrades**
+ Flink 1\.8\.0
+ Hue 4\.4\.0
+ JupyterHub 0\.9\.6
+ Livy 0\.6\.0
+ MxNet 1\.4\.0
+ Presto 0\.219
+ Spark 2\.4\.2
+ AWS SDK for Java 1\.11\.546
+ Connectors and drivers:
  + DynamoDB Connector 4\.9\.0
  + MariaDB Connector 2\.4\.1
  + Amazon Redshift JDBC Driver 1\.2\.27\.1051

**Changes, Enhancements, and Resolved Issues**
+ Spark
  + Added optimization to dynamically prune partitions\. The optimization is disabled by default\. To enable it, set the Spark configuration parameter `spark.sql.dynamicPartitionPruning.enabled` to `true`\.
  + Improved performance of `INTERSECT` queries\. This optimization is disabled by default\. To enable it, set the Spark configuration parameter `spark.sql.optimizer.distinctBeforeIntersect.enabled` to `true`\.
  + Added optimization to flatten scalar subqueries with aggregates that use the same relation\. The optimization is disabled by default\. To enable it, set the Spark configuration parameter `spark.sql.optimizer.flattenScalarSubqueriesWithAggregates.enabled` to `true`\.
  + Improved whole stage code generation\.

  For more information, see [Optimizing Spark Performance](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-spark-performance.html)\.
+ Local Disk Encryption and S3 Encryption Improvements in Security Configurations \(August 5, 2019\)
  + Separated Amazon S3 encryption settings from local disk encryption settings in security configuration setup\.
  + Added an option to enable EBS encryption\. Selecting this option encrypts the root device volume in addition to storage volumes\. Previous versions required using a custom AMI to encrypt the root device volume\.
  + For more information, see [Encryption Options](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-data-encryption-options.html) in the *Amazon EMR Management Guide*\.

**Known Issues**
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

## Release 5\.23\.0<a name="emr-5230-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.23\.0\. Changes are relative to 5\.22\.0\.

Initial release date: April 01, 2019

Last updated date: April 30, 2019

**Upgrades**
+ AWS SDK for Java 1\.11\.519

**New Features**
+ \(April 30, 2019\) With Amazon EMR 5\.23\.0 and later, you can launch a cluster with three master nodes to support high availability of applications like YARN Resource Manager, HDFS Name Node, Spark, Hive, and Ganglia\. The master node is no longer a potential single point of failure with this feature\. If one of the master nodes fails, Amazon EMR automatically fails over to a standby master node and replaces the failed master node with a new one with the same configuration and bootstrap actions\. For more information, see [Plan and Configure Master Nodes](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha.html)\.
+ Instance Metadata Service \(IMDS\) V2 support status: Amazon EMR 5\.23\.1, 5\.27\.1 and 5\.32 or later components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. For other 5\.x EMR releases, disabling IMDSv1 causes cluster startup failure\.

**Known Issues**
+ Tez UI \(Fixed in Amazon EMR release version 5\.26\.0\)

  Tez UI does not work on an EMR cluster with multiple master nodes\. 
+ Hue \(Fixed in Amazon EMR release version 5\.24\.0\)
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

## Release 5\.22\.0<a name="emr-5220-whatsnew"></a>

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
+ In Amazon EMR version 5\.19\.0, 5\.20\.0, and 5\.21\.0, YARN node labels are stored in an HDFS directory\. In some situations, this leads to core node startup delays and then causes cluster time\-out and launch failure\. Beginning with Amazon EMR 5\.22\.0, this issue is resolved\. YARN node labels are stored on the local disk of each cluster node, avoiding dependencies on HDFS\. 

**Known Issues**
+ Hue \(Fixed in Amazon EMR release version 5\.24\.0\)
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

## Release 5\.21\.1<a name="emr-5211-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.21\.1\. Changes are relative to 5\.21\.0\.

Initial release date: July 18, 2019

**Changes, Enhancements, and Resolved Issues**
+ Updated the defaultAmazon Linux AMI for EMR to include important Linux kernel security updates, including the TCP SACK Denial of Service Issue \([AWS\-2019\-005](http://aws.amazon.com/security/security-bulletins/AWS-2019-005/)\)\.

**Known Issues**
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

## Release 5\.21\.0<a name="emr-5210-whatsnew"></a>

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
+ Hue \(Fixed in Amazon EMR release version 5\.24\.0\)
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
+ In Amazon EMR version 5\.19\.0, 5\.20\.0, and 5\.21\.0, YARN node labels are stored in an HDFS directory\. In some situations, this leads to core node startup delays and then causes cluster time\-out and launch failure\. Beginning with Amazon EMR 5\.22\.0, this issue is resolved\. YARN node labels are stored on the local disk of each cluster node, avoiding dependencies on HDFS\. 
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

## Release 5\.20\.0<a name="emr-5200-whatsnew"></a>

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
+ Hue \(Fixed in Amazon EMR release version 5\.24\.0\)
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
+ In Amazon EMR version 5\.19\.0, 5\.20\.0, and 5\.21\.0, YARN node labels are stored in an HDFS directory\. In some situations, this leads to core node startup delays and then causes cluster time\-out and launch failure\. Beginning with Amazon EMR 5\.22\.0, this issue is resolved\. YARN node labels are stored on the local disk of each cluster node, avoiding dependencies on HDFS\. 
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

## Release 5\.19\.0<a name="emr-5190-whatsnew"></a>

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
+ **CloudWatch ContainerPending Metric and Automatic Scaling**—\(Fixed in 5\.20\.0\)Amazon EMR may emit a negative value for `ContainerPending`\. If `ContainerPending` is used in an automatic scaling rule, automatic scaling does not behave as expected\. Avoid using `ContainerPending` with automatic scaling\.
+ In Amazon EMR version 5\.19\.0, 5\.20\.0, and 5\.21\.0, YARN node labels are stored in an HDFS directory\. In some situations, this leads to core node startup delays and then causes cluster time\-out and launch failure\. Beginning with Amazon EMR 5\.22\.0, this issue is resolved\. YARN node labels are stored on the local disk of each cluster node, avoiding dependencies on HDFS\. 

## Release 5\.18\.0<a name="emr-5180-whatsnew"></a>

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

## Release 5\.17\.1<a name="emr-5171-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.17\.1\. Changes are relative to 5\.17\.0\.

Initial release date: July 18, 2019

**Changes, Enhancements, and Resolved Issues**
+ Updated the defaultAmazon Linux AMI for EMR to include important Linux kernel security updates, including the TCP SACK Denial of Service Issue \([AWS\-2019\-005](http://aws.amazon.com/security/security-bulletins/AWS-2019-005/)\)\.

## Release 5\.17\.0<a name="emr-5170-whatsnew"></a>

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
+ Resolved the issues with the Cloudwatch metrics and the automatic scaling feature in Amazon EMR version 5\.14\.0, 5\.15\.0, or 5\.16\.0\. 

**Known Issues**
+ When you create a kerberized cluster with Livy installed, Livy fails with an error that simple authentication is not enabled\. Rebooting the Livy server resolves the issue\. As a workaround, add a step during cluster creation that runs `sudo restart livy-server` on the master node\.
+ If you use a customAmazon Linux AMI based on anAmazon Linux AMI with a creation date of 2018\-08\-11, the Oozie server fails to start\. If you use Oozie, create a custom AMI based on anAmazon Linux AMI ID with a different creation date\. You can use the following AWS CLI command to return a list of Image IDs for all HVMAmazon Linux AMIs with a 2018\.03 version, along with the release date, so that you can choose an appropriateAmazon Linux AMI as your base\. Replace MyRegion with your region identifier, such as us\-west\-2\.

  ```
  aws ec2 --region MyRegion describe-images --owner amazon --query 'Images[?Name!=`null`]|[?starts_with(Name, `amzn-ami-hvm-2018.03`) == `true`].[CreationDate,ImageId,Name]' --output text | sort -rk1
  ```

## Release 5\.16\.0<a name="emr-5160-whatsnew"></a>

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
+ After the master node reboots or the instance controller restarts, the CloudWatch metrics will not be collected and the automatic scaling feature will not be available in Amazon EMR version 5\.14\.0, 5\.15\.0, or 5\.16\.0\. This issue is fixed in Amazon EMR version 5\.17\.0\. 

## Release 5\.15\.0<a name="emr-5150-whatsnew"></a>

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
  + Fixed an error in the script that generates self\-signed certificates\. For more information about the issue, see [Release Notes](emr-release-5x.md#emr-5140-relnotes)

**Known Issues**
+ This release version does not support the c1\.medium or m1\.small instance types\. Clusters using either of these instance types fail to start\. As a workaround, specify a different instance type or use a different release version\.
+ After the master node reboots or the instance controller restarts, the CloudWatch metrics will not be collected and the automatic scaling feature will not be available in Amazon EMR version 5\.14\.0, 5\.15\.0, or 5\.16\.0\. This issue is fixed in Amazon EMR version 5\.17\.0\. 

## Release 5\.14\.1<a name="emr-5141-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.14\.1\. Changes are relative to 5\.14\.0\.

Initial release date: October 17, 2018

Updated the default AMI for Amazon EMR to address potential security vulnerabilities\.

## Release 5\.14\.0<a name="emr-5140-whatsnew"></a>

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
+ After the master node reboots or the instance controller restarts, the CloudWatch metrics will not be collected and the automatic scaling feature will not be available in Amazon EMR version 5\.14\.0, 5\.15\.0, or 5\.16\.0\. This issue is fixed in Amazon EMR version 5\.17\.0\. 

## Release 5\.13\.0<a name="emr-5130-whatsnew"></a>

The following release notes include information for the Amazon EMR release version 5\.13\.0\. Changes are relative to 5\.12\.0\.

**Upgrades**
+ Upgraded Spark to 2\.3\.0
+ Upgraded HBase to 1\.4\.2
+ Upgraded Presto to 0\.194
+ Upgraded to 1\.11\.297

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Backported [HIVE\-15436](https://issues.apache.org/jira/browse/HIVE-15436)\. Enhanced Hive APIs to return only views\.

**Known Issues**
+ MXNet does not currently have OpenCV libraries\.

## Release 5\.12\.2<a name="emr-5122-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.12\.2\. Changes are relative to 5\.12\.1\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

## Release 5\.12\.1<a name="emr-5121-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.12\.1\. Changes are relative to 5\.12\.0\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

## Release 5\.12\.0<a name="emr-5120-whatsnew"></a>

The following release notes include information for the Amazon EMR release version 5\.12\.0\. Changes are relative to 5\.11\.1\.

**Upgrades**
+ AWS SDK for Java 1\.11\.238 ⇒ 1\.11\.267\. For more information, see the [AWS SDK for Java Change Log](https://github.com/aws/aws-sdk-java/blob/master/CHANGELOG.md) on GitHub\.
+ Hadoop 2\.7\.3 ⇒ 2\.8\.3\. For more information, see [Apache Hadoop Releases](http://hadoop.apache.org/releases.html)\.
+ Flink 1\.3\.2 ⇒ 1\.4\.0\. For more information, see the [Apache Flink 1\.4\.0 Release Announcement](https://flink.apache.org/news/2017/12/12/release-1.4.0.html)\.
+ HBase 1\.3\.1 ⇒ 1\.4\.0\. For more information, see the [HBase Release Announcement](http://mail-archives.apache.org/mod_mbox/www-announce/201712.mbox/%3CCA+RK=_AU+tB=7SU1HRbeKVEd-sKA5WcJo3oa43vQ6PMB3L9pgQ@mail.gmail.com%3E)\.
+ Hue 4\.0\.1 ⇒ 4\.1\.0\. For more information, see the [Release Notes](http://cloudera.github.io/hue/latest/releases/release-notes-4.1.0/index.html)\.
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

## Release 5\.11\.3<a name="emr-5113-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.11\.3\. Changes are relative to 5\.11\.2\.

Initial release date: July 18, 2019

**Changes, Enhancements, and Resolved Issues**
+ Updated the defaultAmazon Linux AMI for EMR to include important Linux kernel security updates, including the TCP SACK Denial of Service Issue \([AWS\-2019\-005](http://aws.amazon.com/security/security-bulletins/AWS-2019-005/)\)\.

## Release 5\.11\.2<a name="emr-5112-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.11\.2\. Changes are relative to 5\.11\.1\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

## Release 5\.11\.1<a name="emr-5111-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.11\.1 release\. Changes are relative to the Amazon EMR 5\.11\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-5111-enhancements"></a>
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

### Known Issues<a name="emr-5111-known-issues"></a>
+ MXNet does not include OpenCV libraries\.
+ Hive 2\.3\.2 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.11\.0<a name="emr-5110-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.11\.0 release\. Changes are relative to the Amazon EMR 5\.10\.0 release\.

### Upgrades<a name="emr-5110-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.
+ Hive 2\.3\.2
+ Spark 2\.2\.1
+ SDK for Java 1\.11\.238

### New Features<a name="emr-5110-new-features"></a>
+ **Spark**
  + Added `spark.decommissioning.timeout.threshold` setting, which improves Spark decommissioning behavior when using Spot instances\. For more information, see [Configuring Node Decommissioning Behavior](emr-spark-configure.md#spark-decommissioning)\.
  + Added the `aws-sagemaker-spark-sdk` component to Spark, which installs Amazon SageMaker Spark and associated dependencies for Spark integration with [Amazon SageMaker](https://aws.amazon.com/sagemaker/)\. You can use Amazon SageMaker Spark to construct Spark machine learning \(ML\) pipelines using Amazon SageMaker stages\. For more information, see the [SageMaker Spark Readme](https://github.com/aws/sagemaker-spark/blob/master/README.md) on GitHub and [Using Apache Spark with Amazon SageMaker](https://docs.aws.amazon.com/sagemaker/latest/dg/apache-spark.html) in the *Amazon SageMaker Developer Guide*\.

### Known Issues<a name="emr-5110-known-issues"></a>
+ MXNet does not include OpenCV libraries\.
+ Hive 2\.3\.2 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.10\.0<a name="emr-5100-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.10\.0 release\. Changes are relative to the Amazon EMR 5\.9\.0 release\.

### Upgrades<a name="emr-5100-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.
+ AWS SDK for Java 1\.11\.221
+ Hive 2\.3\.1
+ Presto 0\.187

### New Features<a name="emr-5100-new-features"></a>
+ Added support for Kerberos authentication\. For more information, see [Use Kerberos Authentication](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html) in the *Amazon EMR Management Guide*
+ Added support for IAM roles for EMRFS requests to Amazon S3\. For more information, see [Configure IAM Roles for EMRFS Requests to Amazon S3](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-iam-roles.html) in the *Amazon EMR Management Guide*\.
+ Added support for GPU\-based P2 and P3 instance types\. For more information, see [Amazon EC2 P2 Instances](https://aws.amazon.com/ec2/instance-types/p2/) and [Amazon EC2 P3 Instances](https://aws.amazon.com/ec2/instance-types/p3/)\. NVIDIA driver 384\.81 and CUDA driver 9\.0\.176 are installed on these instance types by default\.
+ Added support for [Apache MXNet](emr-mxnet.md)\.

### Changes, Enhancements, and Resolved Issues<a name="emr-5100-enhancements"></a>
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

### Known Issues<a name="emr-5100-known-issues"></a>
+ MXNet does not include OpenCV libraries\.
+ Hive 2\.3\.1 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.9\.0<a name="emr-590-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.9\.0 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Release date: October 5, 2017

Latest feature update: October 12, 2017

### Upgrades<a name="emr-590-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions\.
+ AWS SDK for Java version 1\.11\.183
+ Flink 1\.3\.2
+ Hue 4\.0\.1
+ Pig 0\.17\.0
+ Presto 0\.184

### New Features<a name="emr-590-new-features"></a>
+ Added Livy support \(version 0\.4\.0\-incubating\)\. For more information, see [Apache Livy](emr-livy.md)\.
+ Added support for Hue Notebook for Spark\.
+ Added support for i3\-series Amazon EC2 instances \(October 12, 2017\)\.

### Changes, Enhancements, and Resolved Issues<a name="emr-590-enhancements"></a>
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

### Known Issues<a name="emr-590-known-issues"></a>
+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.
+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.

## Release 5\.8\.2<a name="emr-582-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.8\.2\. Changes are relative to 5\.8\.1\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

## Release 5\.8\.1<a name="emr-581-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.8\.1 release\. Changes are relative to the Amazon EMR 5\.8\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-581-enhancements"></a>
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 5\.8\.0<a name="emr-580-whatsnew"></a>

The following release notes include information for the Amazon EMR version 5\.8\.0 release\. Changes are relative to the Amazon EMR 5\.7\.0 release\.

Initial release date: August 10, 2017

Latest feature update: September 25, 2017

### Upgrades<a name="emr-580-upgrades"></a>

The following applications and components have been upgraded in this release to include the following versions:
+ AWS SDK 1\.11\.160
+ Flink 1\.3\.1
+ Hive 2\.3\.0\. For more information, see [Release Notes](https://issues.apache.org/jira/secure/ConfigureReleaseNote.jspa?projectId=12310843&version=12340269) on the Apache Hive site\.
+ Spark 2\.2\.0\. For more information, see [Release Notes](https://spark.apache.org/releases/spark-release-2-2-0.html) on the Apache Spark site\.

### New Features<a name="emr-580-new-features"></a>
+ Added support for viewing application history \(September 25, 2017\)\. For more information, see [Viewing Application History](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.

### Changes, Enhancements, and Resolved Issues<a name="emr-580-enhancements"></a>
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

### Known Issues<a name="emr-580-known-issues"></a>
+ Cluster launch fails when all applications are installed and the default Amazon EBS root volume size is not changed\. As a workaround, use the `aws emr create-cluster` command from the AWS CLI and specify a larger `--ebs-root-volume-size` parameter\.
+ Hive 2\.3\.0 sets `hive.compute.query.using.stats=true` by default\. This causes queries to get data from existing statistics rather than directly from data, which could be confusing\. For example, if you have a table with `hive.compute.query.using.stats=true` and upload new files to the table `LOCATION`, running a `SELECT COUNT(*)` query on the table returns the count from the statistics, rather than picking up the added rows\.

  As a workaround, use the `ANALYZE TABLE` command to gather new statistics, or set `hive.compute.query.using.stats=false`\. For more information, see [Statistics in Hive](https://cwiki.apache.org/confluence/display/Hive/StatsDev#StatsDev-ExistingTables–ANALYZE) in the Apache Hive documentation\.
+ **Spark**—When using Spark, there is a file handler leak issue with the apppusher daemon, which can appear for a long\-running Spark job after several hours or days\. To fix the issue, connect to the master node and type `sudo /etc/init.d/apppusher stop`\. This stops that apppusher daemon, which Amazon EMR will restart automatically\.
+ **Application history**
  + Historical data for dead Spark executors is not available\.
  + Application history is not available for clusters that use a security configuration to enable in\-flight encryption\.

## Release 5\.7\.0<a name="w138aac12c15c93"></a>

The following release notes include information for the Amazon EMR 5\.7\.0 release\. Changes are relative to the Amazon EMR 5\.6\.0 release\.

Release date: July 13, 2017

### Upgrades<a name="w138aac12c15c93b6"></a>
+ Flink 1\.3\.0
+ Phoenix 4\.11\.0
+ Zeppelin 0\.7\.2

### New Features<a name="w138aac12c15c93b8"></a>
+ Added the ability to specify a custom Amazon Linux AMI when you create a cluster\. For more information, see [Using a Custom AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html)\.

### Changes, Enhancements, and Resolved Issues<a name="w138aac12c15c93c10"></a>
+ **HBase**
  + Added capability to configure HBase read\-replica clusters\. See [Using a Read\-Replica Cluster\.](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html#emr-hbase-s3-read-replica)
  + Multiple bug fixes and enhancements
+ **Presto**—added ability to configure `node.properties`\.
+ **YARN**—added ability to configure `container-log4j.properties`
+ **Sqoop**—backported [SQOOP\-2880](https://issues.apache.org/jira/browse/SQOOP-2880), which introduces an argument that allows you to set the Sqoop temporary directory\.

## Release 5\.6\.0<a name="w138aac12c15c95"></a>

The following release notes include information for the Amazon EMR 5\.6\.0 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Release date: June 5, 2017

### Upgrades<a name="w138aac12c15c95b6"></a>
+ Flink 1\.2\.1
+ HBase 1\.3\.1
+ Mahout 0\.13\.0\. This is the first version of Mahout to support Spark 2\.x in Amazon EMR version 5\.0 and later\.
+ Spark 2\.1\.1

### Changes, Enhancements, and Resolved Issues<a name="w138aac12c15c95b8"></a>
+ **Presto**
  + Added the ability to enable SSL/TLS secured communication between Presto nodes by enabling in\-transit encryption using a security configuration\. For more information, see [In\-transit Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption-options.html#emr-encryption-intransit)\.
  + Backported [Presto 7661](https://github.com/prestodb/presto/pull/7661/commits), which adds the `VERBOSE` option to the `EXPLAIN ANALYZE` statement to report more detailed, low level statistics about a query plan\.

## Release 5\.5\.3<a name="emr-553-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.5\.3\. Changes are relative to 5\.5\.2\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ This release addresses a potential security vulnerability\.

## Release 5\.5\.2<a name="emr-552-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.5\.2\. Changes are relative to 5\.5\.1\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

## Release 5\.5\.1<a name="emr-551-whatsnew"></a>

The following release notes include information for the Amazon EMR 5\.5\.1 release\. Changes are relative to the Amazon EMR 5\.5\.0 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-551-enhancements"></a>
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 5\.5\.0<a name="w138aac12c15d103"></a>

The following release notes include information for the Amazon EMR 5\.5\.0 release\. Changes are relative to the Amazon EMR 5\.4\.0 release\.

Release date: April 26, 2017

### Upgrades<a name="w138aac12c15d103b6"></a>
+ Hue 3\.12
+ Presto 0\.170
+ Zeppelin 0\.7\.1
+ ZooKeeper 3\.4\.10

### Changes, Enhancements, and Resolved Issues<a name="w138aac12c15d103b8"></a>
+ **Spark**
  + Backported Spark Patch [\(SPARK\-20115\) Fix DAGScheduler to recompute all the lost shuffle blocks when external shuffle service is unavailable](https://issues.apache.org/jira/browse/SPARK-20115) to version 2\.1\.0 of Spark, which is included in this release\.
+ **Flink**
  + Flink is now built with Scala 2\.11\. If you use the Scala API and libraries, we recommend that you use Scala 2\.11 in your projects\.
  + Addressed an issue where `HADOOP_CONF_DIR` and `YARN_CONF_DIR` defaults were not properly set, so `start-scala-shell.sh` failed to work\. Also added the ability to set these values using `env.hadoop.conf.dir` and `env.yarn.conf.dir` in `/etc/flink/conf/flink-conf.yaml` or the `flink-conf` configuration classification\.
  + Introduced a new EMR\-specific command, `flink-scala-shell` as a wrapper for `start-scala-shell.sh`\. We recommend using this command instead of `start-scala-shell`\. The new command simplifies execution\. For example, `flink-scala-shell -n 2` starts a Flink Scala shell with a task parallelism of 2\.
  + Introduced a new EMR\-specific command, `flink-yarn-session` as a wrapper for `yarn-session.sh`\. We recommend using this command instead of `yarn-session`\. The new command simplifies execution\. For example, `flink-yarn-session -d -n 2` starts a long\-running Flink session in a detached state with two task managers\. 
  + Addressed [\(FLINK\-6125\) Commons httpclient is not shaded anymore in Flink 1\.2](https://issues.apache.org/jira/browse/FLINK-6125)\.
+ **Presto**
  + Added support for LDAP authentication\. Using LDAP with Presto on Amazon EMR requires that you enable HTTPS access for the Presto coordinator \(`http-server.https.enabled=true` in `config.properties`\)\. For configuration details, see [LDAP Authentication](https://prestodb.io/docs/current/security/ldap.html) in Presto documentation\.
  + Added support for `SHOW GRANTS`\.
+ **Amazon EMR Base Linux AMI**
  + Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [Amazon Linux AMI 2017\.03 Release Notes](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.
  + Removed Python 2\.6 from the Amazon EMR base Linux image\. Python 2\.7 and 3\.4 are installed by default\. You can install Python 2\.6 manually if necessary\.

## Release 5\.4\.0<a name="w138aac12c15d105"></a>

The following release notes include information for the Amazon EMR 5\.4\.0 release\. Changes are relative to the Amazon EMR 5\.3\.0 release\.

Release date: March 08, 2017

### Upgrades<a name="w138aac12c15d105b6"></a>

The following upgrades are available in this release:
+ Upgraded to Flink 1\.2\.0
+ Upgraded to Hbase 1\.3\.0
+ Upgraded to Phoenix 4\.9\.0
**Note**  
If you upgrade from an earlier version of Amazon EMR to Amazon EMR version 5\.4\.0 or later and use secondary indexing, upgrade local indexes as described in the [Apache Phoenix documentation](https://phoenix.apache.org/secondary_indexing.html#Upgrading_Local_Indexes_created_before_4.8.0)\. Amazon EMR removes the required configurations from the `hbase-site` classification, but indexes need to be repopulated\. Online and offline upgrade of indexes are supported\. Online upgrades are the default, which means indexes are repopulated while initializing from Phoenix clients of version 4\.8\.0 or greater\. To specify offline upgrades, set the `phoenix.client.localIndexUpgrade` configuration to false in the `phoenix-site` classification, and then SSH to the master node to run `psql [zookeeper] -1`\.
+ Upgraded to Presto 0\.166
+ Upgraded to Zeppelin 0\.7\.0

### Changes and Enhancements<a name="w138aac12c15d105b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.4\.0:
+ Added support for r4 instances\. See [Amazon EC2 Instance Types](https://aws.amazon.com/ec2/instance-types/)\.

## Release 5\.3\.1<a name="emr-531-whatsnew"></a>

The following release notes include information for the Amazon EMR 5\.3\.1 release\. Changes are relative to the Amazon EMR 5\.3\.0 release\.

Release date: February 7, 2017

Minor changes to backport Zeppelin patches and update the default AMI for Amazon EMR\.

## Release 5\.3\.0<a name="w138aac12c15d109"></a>

The following release notes include information for the Amazon EMR 5\.3\.0 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: January 26, 2017

### Upgrades<a name="w138aac12c15d109b6"></a>

The following upgrades are available in this release:
+ Upgraded to Hive 2\.1\.1
+ Upgraded to Hue 3\.11\.0
+ Upgraded to Spark 2\.1\.0
+ Upgraded to Oozie 4\.3\.0
+ Upgraded to Flink 1\.1\.4

### Changes and Enhancements<a name="w138aac12c15d109b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.3\.0:
+ Added a patch to Hue that allows you to use the `interpreters_shown_on_wheel` setting to configure what interpreters to show first on the Notebook selection wheel, regardless of their ordering in the `hue.ini` file\.
+ Added the `hive-parquet-logging` configuration classification, which you can use to configure values in Hive's `parquet-logging.properties` file\.

## Release 5\.2\.2<a name="w138aac12c15d111"></a>

The following release notes include information for the Amazon EMR 5\.2\.2 release\. Changes are relative to the Amazon EMR 5\.2\.1 release\.

Release date: May 2, 2017

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d111b6"></a>
+ Backported [SPARK\-194459](https://issues.apache.org/jira/browse/SPARK-19459), which addresses an issue where reading from an ORC table with char/varchar columns can fail\.

## Release 5\.2\.1<a name="w138aac12c15d113"></a>

The following release notes include information for the Amazon EMR 5\.2\.1 release\. Changes are relative to the Amazon EMR 5\.2\.0 release\.

Release date: December 29, 2016

### Upgrades<a name="w138aac12c15d113b6"></a>

The following upgrades are available in this release:
+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\. 
+ Upgraded to Zookeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

### Changes and Enhancements<a name="w138aac12c15d113b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.2\.1:
+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.
+ The location of Flink and YARN configuration paths are now set by default in `/etc/default/flink` that you don't need to set the environment variables `FLINK_CONF_DIR` and `HADOOP_CONF_DIR` when running the `flink` or `yarn-session.sh` driver scripts to launch Flink jobs\.
+ Added support for FlinkKinesisConsumer class\.

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d113c10"></a>
+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.
+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

## Release 5\.2\.0<a name="w138aac12c15d115"></a>

The following release notes include information for the Amazon EMR 5\.2\.0 release\. Changes are relative to the Amazon EMR 5\.1\.0 release\.

Release date: November 21, 2016

### Changes and enhancements<a name="w138aac12c15d115b6"></a>

The following changes and enhancements are available in this release:
+ Added Amazon S3 storage mode for HBase\.
+  Enables you to specify an Amazon S3 location for the HBase rootdir\. For more information, see [HBase on Amazon S3](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hbase-s3.html)\.

### Upgrades<a name="w138aac12c15d115b8"></a>

The following upgrades are available in this release:
+ Upgraded to Spark 2\.0\.2

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d115c10"></a>
+ Fixed an issue with /mnt being constrained to 2 TB on EBS\-only instance types\.
+ Fixed an issue with instance\-controller and logpusher logs being output to their corresponding \.out files instead of to their normal log4j\-configured \.log files, which rotate hourly\. The \.out files don't rotate, so this would eventually fill up the /emr partition\. This issue only affects hardware virtual machine \(HVM\) instance types\.

## Release 5\.1\.0<a name="w138aac12c15d117"></a>

The following release notes include information for the Amazon EMR 5\.1\.0 release\. Changes are relative to the Amazon EMR 5\.0\.0 release\.

Release date: November 03, 2016

### Changes and enhancements<a name="w138aac12c15d117b6"></a>

The following changes and enhancements are available in this release:
+ Added support for Flink 1\.1\.3\.
+ Presto has been added as an option in the notebook section of Hue\.

### Upgrades<a name="w138aac12c15d117b8"></a>

The following upgrades are available in this release:
+ Upgraded to HBase 1\.2\.3
+ Upgraded to Zeppelin 0\.6\.2

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d117c10"></a>
+ Fixed an issue with Tez queries on Amazon S3 with ORC files did not perform as well as earlier Amazon EMR 4\.x versions\.

## Release 5\.0\.3<a name="w138aac12c15d119"></a>

The following release notes include information for the Amazon EMR 5\.0\.3 release\. Changes are relative to the Amazon EMR 5\.0\.0 release\.

Release date: October 24, 2016

### Upgrades<a name="w138aac12c15d119b6"></a>

The following upgrades are available in this release:
+ Upgraded to Hadoop 2\.7\.3
+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.
+ Upgraded to Spark 2\.0\.1
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

## Release 5\.0\.0<a name="w138aac12c15d121"></a>

 Release date: July 27, 2016

### Upgrades<a name="w138aac12c15d121b4"></a>

The following upgrades are available in this release:
+ Upgraded to Hive 2\.1
+ Upgraded to Presto 0\.150
+ Upgraded to Spark 2\.0
+ Upgraded to Hue 3\.10\.0
+ Upgraded to Pig 0\.16\.0
+ Upgraded to Tez 0\.8\.4
+ Upgraded to Zeppelin 0\.6\.1

### Changes and Enhancements<a name="w138aac12c15d121b6"></a>

The following are changes made to Amazon EMR releases for release label emr\-5\.0\.0 or greater:
+ Amazon EMR supports the latest open\-source versions of Hive \(version 2\.1\) and Pig \(version 0\.16\.0\)\. If you have used Hive or Pig on Amazon EMR in the past, this may affect some use cases\. For more information, see [Hive](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-hive.html) and [Pig](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-pig.html)\.
+ The default execution engine for Hive and Pig is now Tez\. To change this, you would edit the appropriate values in the `hive-site` and `pig-properties` configuration classifications, respectively\.
+ An enhanced step debugging feature was added, which allows you to see the root cause of step failures if the service can determine the cause\. For more information, see [ Enhanced Step Debugging](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-enhanced-step-debugging.html) in the Amazon EMR Management Guide\.
+ Applications that previously ended with "\-Sandbox" no longer have that suffix\. This may break your automation, for example, if you are using scripts to launch clusters with these applications\. The following table shows application names in Amazon EMR 4\.7\.2 versus Amazon EMR 5\.0\.0\.   
**Application name changes**    
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-whatsnew-history.html)
+ Spark is now compiled for Scala 2\.11\.
+ Java 8 is now the default JVM\. All applications run using the Java 8 runtime\. There are no changes to any application’s byte code target\. Most applications continue to target Java 7\.
+ Zeppelin now includes authentication features\. For more information, see [Zeppelin](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-zeppelin.html)\.
+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

## Release 4\.9\.5<a name="emr-495-whatsnew"></a>

The following release notes include information for Amazon EMR release version 4\.9\.5\. Changes are relative to 4\.9\.4\.

Initial release date: August 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ HBase
  + This release addresses a potential security vulnerability\.

## Release 4\.9\.4<a name="emr-494-whatsnew"></a>

The following release notes include information for Amazon EMR release version 4\.9\.4\. Changes are relative to 4\.9\.3\.

Initial release date: March 29, 2018

**Changes, Enhancements, and Resolved Issues**
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address potential vulnerabilities\.

## Release 4\.9\.3<a name="emr-493-whatsnew"></a>

The following release notes include information for the Amazon EMR 4\.9\.3 release\. Changes are relative to the Amazon EMR 4\.9\.2 release\.

Initial release date: January 22, 2018

### Changes, Enhancements, and Resolved Issues<a name="emr-493-enhancements"></a>
+ Updated the Amazon Linux kernel of the defaultAmazon Linux AMI for Amazon EMR to address vulnerabilities associated with speculative execution \(CVE\-2017\-5715, CVE\-2017\-5753, and CVE\-2017\-5754\)\. For more information, see [https://aws.amazon.com/security/security-bulletins/AWS-2018-013/](https://aws.amazon.com/security/security-bulletins/AWS-2018-013/)\.

## Release 4\.9\.2<a name="w138aac12c15d129"></a>

The following release notes include information for the Amazon EMR 4\.9\.2 release\. Changes are relative to the Amazon EMR 4\.9\.1 release\.

Release date: July 13, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

## Release 4\.9\.1<a name="w138aac12c15d131"></a>

The following release notes include information for the Amazon EMR 4\.9\.1 release\. Changes are relative to the Amazon EMR 4\.8\.4 release\.

Release date: April 10, 2017

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d131b6"></a>
+ Backports of [HIVE\-9976](https://issues.apache.org/jira/browse/HIVE-9976) and [HIVE\-10106](https://issues.apache.org/jira/browse/HIVE-10106)
+ Fixed an issue in YARN where a large number of nodes \(greater than 2,000\) and containers \(greater than 5,000\) would cause an out of memory error, for example: `"Exception in thread 'main' java.lang.OutOfMemoryError"`\.

### Changes and Enhancements<a name="w138aac12c15d131b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.9\.1:
+ Amazon EMR releases are now based on Amazon Linux 2017\.03\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2017.03-release-notes/)\.
+ Removed Python 2\.6 from the Amazon EMR base Linux image\. You can install Python 2\.6 manually if necessary\.

## Release 4\.8\.4<a name="w138aac12c15d133"></a>

The following release notes include information for the Amazon EMR 4\.8\.4 release\. Changes are relative to the Amazon EMR 4\.8\.3 release\.

Release date: Feb 7, 2017

Minor changes, bug fixes, and enhancements were made in this release\.

## Release 4\.8\.3<a name="w138aac12c15d135"></a>

The following release notes include information for the Amazon EMR 4\.8\.3 release\. Changes are relative to the Amazon EMR 4\.8\.2 release\.

Release date: December 29, 2016

### Upgrades<a name="w138aac12c15d135b6"></a>

The following upgrades are available in this release:
+ Upgraded to Presto 0\.157\.1\. For more information, see [Presto Release Notes](https://prestodb.io/docs/current/release/release-0.157.1.html) in the Presto documentation\.
+ Upgraded to Spark 1\.6\.3\. For more information, see [Spark Release Notes](http://spark.apache.org/releases/spark-release-1-6-3.html) in the Apache Spark documentation\.
+ Upgraded to ZooKeeper 3\.4\.9\. For more information, see [ZooKeeper Release Notes](https://zookeeper.apache.org/doc/r3.4.9/releasenotes.html) in the Apache ZooKeeper documentation\.

### Changes and Enhancements<a name="w138aac12c15d135b8"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.8\.3:
+ Added support for the Amazon EC2 m4\.16xlarge instance type in Amazon EMR version 4\.8\.3 and later, excluding 5\.0\.0, 5\.0\.3, and 5\.2\.0\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d135c10"></a>
+ Fixed an issue in Hadoop where the ReplicationMonitor thread could get stuck for a long time because of a race between replication and deletion of the same file in a large cluster\.
+ Fixed an issue where ControlledJob\#toString failed with a null pointer exception \(NPE\) when job status was not successfully updated\.

## Release 4\.8\.2<a name="w138aac12c15d137"></a>

The following release notes include information for the Amazon EMR 4\.8\.2 release\. Changes are relative to the Amazon EMR 4\.8\.0 release\.

Release date: October 24, 2016

### Upgrades<a name="w138aac12c15d137b6"></a>

The following upgrades are available in this release:
+ Upgraded to Hadoop 2\.7\.3
+ Upgraded to Presto 0\.152\.3, which includes support for the Presto web interface\. You can access the Presto web interface on the Presto coordinator using port 8889\. For more information about the Presto web interface, see [Web Interface](https://prestodb.io/docs/current/admin/web-interface.html) in the Presto documentation\.
+ Amazon EMR releases are now based on Amazon Linux 2016\.09\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.09-release-notes/)\.

## Release 4\.8\.0<a name="w138aac12c15d139"></a>

Release date: September 7, 2016

### Upgrades<a name="w138aac12c15d139b4"></a>

The following upgrades are available in this release:
+ Upgraded to HBase 1\.2\.2
+ Upgraded to Presto\-Sandbox 0\.151
+ Upgraded to Tez 0\.8\.4
+ Upgraded to Zeppelin\-Sandbox 0\.6\.1

### Changes and Enhancements<a name="w138aac12c15d139b6"></a>

The following are changes made to Amazon EMR releases for release label emr\-4\.8\.0:
+ Fixed an issue in YARN where the ApplicationMaster would attempt to clean up containers that no longer exist because their instances have been terminated\.
+ Corrected the hive\-server2 URL for Hive2 actions in the Oozie examples\.
+ Added support for additional Presto catalogs\.
+ Backported patches: [HIVE\-8948](https://issues.apache.org/jira/browse/HIVE-8948), [HIVE\-12679](https://issues.apache.org/jira/browse/HIVE-12679), [HIVE\-13405](https://issues.apache.org/jira/browse/HIVE-13405), [PHOENIX\-3116](https://issues.apache.org/jira/browse/PHOENIX-3116), [HADOOP\-12689](https://issues.apache.org/jira/browse/HADOOP-12689)
+ Added support for security configurations, which allow you to create and apply encryption options more easily\. For more information, see [Data Encryption](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-data-encryption.html)\.

## Release 4\.7\.2<a name="w138aac12c15d141"></a>

The following release notes include information for Amazon EMR 4\.7\.2\.

Release date: July 15, 2016

### Features<a name="w138aac12c15d141b6"></a>

The following features are available in this release:
+ Upgraded to Mahout 0\.12\.2
+ Upgraded to Presto 0\.148
+ Upgraded to Spark 1\.6\.2
+ You can now create an AWSCredentialsProvider for use with EMRFS using a URI as a parameter\. For more information, see [Create an AWSCredentialsProvider for EMRFS](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-plan-credentialsprovider.html)\.
+ EMRFS now allows users to configure a custom DynamoDB endpoint for their Consistent View metadata using the `fs.s3.consistent.dynamodb.endpoint` property in `emrfs-site.xml`\.
+ Added a script in `/usr/bin` called `spark-example`, which wraps `/usr/lib/spark/spark/bin/run-example` so you can run examples directly\. For instance, to run the SparkPi example that comes with the Spark distribution, you can run `spark-example SparkPi 100` from the command line or using `command-runner.jar` as a step in the API\.

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d141b8"></a>
+ Fixed an issue where Oozie had the `spark-assembly.jar` was not in the correct location when Spark was also installed, which resulted in failure to launch Spark applications with Oozie\.
+ Fixed an issue with Spark Log4j\-based logging in YARN containers\.

## Release 4\.7\.1<a name="w138aac12c15d143"></a>

Release date: June 10, 2016

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d143b4"></a>
+ Fixed an issue that extended the startup time of clusters launched in a VPC with private subnets\. The bug only impacted clusters launched with the Amazon EMR 4\.7\.0 release\. 
+ Fixed an issue that improperly handled listing of files in Amazon EMR for clusters launched with the Amazon EMR 4\.7\.0 release\.

## Release 4\.7\.0<a name="w138aac12c15d145"></a>

**Important**  
Amazon EMR 4\.7\.0 is deprecated\. Use Amazon EMR 4\.7\.1 or later instead\.

Release date: June 2, 2016

### Features<a name="w138aac12c15d145b6"></a>

The following features are available in this release:
+ Added Apache Phoenix 4\.7\.0
+ Added Apache Tez 0\.8\.3
+ Upgraded to HBase 1\.2\.1
+ Upgraded to Mahout 0\.12\.0
+ Upgraded to Presto 0\.147
+ Upgraded the AWS SDK for Java to 1\.10\.75
+ The final flag was removed from the `mapreduce.cluster.local.dir` property in `mapred-site.xml` to allow users to run Pig in local mode\.

### Amazon Redshift JDBC Drivers Available on Cluster<a name="w138aac12c15d145b8"></a>

Amazon Redshift JDBC drivers are now included at `/usr/share/aws/redshift/jdbc`\. `/usr/share/aws/redshift/jdbc/RedshiftJDBC41.jar` is the JDBC 4\.1\-compatible Amazon Redshift driver and `/usr/share/aws/redshift/jdbc/RedshiftJDBC4.jar` is the JDBC 4\.0\-compatible Amazon Redshift driver\. For more information, see [Configure a JDBC Connection](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html) in the *Amazon Redshift Cluster Management Guide*\.

### Java 8<a name="w138aac12c15d145c10"></a>

Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d145c12"></a>
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

## Release 4\.6\.0<a name="w138aac12c15d147"></a>

Release date: April 21, 2016

### Features<a name="w138aac12c15d147b4"></a>

The following features are available in this release:
+ Added HBase 1\.2\.0
+ Added Zookeeper\-Sandbox 3\.4\.8 
+ Upgraded to Presto\-Sandbox 0\.143
+ Amazon EMR releases are now based on Amazon Linux 2016\.03\.0\. For more information, see [https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/](https://aws.amazon.com/amazon-linux-ami/2016.03-release-notes/)\.

### Issue Affecting Throughput Optimized HDD \(st1\) EBS Volume Types<a name="w138aac12c15d147b6"></a>

An issue in the Linux kernel versions 4\.2 and above significantly affects performance on Throughput Optimized HDD \(st1\) EBS volumes for EMR\. This release \(emr\-4\.6\.0\) uses kernel version 4\.4\.5 and hence is impacted\. Therefore, we recommend not using emr\-4\.6\.0 if you want to use st1 EBS volumes\. You can use emr\-4\.5\.0 or prior Amazon EMR releases with st1 without impact\. In addition, we provide the fix with future releases\.

### Python Defaults<a name="w138aac12c15d147b8"></a>

Python 3\.4 is now installed by default, but Python 2\.7 remains the system default\. You may configure Python 3\.4 as the system default using either a bootstrap action; you can use the configuration API to set PYSPARK\_PYTHON export to `/usr/bin/python3.4` in the `spark-env` classification to affect the Python version used by PySpark\.

### Java 8<a name="w138aac12c15d147c10"></a>

Except for Presto, OpenJDK 1\.7 is the default JDK used for all applications\. However, both OpenJDK 1\.7 and 1\.8 are installed\. For information about how to set `JAVA_HOME` for applications, see [Configuring Applications to Use Java 8](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html#configuring-java8)\.

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d147c12"></a>
+ Fixed an issue where application provisioning would sometimes randomly fail due to a generated password\.
+ Previously, `mysqld` was installed on all nodes\. Now, it is only installed on the master instance and only if the chosen application includes `mysql-server` as a component\. Currently, the following applications include the `mysql-server` component: HCatalog, Hive, Hue, Presto\-Sandbox, and Sqoop\-Sandbox\.
+ Changed `yarn.scheduler.maximum-allocation-vcores` to 80 from the default of 32, which fixes an issue introduced in emr\-4\.4\.0 that mainly occurs with Spark while using the `maximizeResourceAllocation` option in a cluster whose core instance type is one of a few large instance types that have the YARN vcores set higher than 32; namely c4\.8xlarge, cc2\.8xlarge, hs1\.8xlarge, i2\.8xlarge, m2\.4xlarge, r3\.8xlarge, d2\.8xlarge, or m4\.10xlarge were affected by this issue\.
+ s3\-dist\-cp now uses EMRFS for all Amazon S3 nominations and no longer stages to a temporary HDFS directory\.
+ Fixed an issue with exception handling for client\-side encryption multipart uploads\.
+ Added an option to allow users to change the Amazon S3 storage class\. By default this setting is `STANDARD`\. The `emrfs-site` configuration classification setting is `fs.s3.storageClass` and the possible values are `STANDARD`, `STANDARD_IA`, and `REDUCED_REDUNDANCY`\. For more information about storage classes, see [Storage Classes](https://docs.aws.amazon.com/AmazonS3/latest/dev/storage-class-intro.html) in the Amazon Simple Storage Service Developer Guide\. 

## Release 4\.5\.0<a name="w138aac12c15d149"></a>

Release date: April 4, 2016

### Features<a name="w138aac12c15d149b4"></a>

The following features are available in this release:
+ Upgraded to Spark 1\.6\.1
+ Upgraded to Hadoop 2\.7\.2
+ Upgraded to Presto 0\.140
+ Added AWS KMS support for Amazon S3 server\-side encryption\.

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d149b6"></a>
+ Fixed an issue where MySQL and Apache servers would not start after a node was rebooted\. 
+ Fixed an issue where IMPORT did not work correctly with non\-partitioned tables stored in Amazon S3
+ Fixed an issue with Presto where it requires the staging directory to be `/mnt/tmp` rather than `/tmp` when writing to Hive tables\.

## Release 4\.4\.0<a name="w138aac12c15d151"></a>

Release date: March 14, 2016

### Features<a name="w138aac12c15d151b4"></a>

The following features are available in this release:
+ Added HCatalog 1\.0\.0
+ Added Sqoop\-Sandbox 1\.4\.6
+ Upgraded to Presto 0\.136
+ Upgraded to Zeppelin 0\.5\.6
+ Upgraded to Mahout 0\.11\.1
+ Enabled `dynamicResourceAllocation` by default\.
+ Added a table of all configuration classifications for the release\. For more information, see the Configuration Classifications table in [Configuring Applications](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.

### Known Issues Resolved from Previous Releases<a name="w138aac12c15d151b6"></a>
+ Fixed an issue where the `maximizeResourceAllocation` setting would not reserve enough memory for YARN ApplicationMaster daemons\.
+ Fixed an issue encountered with a custom DNS\. If any entries in `resolve.conf` precede the custom entries provided, then the custom entries are not resolvable\. This behavior was affected by clusters in a VPC where the default VPC name server is inserted as the top entry in `resolve.conf`\.
+ Fixed an issue where the default Python moved to version 2\.7 and boto was not installed for that version\.
+ Fixed an issue where YARN containers and Spark applications would generate a unique Ganglia round robin database \(rrd\) file, which resulted in the first disk attached to the instance filling up\. Because of this fix, YARN container level metrics have been disabled and Spark application level metrics have been disabled\.
+ Fixed an issue in log pusher where it would delete all empty log folders\. The effect was that the Hive CLI was not able to log because log pusher was removing the empty `user` folder under `/var/log/hive`\.
+ Fixed an issue affecting Hive imports, which affected partitioning and resulted in an error during import\.
+ Fixed an issue where EMRFS and s3\-dist\-cp did not properly handle bucket names that contain periods\.
+ Changed a behavior in EMRFS so that in versioning\-enabled buckets the `_$folder$` marker file is not continuously created, which may contribute to improved performance for versioning\-enabled buckets\.
+ Changed the behavior in EMRFS such that it does not use instruction files except for cases where client\-side encryption is enabled\. If you want to delete instruction files while using client\-side encryption, you can set the emrfs\-site\.xml property, `fs.s3.cse.cryptoStorageMode.deleteInstructionFiles.enabled`, to true\. 
+ Changed YARN log aggregation to retain logs at the aggregation destination for two days\. The default destination is your cluster's HDFS storage\. If you want to change this duration, change the value of `yarn.log-aggregation.retain-seconds` using the `yarn-site` configuration classification when you create your cluster\. As always, you can save your application logs to Amazon S3 using the `log-uri` parameter when you create your cluster\.

### Patches Applied<a name="w138aac12c15d151b8"></a>

The following patches from open source projects were included in this release:
+ [HIVE\-9655](https://issues.apache.org/jira/browse/HIVE-9655)
+ [HIVE\-9183](https://issues.apache.org/jira/browse/HIVE-9183)
+ [HADOOP\-12810](https://issues.apache.org/jira/browse/HADOOP-12810)

## Release 4\.3\.0<a name="w138aac12c15d153"></a>

Release date: January 19, 2016

### Features<a name="w138aac12c15d153b4"></a>

The following features are available in this release:
+ Upgraded to Hadoop 2\.7\.1
+ Upgraded to Spark 1\.6\.0
+ Upgraded Ganglia to 3\.7\.2 
+ Upgraded Presto to 0\.130

Amazon EMR made some changes to `spark.dynamicAllocation.enabled` when it is set to true; it is false by default\. When set to true, this affects the defaults set by the `maximizeResourceAllocation` setting:
+ If `spark.dynamicAllocation.enabled` is set to true, `spark.executor.instances` is not set by `maximizeResourceAllocation`\.
+ The `spark.driver.memory` setting is now configured based on the instance types in the cluster in a similar way to how `spark.executors.memory` is set\. However, because the Spark driver application may run on either the master or one of the core instances \(for example, in YARN client and cluster modes, respectively\), the `spark.driver.memory` setting is set based on the instance type of the smaller instance type between these two instance groups\.
+ The `spark.default.parallelism` setting is now set at twice the number of CPU cores available for YARN containers\. In previous releases, this was half that value\.
+ The calculations for the memory overhead reserved for Spark YARN processes was adjusted to be more accurate, resulting in a small increase in the total amount of memory available to Spark \(that is, `spark.executor.memory`\)\.

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d153b6"></a>
+ YARN log aggregation is now enabled by default\.
+ Fixed an issue where logs would not be pushed to a cluster's Amazon S3 logs bucket when YARN log aggregation was enabled\.
+ YARN container sizes now have a new minimum of 32 across all node types\.
+ Fixed an issue with Ganglia that caused excessive disk I/O on the master node in large clusters\.
+ Fixed an issue that prevented applications logs from being pushed to Amazon S3 when a cluster is shutting down\.
+ Fixed an issue in EMRFS CLI that caused certain commands to fail\.
+ Fixed an issue with Zeppelin that prevented dependencies from being loaded in the underlying SparkContext\.
+ Fixed an issue that resulted from issuing a resize attempting to add instances\. 
+ Fixed an issue in Hive where CREATE TABLE AS SELECT makes excessive list calls to Amazon S3\. 
+ Fixed an issue where large clusters would not provision properly when Hue, Oozie, and Ganglia are installed\.
+ Fixed an issue in s3\-dist\-cp where it would return a zero exit code even if it failed with an error\.

### Patches Applied<a name="w138aac12c15d153b8"></a>

The following patches from open source projects were included in this release:
+ [OOZIE\-2402](https://issues.apache.org/jira/browse/OOZIE-2402)
+ [HIVE\-12502](https://issues.apache.org/jira/browse/HIVE-12502)
+ [HIVE\-10631](https://issues.apache.org/jira/browse/HIVE-10631)
+ [HIVE\-12213](https://issues.apache.org/jira/browse/HIVE-12213)
+ [HIVE\-10559](https://issues.apache.org/jira/browse/HIVE-10559)
+ [HIVE\-12715](https://issues.apache.org/jira/browse/HIVE-12715)
+ [HIVE\-10685](https://issues.apache.org/jira/browse/HIVE-10685)

## Release 4\.2\.0<a name="w138aac12c15d155"></a>

Release date: November 18, 2015

### Features<a name="w138aac12c15d155b4"></a>

The following features are available in this release:
+ Added Ganglia support
+ Upgraded to Spark 1\.5\.2
+ Upgraded to Presto 0\.125
+ Upgraded Oozie to 4\.2\.0
+ Upgraded Zeppelin to 0\.5\.5
+ Upgraded the AWS SDK for Java to 1\.10\.27

### Known Issues Resolved from the Previous Releases<a name="w138aac12c15d155b6"></a>
+ Fixed an issue with the EMRFS CLI where it did not use the default metadata table name\.
+ Fixed an issue encountered when using ORC\-backed tables in Amazon S3\.
+ Fixed an issue encountered with a Python version mismatch in the Spark configuration\.
+ Fixed an issue when a YARN node status fails to report because of DNS issues for clusters in a VPC\.
+ Fixed an issue encountered when YARN decommissioned nodes, resulting in hanged applications or the inability to schedule new applications\.
+ Fixed an issue encountered when clusters terminated with status TIMED\_OUT\_STARTING\.
+ Fixed an issue encountered when including the EMRFS Scala dependency in other builds\. The Scala dependency has been removed\.