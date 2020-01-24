# Configuring Flink<a name="flink-configure"></a>

You may want to configure Flink using a configuration file\. For example, the main configuration file for Flink is called `flink-conf.yaml`\. This is configurable using the Amazon EMR configuration API\.

**To configure the number of task slots used for Flink using the AWS CLI**

1. Create a file, `configuration.json`, with the following content:

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
   aws emr create-cluster --release-label emr-5.29.0 \
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
It is also possible to change some configurations using the Flink API\. For more information, see [https://ci.apache.org/projects/flink/flink-docs-master/dev/api_concepts.html](https://ci.apache.org/projects/flink/flink-docs-master/dev/api_concepts.html) in the Flink documentation\.  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

## Parallelism Options<a name="flink-parallelism"></a>

As the owner of your application, you know best what resources should be assigned to tasks within Flink\. For the purposes of the examples in this documentation, use the same number of tasks as the slave instances that you use for the application\. We generally recommend this for the initial level of parallelism but you can also increase the granularity of parallelism using task slots, which should generally not exceed the number of [virtual cores](https://aws.amazon.com/ec2/virtualcores/) per instance\. For more information about Flink’s architecture, see [https://ci.apache.org/projects/flink/flink-docs-master/concepts/index.html](https://ci.apache.org/projects/flink/flink-docs-master/concepts/index.html) in the Flink documentation\.

## Configurable Files<a name="flink-configurable-files"></a>

Currently, the files that are configurable within the Amazon EMR configuration API are:
+ `flink-conf.yaml`
+ `log4j.properties`
+ `log4j-yarn-session.properties`
+ `log4j-cli.properties`

## Configuring Flink on an EMR Cluster with Multiple Master Nodes<a name="flink-multi-master"></a>

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

You must configure both maximum application master attempts for YARN and application attempts for Flink\. For more information, see [Configuration of YARN Cluster High Availability](https://ci.apache.org/projects/flink/flink-docs-release-1.8/ops/jobmanager_high_availability.html#maximum-application-master-attempts-yarn-sitexml)\. You may also want to configure Flink checkpointing to make restarted JobManager recover running jobs from previously completed checkpoints\. For more information, see [Flink Checkpointing](https://ci.apache.org/projects/flink/flink-docs-release-1.8/dev/stream/state/checkpointing.html)\.