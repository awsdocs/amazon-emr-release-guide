# Configuring Flink<a name="flink-configure"></a>

You may want to configure Flink using a configuration file\. For example, the main configuration file for Flink is called `flink-conf.yaml`\. This is configurable using the Amazon EMR configuration API\.

**To configure the number of task slots used for Flink using the AWS CLI**

1. Create a file, `configurations.json`, with the following content:

   ```
   [
       {
         "Classification": "flink-conf",
         "Properties": {
           "taskmanager.numberOfTaskSlots":"2"
         }
       }
   ]
   ```

1. Next, create a cluster with the following configuration:

   ```
   aws emr create-cluster --release-label emr-5.34.0 \
   --applications Name=Flink \
   --configurations file://./configurations.json \
   --region us-east-1 \
   --log-uri s3://myLogUri \
   --instance-type m5.xlarge \
   --instance-count 2 \
   --service-role EMR_DefaultRole \ 
   --ec2-attributes KeyName=YourKeyName,InstanceProfile=EMR_EC2_DefaultRole
   ```

**Note**  
It is also possible to change some configurations using the Flink API\. For more information, see [https://ci.apache.org/projects/flink/flink-docs-release-1.12/concepts/index.html](https://ci.apache.org/projects/flink/flink-docs-release-1.12/concepts/index.html) in the Flink documentation\.  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

## Parallelism options<a name="flink-parallelism"></a>

As the owner of your application, you know best what resources should be assigned to tasks within Flink\. For the purposes of the examples in this documentation, use the same number of tasks as the slave instances that you use for the application\. We generally recommend this for the initial level of parallelism but you can also increase the granularity of parallelism using task slots, which should generally not exceed the number of [virtual cores](https://aws.amazon.com/ec2/virtualcores/) per instance\. For more information about Flink's architecture, see [https://ci.apache.org/projects/flink/flink-docs-master/concepts/index.html](https://ci.apache.org/projects/flink/flink-docs-master/concepts/index.html) in the Flink documentation\.

## Configurable files<a name="flink-configurable-files"></a>

Currently, the files that are configurable within the Amazon EMR configuration API are:
+ `flink-conf.yaml`
+ `log4j.properties`
+ `flink-log4j-session`
+ `log4j-cli.properties`

## Configuring Flink on an EMR Cluster with multiple master nodes<a name="flink-multi-master"></a>

The JobManager of Flink remains available during the master node failover process in an EMR cluster with multiple master nodes\. Beginning with Amazon EMR version 5\.28\.0, JobManager high availability is also enabled automatically\. No manual configuration is needed\.

With Amazon EMR versions 5\.27\.0 or earlier, the JobManager is a single point of failure\. When the JobManager fails, it loses all job states and will not resume the running jobs\. You can enable JobManager high availability by configuring application attempt count, checkpointing, and enabling ZooKeeper as state storage for Flink, as the following example demonstrates:

```
[
  {
    "Classification": "yarn-site",
    "Properties": {
      "yarn.resourcemanager.am.max-attempts": "10"
    }
  },
  {
    "Classification": "flink-conf",
    "Properties": {
        "yarn.application-attempts": "10",
        "high-availability": "zookeeper",
        "high-availability.zookeeper.quorum": "%{hiera('hadoop::zk')}",
        "high-availability.storageDir": "hdfs:///user/flink/recovery",
        "high-availability.zookeeper.path.root": "/flink"
    }
  }
]
```

You must configure both maximum application master attempts for YARN and application attempts for Flink\. For more information, see [Configuration of YARN cluster high availability](https://ci.apache.org/projects/flink/flink-docs-release-1.8/ops/jobmanager_high_availability.html#maximum-application-master-attempts-yarn-sitexml)\. You may also want to configure Flink checkpointing to make restarted JobManager recover running jobs from previously completed checkpoints\. For more information, see [Flink checkpointing](https://ci.apache.org/projects/flink/flink-docs-release-1.8/dev/stream/state/checkpointing.html)\.

## Configuring memory process size<a name="flink-process-memory"></a>

For Amazon EMR versions that use Flink 1\.11\.x, you must configure the total memory process size for both JobManager \(`jobmanager.memory.process.size`\) and TaskManager \(`taskmanager.memory.process.size`\) in `flink-conf.yaml`\. You can set these values by either configuring the cluster with the configuration API or manually uncommenting these fields via SSH\. Flink provides the following default values\.
+ `jobmanager.memory.process.size`: 1600m
+ `taskmanager.memory.process.size`: 1728m

To exclude JVM metaspace and overhead, use the total Flink memory size \(`taskmanager.memory.flink.size`\) instead of `taskmanager.memory.process.size`\. The default value for `taskmanager.memory.process.size` is 1280m\. It's not recommended to set both `taskmanager.memory.process.size` and `taskmanager.memory.process.size`\.

All Amazon EMR versions using Flink 1\.12\.0 and later have the default values listed in Flink's open\-source set as the default values on Amazon EMR, so you don't need to configure them yourself\.

## Configuring log output file size<a name="flink-log-output"></a>

Flink application containers create and write to three types of log files: `.out` files, `.log` files, and `.err` files\. Only `.err` files are compressed and removed from the file system, while `.log` and `.out` log files remain in the file system\. To ensure these output files remain manageable and the cluster remains stable, you can configure log rotation in `log4j.properties` to set a maximum number of files and limit their sizes\.

**Amazon EMR versions 5\.30\.0 and later**

Starting with Amazon EMR 5\.30\.0, Flink uses the log4j2 logging framework with the configuration classification name `flink-log4j.` The following example configuration demonstrates the log4j2 format\.

```
[
  {
    "Classification": "flink-log4j",
    "Properties": {
      "appender.rolling.name": "RollingFileAppender",
      "appender.rolling.type":"RollingFile",
      "appender.rolling.append" : "false",
      "appender.rolling.fileName" : "${sys:log.file}",
      "appender.rolling.filePattern" : "${sys:log.file}.%i",
      "appender.rolling.layout.type" : "PatternLayout",
      "appender.rolling.layout.pattern" : "%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %-60c %x - %m%n",
      "appender.rolling.policies.type" : "Policies",
      "appender.rolling.policies.size.type" : "SizeBasedTriggeringPolicy",
      "appender.rolling.policies.size.size" : "100MB",
      "appender.rolling.strategy.type" : "DefaultRolloverStrategy",
      "appender.rolling.strategy.max" : "10"
    },
  }
]
```

**Amazon EMR versions 5\.29\.0 and earlier**

With Amazon EMR versions 5\.29\.0 and earlier, Flink uses the log4j logging framework\. The following example configuration demonstrates the log4j format\.

```
[
  {
    "Classification": "flink-log4j",
    "Properties": {
      "log4j.appender.file": "org.apache.log4j.RollingFileAppender",
      "log4j.appender.file.append":"true",
      # keep up to 4 files and each file size is limited to 100MB
      "log4j.appender.file.MaxFileSize":"100MB",
      "log4j.appender.file.MaxBackupIndex":4,
      "log4j.appender.file.layout":"org.apache.log4j.PatternLayout",
      "log4j.appender.file.layout.ConversionPattern":"%d{yyyy-MM-dd HH:mm:ss,SSS} %-5p %-60c %x - %m%n"
    },
  }
]
```