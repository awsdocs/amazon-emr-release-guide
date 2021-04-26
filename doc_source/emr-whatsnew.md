# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR 6\.x series and 5\.x series\. These release notes are also available on the [Release 6\.2\.0 Tab](emr-release-6x.md#emr-620-release) and [Release 5\.33\.0 Tab](emr-release-5x.md#emr-5330-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

**Note**  
Twenty\-five previous Amazon EMR release versions now use AWS Signature Version 4 to authenticate requests to Amazon S3\. The use of AWS Signature version 2 is being phased out and new S3 buckets created after June 24, 2020 will not support Signature Version 2 signed requests\. Existing buckets will continue to support Signature Version 2\. We recommend migrating to an Amazon EMR release that supports Signature Version 4 so you can continue accessing new S3 buckets and avoid any potential interruption to your workloads\.  
The following EMR releases are now available that supports Signature Version 4: emr\-4\.7\.4, emr\-4\.8\.5, emr\-4\.9\.6, emr\-4\.10\.1, emr\-5\.1\.1, emr\-5\.2\.3, emr\-5\.3\.2, emr\-5\.4\.1, emr\-5\.5\.4, emr\-5\.6\.1, emr\-5\.7\.1, emr\-5\.8\.3, emr\-5\.9\.1, emr\-5\.10\.1, emr\-5\.11\.4, emr\-5\.12\.3, emr\-5\.13\.1, emr\-5\.14\.2, emr\-5\.15\.1, emr\-5\.16\.1, emr\-5\.17\.2, emr\-5\.18\.1, emr\-5\.19\.1, emr\-5\.20\.1, and emr\-5\.21\.2\. EMR version 5\.22\.0 and later already support Signature Version 4\.  
You do not need to change your application code to use Signature Version 4 if you are using Amazon EMR applications, such as Apache Spark, Apache Hive, Presto, etc\. If you are using custom applications, which are not included with Amazon EMR, you may need to update your code to use Signature Version 4\. For more information about what updates may be required, see [Moving from Signature Version 2 to Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html#UsingAWSSDK-move-to-Sig4)\.

## Release 6\.2\.0 \(Latest version of Amazon EMR 6\.x series\)<a name="emr-620-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

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
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions of Amazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latest Amazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
Amazon EMR clusters that are running Amazon Linux or Amazon Linux 2 AMIs \(Amazon Linux Machine Images\) use default Amazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If new Amazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an EMR version is released, EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latest Amazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
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

## Release 5\.33\.0 \(Latest version of Amazon EMR 5\.x series\)<a name="emr-5330-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 5\.33\.0\. Changes are relative to 5\.32\.0\.

Initial release date: Apr 19, 2021

**Upgrades**
+ Upgraded Amazon Glue connector to version 1\.15\.0
+ Upgraded AWS Java SDK to version 1\.11\.970
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
+ **Lower "Max open files" limit on older AL2\.** Amazon EMR releases: emr\-5\.30\.x, emr\-5\.31\.0, emr\-5\.32\.0, emr\-6\.0\.0, emr\-6\.1\.0, and emr\-6\.2\.0 are based on older versions of Amazon Linux 2 \(AL2\), which have a lower ulimit setting for “Max open files” when EMR clusters are created with the default AMI\. The lower open file limit causes a "Too many open files" error when submitting Spark job\. In the impacted EMR releases, the Amazon EMR default AMI has a default ulimit setting of 4096 for "Max open files," which is lower than the 65536 file limit in the latest Amazon Linux 2 AMI\. The lower ulimit setting for "Max open files" causes Spark job failure when the Spark driver and executor try to open more than 4096 files\. To fix the issue, Amazon EMR has a bootstrap action \(BA\) script that adjusts the ulimit setting at cluster creation\. Amazon EMR releases 6\.3\.0 and 5\.33\.0 will include a permanent fix with a higher "Max open files" setting\.

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
Amazon EMR clusters that are running Amazon Linux or Amazon Linux 2 AMIs \(Amazon Linux Machine Images\) use default Amazon Linux behavior, and do not automatically download and install important and critical kernel updates that require a reboot\. This is the same behavior as other Amazon EC2 instances running the default Amazon Linux AMI\. If new Amazon Linux software updates that require a reboot \(such as, kernel, NVIDIA, and CUDA updates\) become available after an EMR version is released, EMR cluster instances running the default AMI do not automatically download and install those updates\. To get kernel updates, you can [customize your Amazon EMR AMI](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-custom-ami.html) to [use the latest Amazon Linux AMI](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/finding-an-ami.html)\.
+ Console support to create a security configuration that specifies the AWS Ranger integration option is currently not supported in the GovCloud region\. Security configuration can be done using the CLI\. See [Create the EMR Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger-security-config.html) in the *Amazon EMR Management Guide*\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.