# Configuring Applications<a name="emr-configure-apps"></a>

You can override the default configurations for applications by supplying a configuration object for applications when you create a cluster\. The configuration object is referenced as a JSON file\. Configuration objects consist of a classification, properties, and optional nested configurations\. Properties are the settings you want to change in that file\. You can specify multiple classifications for multiple applications in a single JSON object\.

**Warning**  
Amazon EMR Describe and List APIs will emit custom/configurable settings used as a part of EMR jobflows in plain text\. We recommend not to insert sensitive information such as passwords in such settings\.

The configuration classifications available vary by Amazon EMR release version\. For a list of configuration classifications that are available for each release version of Amazon EMR, see [About Amazon EMR Releases](emr-release-components.md)\.

Example JSON for a list of configurations is provided below:

```
[
  {
    "Classification": "core-site",
    "Properties": {
      "hadoop.security.groups.cache.secs": "250"
    }
  },
  {
    "Classification": "mapred-site",
    "Properties": {
      "mapred.tasktracker.map.tasks.maximum": "2",
      "mapreduce.map.sort.spill.percent": "0.90",
      "mapreduce.tasktracker.reduce.tasks.maximum": "5"
    }
  }
]
```

A configuration classification often maps to an application\-specific configuration file\. For example, the `hive-site` classification maps to settings in the `hive-site.xml` configuration file for Hive\. An exception to this is the deprecated bootstrap action `configure-daemons`, which is used to set environment parameters such as `--namenode-heap-size`\. Now, options like this are subsumed into the `hadoop-env` and `yarn-env` classifications with their own nested export classifications\. If any classification ends in "env", you should use the export sub\-classification\. Another exception is `s3get`, which was used to place a customer `EncryptionMaterialsProvider` object on each node in a cluster for use in client\-side encryption\. An option was added to the `emrfs-site` classification for this purpose\.

An example of the `hadoop-env` classification is provided below:

```
[
  {
    "Classification": "hadoop-env",
    "Properties": {
      
    },
    "Configurations": [
      {
        "Classification": "export",
        "Properties": {
          "HADOOP_DATANODE_HEAPSIZE": "2048",
          "HADOOP_NAMENODE_OPTS": "-XX:GCTimeRatio=19"
        },
        "Configurations": [
          
        ]
      }
    ]
  }
]
```

An example of the yarn\-env classification is provided below:

```
[
  {
    "Classification": "yarn-env",
    "Properties": {
      
    },
    "Configurations": [
      {
        "Classification": "export",
        "Properties": {
          "YARN_RESOURCEMANAGER_OPTS": "-Xdebug -Xrunjdwp:transport=dt_socket"
        },
        "Configurations": [
          
        ]
      }
    ]
  }
]
```

The following settings do not belong to a configuration file but are used by Amazon EMR to potentially set multiple settings on your behalf\.


**Amazon EMR\-curated Settings**  

| Application | Release label classification | Valid properties | When to use | 
| --- | --- | --- | --- | 
| Spark | spark | maximizeResourceAllocation | Configure executors to utilize the maximum resources of each node\. | 

## Supplying a Configuration in the Console<a name="w3ab1c14c26"></a>

To supply a configuration, you navigate to the **Create cluster** page and choose **Edit software settings**\. You can then enter the configuration directly \(in JSON or using shorthand syntax demonstrated in shadow text\) in the console or provide an Amazon S3 URI for a file with a JSON `Configurations` object\.

## Supplying a Configuration Using the CLI<a name="w3ab1c14c28"></a>

You can provide a configuration to create\-cluster by supplying a path to a JSON file stored locally or in Amazon S3\. The following example assumes you are using default roles for Amazon EMR and the roles have been created\. If you need to create the roles, run `aws emr create-default-roles` first\.

```
aws emr create-cluster --use-default-roles --release-label emr-5.15.0 --instance-type m4.large --instance-count 2 --applications Name=Hive --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
```

If you configuration is in your local directory, you can use the following:

```
aws emr create-cluster --use-default-roles --release-label emr-5.15.0 --applications Name=Hive \
--instance-type m4.large --instance-count 3 --configurations file://./configurations.json
```

## Supplying a Configuration Using the Java SDK<a name="w3ab1c14c30"></a>

The following program excerpt shows how to supply a configuration using the AWS SDK for Java:

```
Application hive = new Application().withName("Hive");

Map<String,String> hiveProperties = new HashMap<String,String>();
	hiveProperties.put("hive.join.emit.interval","1000");
	hiveProperties.put("hive.merge.mapfiles","true");
	    
Configuration myHiveConfig = new Configuration()
	.withClassification("hive-site")
	.withProperties(hiveProperties);

RunJobFlowRequest request = new RunJobFlowRequest()
	.withName("Create cluster with ReleaseLabel")
	.withReleaseLabel("emr-5.15.0")
	.withApplications(hive)
	.withConfigurations(myHiveConfig)
	.withServiceRole("EMR_DefaultRole")
	.withJobFlowRole("EMR_EC2_DefaultRole")
	.withInstances(new JobFlowInstancesConfig()
		.withEc2KeyName("myKey")
		.withInstanceCount(1)
		.withKeepJobFlowAliveWhenNoSteps(true)
		.withMasterInstanceType("m4.large")
		.withSlaveInstanceType("m4.large")
	);
```

## Configuring Applications to Use a Specific Java Virtual Machine<a name="configuring-java8"></a>

Java 8 is the default Java virtual machine \(JVM\) for cluster instances created using Amazon EMR version 4\.9\.2 or later\. To override this JVM setting—for example, to use Java 8 with a cluster created using Amazon EMR version 4\.8\.0—you can set `JAVA_HOME` for an application by supplying the setting to its environment classification, `application-env`\. For Hadoop and Hive, this would look like:

```
[
    {
        "Classification": "hadoop-env", 
        "Configurations": [
            {
                "Classification": "export", 
                "Configurations": [], 
                "Properties": {
                    "JAVA_HOME": "/usr/lib/jvm/java-1.8.0"
                }
            }
        ], 
        "Properties": {}
    }
]
```

For Spark, if you are writing a driver for submission in cluster mode, the driver will use Java 7 but setting the environment can ensure that the executors use Java 8\. To do this, we recommend setting both Hadoop and Spark classifications:

```
[
    {
        "Classification": "hadoop-env", 
        "Configurations": [
            {
                "Classification": "export", 
                "Configurations": [], 
                "Properties": {
                    "JAVA_HOME": "/usr/lib/jvm/java-1.8.0"
                }
            }
        ], 
        "Properties": {}
    }, 
    {
        "Classification": "spark-env", 
        "Configurations": [
            {
                "Classification": "export", 
                "Configurations": [], 
                "Properties": {
                    "JAVA_HOME": "/usr/lib/jvm/java-1.8.0"
                }
            }
        ], 
        "Properties": {}
    }
]
```

## Service ports<a name="w3ab1c14c34"></a>

The following are YARN and HDFS service ports\. These settings reflect Hadoop defaults\. Other application services are hosted at default ports unless otherwise documented\. Please see the application's project documentation for further information\.


**Port Settings for YARN and HDFS**  

| Setting | Hostname/Port | 
| --- | --- | 
| fs\.default\.name | default \(hdfs://emrDeterminedIP:8020\)  | 
| dfs\.datanode\.address | default \(0\.0\.0\.0:50010\)  | 
| dfs\.datanode\.http\.address | default \(0\.0\.0\.0:50075\)  | 
| dfs\.datanode\.https\.address | default \(0\.0\.0\.0:50475\) | 
| dfs\.datanode\.ipc\.address | default \(0\.0\.0\.0:50020\) | 
| dfs\.http\.address | default \(0\.0\.0\.0:50070\)  | 
| dfs\.https\.address | default \(0\.0\.0\.0:50470\)  | 
| dfs\.secondary\.http\.address | default \(0\.0\.0\.0:50090\) | 
| yarn\.nodemanager\.address | default \($\{yarn\.nodemanager\.hostname\}:0\)  | 
| yarn\.nodemanager\.localizer\.address  | default \($\{yarn\.nodemanager\.hostname\}:8040\) | 
| yarn\.nodemanager\.webapp\.address | default \($\{yarn\.nodemanager\.hostname\}:8042\) | 
| yarn\.resourcemanager\.address | default \($\{yarn\.resourcemanager\.hostname\}:8032\) | 
| yarn\.resourcemanager\.admin\.address | default \($\{yarn\.resourcemanager\.hostname\}:8033\) | 
| yarn\.resourcemanager\.resource\-tracker\.address | default \($\{yarn\.resourcemanager\.hostname\}:8031\) | 
| yarn\.resourcemanager\.scheduler\.address | default \($\{yarn\.resourcemanager\.hostname\}:8030\) | 
| yarn\.resourcemanager\.webapp\.address | default \($\{yarn\.resourcemanager\.hostname\}:8088\) | 
| yarn\.web\-proxy\.address | default \(no\-value\)  | 
| yarn\.resourcemanager\.hostname | emrDeterminedIP | 

**Note**  
The term *emrDeterminedIP* is an IP address that is generated by the Amazon EMR control plane\. In the newer version, this convention has been eliminated except for the `yarn.resourcemanager.hostname` and `fs.default.name` settings\.

## Application users<a name="w3ab1c14c36"></a>

Applications will run processes as their own user\. For example, Hive JVMs will run as user `hive`, MapReduce JVMs will run as `mapred`, and so on\. The following process status demonstrates this:

```
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
hive      6452  0.2  0.7 853684 218520 ?       Sl   16:32   0:13 /usr/lib/jvm/java-openjdk/bin/java -Xmx256m -Dhive.log.dir=/var/log/hive -Dhive.log.file=hive-metastore.log -Dhive.log.threshold=INFO -Dhadoop.log.dir=/usr/lib/hadoop
hive      6557  0.2  0.6 849508 202396 ?       Sl   16:32   0:09 /usr/lib/jvm/java-openjdk/bin/java -Xmx256m -Dhive.log.dir=/var/log/hive -Dhive.log.file=hive-server2.log -Dhive.log.threshold=INFO -Dhadoop.log.dir=/usr/lib/hadoop/l
hbase     6716  0.1  1.0 1755516 336600 ?      Sl   Jun21   2:20 /usr/lib/jvm/java-openjdk/bin/java -Dproc_master -XX:OnOutOfMemoryError=kill -9 %p -Xmx1024m -ea -XX:+UseConcMarkSweepGC -XX:+CMSIncrementalMode -Dhbase.log.dir=/var/
hbase     6871  0.0  0.7 1672196 237648 ?      Sl   Jun21   0:46 /usr/lib/jvm/java-openjdk/bin/java -Dproc_thrift -XX:OnOutOfMemoryError=kill -9 %p -Xmx1024m -ea -XX:+UseConcMarkSweepGC -XX:+CMSIncrementalMode -Dhbase.log.dir=/var/
hdfs      7491  0.4  1.0 1719476 309820 ?      Sl   16:32   0:22 /usr/lib/jvm/java-openjdk/bin/java -Dproc_namenode -Xmx1000m -Dhadoop.log.dir=/var/log/hadoop-hdfs -Dhadoop.log.file=hadoop-hdfs-namenode-ip-10-71-203-213.log -Dhadoo
yarn      8524  0.1  0.6 1626164 211300 ?      Sl   16:33   0:05 /usr/lib/jvm/java-openjdk/bin/java -Dproc_proxyserver -Xmx1000m -Dhadoop.log.dir=/var/log/hadoop-yarn -Dyarn.log.dir=/var/log/hadoop-yarn -Dhadoop.log.file=yarn-yarn-
yarn      8646  1.0  1.2 1876916 385308 ?      Sl   16:33   0:46 /usr/lib/jvm/java-openjdk/bin/java -Dproc_resourcemanager -Xmx1000m -Dhadoop.log.dir=/var/log/hadoop-yarn -Dyarn.log.dir=/var/log/hadoop-yarn -Dhadoop.log.file=yarn-y
mapred    9265  0.2  0.8 1666628 260484 ?      Sl   16:33   0:12 /usr/lib/jvm/java-openjdk/bin/java -Dproc_historyserver -Xmx1000m -Dhadoop.log.dir=/usr/lib/hadoop/logs -Dhadoop.log.file=hadoop.log -Dhadoop.home.dir=/usr/lib/hadoop
```