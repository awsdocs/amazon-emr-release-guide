# What's new?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR 6\.x series and 5\.x series\. These release notes are also available on the [Release 6\.3\.0 Tab](emr-release-6x.md#emr-630-release) and [Release 5\.33\.0 Tab](emr-release-5x.md#emr-5330-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier release notes going back to release version 4\.2\.0, see [Amazon EMR what's new history](emr-whatsnew-history.md)\.

**Note**  
Twenty\-five previous Amazon EMR release versions now use AWS Signature Version 4 to authenticate requests to Amazon S3\. The use of AWS Signature version 2 is being phased out and new S3 buckets created after June 24, 2020 will not support Signature Version 2 signed requests\. Existing buckets will continue to support Signature Version 2\. We recommend migrating to an Amazon EMR release that supports Signature Version 4 so you can continue accessing new S3 buckets and avoid any potential interruption to your workloads\.  
The following EMR releases are now available that supports Signature Version 4: emr\-4\.7\.4, emr\-4\.8\.5, emr\-4\.9\.6, emr\-4\.10\.1, emr\-5\.1\.1, emr\-5\.2\.3, emr\-5\.3\.2, emr\-5\.4\.1, emr\-5\.5\.4, emr\-5\.6\.1, emr\-5\.7\.1, emr\-5\.8\.3, emr\-5\.9\.1, emr\-5\.10\.1, emr\-5\.11\.4, emr\-5\.12\.3, emr\-5\.13\.1, emr\-5\.14\.2, emr\-5\.15\.1, emr\-5\.16\.1, emr\-5\.17\.2, emr\-5\.18\.1, emr\-5\.19\.1, emr\-5\.20\.1, and emr\-5\.21\.2\. EMR version 5\.22\.0 and later already support Signature Version 4\.  
You do not need to change your application code to use Signature Version 4 if you are using Amazon EMR applications, such as Apache Spark, Apache Hive, Presto, etc\. If you are using custom applications, which are not included with Amazon EMR, you may need to update your code to use Signature Version 4\. For more information about what updates may be required, see [Moving from Signature Version 2 to Signature Version 4](https://docs.aws.amazon.com/AmazonS3/latest/dev/UsingAWSSDK.html#UsingAWSSDK-move-to-Sig4)\.

## Release 6\.3\.0 \(latest version of Amazon EMR 6\.x series\)<a name="emr-630-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

The following release notes include information for Amazon EMR release version 6\.3\.0\. Changes are relative to 6\.2\.0\.

Initial release date: May 12, 2021

**Supported applications**
+ AWS SDK for Java version 1\.11\.977
+ CloudWatch Sink version 2\.1\.0
+ DynamoDB Connector version 4\.16\.0
+ EMRFS version 2\.46\.0
+ Amazon EMR Goodies version 3\.2\.0
+ Amazon EMR Kinesis Connector version 3\.5\.0
+ Amazon EMR Record Server version 2\.0\.0
+ Amazon EMR Scripts version 2\.5\.0
+ Flink version 1\.12\.1
+ Ganglia version 3\.7\.2
+ AWS Glue Hive Metastore Client version 3\.2\.0
+ Hadoop version 3\.2\.1\-amzn\-3
+ HBase version 2\.2\.6\-amzn\-1
+ HBase\-operator\-tools 1\.0\.0
+ HCatalog version 3\.1\.2\-amzn\-0
+ Hive version 3\.1\.2\-amzn\-4
+ Hudi version 0\.7\.0\-amzn\-0
+ Hue version 4\.9\.0
+ Java JDK version Corretto\-8\.282\.08\.1 \(build 1\.8\.0\_282\-b08\)
+ JupyterHub version 1\.2\.0
+ Livy version 0\.7\.0\-incubating
+ MXNet version 1\.7\.0
+ Oozie version 5\.2\.1
+ Phoenix version 5\.0\.0
+ Pig version 0\.17\.0
+ Presto version 0\.245\.1\-amzn\-0
+ PrestoSQL version 350
+ Apache Ranger KMS \(multi\-master transparent encryption\) version 2\.0\.0
+ ranger\-plugins 2\.0\.1\-amzn\-0
+ ranger\-s3\-plugin 1\.1\.0
+ SageMaker Spark SDK version 1\.4\.1
+ Scala version 2\.12\.10 \(OpenJDK 64\-Bit Server VM, Java 1\.8\.0\_282\)
+ Spark version 3\.1\.1\-amzn\-0
+ spark\-rapids 0\.4\.1
+ Sqoop version 1\.4\.7
+ TensorFlow version 2\.4\.1
+ tez version 0\.9\.2
+ Zeppelin version 0\.9\.0
+ Zookeeper version 3\.4\.14
+ Connectors and drivers: DynamoDB Connector 4\.16\.0

**New features**
+ With Amazon EMR 6\.3\.0, you can launch a cluster that natively integrates with Apache Ranger\. Apache Ranger is an open\-source framework to enable, monitor, and manage comprehensive data security across the Hadoop platform\. For more information, see [Apache Ranger](https://ranger.apache.org/)\. With native integration, you can bring your own Apache Ranger to enforce fine\-grained data access control on Amazon EMR\. See [Integrate Amazon EMR with Apache Ranger](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger.html) in the Amazon EMR Management Guide\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.
+ Instance Metadata Service \(IMDS\) V2 support status: For Amazon EMR 6\.2 or later, Amazon EMR components use IMDSv2 for all IMDS calls\. For IMDS calls in your application code, you can use both IMDSv1 and IMDSv2, or configure the IMDS to use only IMDSv2 for added security\. If you disable IMDSv1 in earlier Amazon EMR 6\.x releases, it causes cluster startup failure\.

**Changes, enhancements, and resolved issues**
+ The file output committer default algorithm has been changed from the v2 algorithm to the v1 algorithm in open source Spark 3\.1\. For more information, see this [Apache Spark JIRA ticket\.](https://issues.apache.org/jira/browse/SPARK-33019)
+ Amazon EMR reverted to the v2 algorithm, the default used in prior Amazon EMR 6\.x releases, to prevent performance regression\. To restore the open source Spark 3\.1 behavior, set `spark.hadoop.mapreduce.fileoutputcommitter.algorithm.version` to `1`\. Open source Spark made this change because task commit in file output committer algorithm v2 is not atomic, which can cause an output data correctness issue in some cases\. However, task commit in algorithm v1 is also not atomic\. In some scenarios task commit includes a delete performed before a rename\. This can result in a silent data correctness issue\.

**Known issues**
+ For Amazon EMR 6\.3\.0 and 6\.2\.0 private subnet clusters, you cannot acces the Ganglia web UI\. You will get an "access denied \(403\)" error\. Other web UIs, such as Spark, Hue, JupyterHub, Zeppelin, Livy, and Tez are working normally\. Ganglia web UI access on public subnet clusters are also working normally\. To resolve this issue, restart httpd service on the master node with `sudo systemctl restart httpd`\.
+ When AWS Glue Data Catalog is enabled, using Spark to access a AWS Glue DB with null string location URI may fail\. This happens to earlier Amazon EMR releases, but SPARK\-31709 \(https://issues\.apache\.org/jira/browse/SPARK\-31709\) makes it apply to more cases\. For example, when creating a table within the default AWS Glue DB whose location URI is a null string, `spark.sql("CREATE TABLE mytest (key string) location '/table_path';")` fails with the message, "Cannot create a Path from an empty string\." To work around this, manually set a location URI of your AWS Glue databases, then create tables within these databases using Spark\.
+ In Amazon EMR 6\.3\.0, PrestoSQL has upgraded from version 343 to version 350\. There are two security related changes from the open source that relate to this version change\. File\-based catalog access control is changed from `deny` to `allow` when table, schema, or session property rules are not defined\. Also, file\-based system access control is changed to support files without catalog rules defined\. In this case, all access to catalogs is allowed\.

  For more information, see [Release 344 \(9 Oct 2020\)](https://trino.io/docs/current/release/release-344.html#security)\.
+ Note that the Hadoop user directory \(/home/hadoop\) is readable by everyone\. It has Unix 755 \(drwxr\-xr\-x\) directory permissions to allow read access by frameworks like Hive\. You can put files in /home/hadoop and its subdirectories, but be aware of the permissions on those directories to protect sensitive information\.
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

## Release 5\.33\.0 \(latest version of Amazon EMR 5\.x series\)<a name="emr-5330-whatsnew"></a>

New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

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

**Changes, enhancements, and resolved issues**
+ Upgraded component versions\.
+ For a list of component versions, see [About Amazon EMR Releases](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-components.html) in this guide\.

**New features**
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
+ Console support to create a security configuration that specifies the AWS Ranger integration option is currently not supported in the GovCloud region\. Security configuration can be done using the CLI\. See [Create the EMR Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ranger-security-config.html) in the *Amazon EMR Management Guide*\.
+ Scoped managed policies: To align with AWS best practices, Amazon EMR has introduced v2 EMR\-scoped default managed policies as replacements for policies that will be deprecated\. See [Amazon EMR Managed Policies](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-managed-iam-policies.html)\.