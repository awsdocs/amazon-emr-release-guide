# Configure Applications<a name="emr-configure-apps"></a>

To override the default configurations for an application, you can supply a configuration object\. You can either use a shorthand syntax to provide the configuration, or you can reference the configuration object in a JSON file\. Configuration objects consist of a classification, properties, and optional nested configurations\. Properties correspond to the application settings you want to change\. You can specify multiple classifications for multiple applications in a single JSON object\.

**Warning**  
Amazon EMR Describe and List API operations will emit custom and configurable settings, which are used as a part of Amazon EMR job flows, in plaintext\. We recommend not to insert sensitive information, such as passwords, in these settings\.

The configuration classifications that are available vary by Amazon EMR release version\. For a list of configuration classifications that are available for each release version of Amazon EMR, see [About Amazon EMR Releases](emr-release-components.md)\.

The following is example JSON file for a list of configurations\.

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

A configuration classification often maps to an application\-specific configuration file\. For example, the `hive-site` classification maps to settings in the `hive-site.xml` configuration file for Hive\. An exception to this is the no longer supported bootstrap action `configure-daemons`, which is used to set environment parameters such as `--namenode-heap-size`\. Options like this are subsumed into the `hadoop-env` and `yarn-env` classifications with their own nested export classifications\. If any classification ends in `env`, use the export sub\-classification\. 

Another exception is `s3get`, which is used to place a customer `EncryptionMaterialsProvider` object on each node in a cluster for use in client\-side encryption\. An option was added to the `emrfs-site` classification for this purpose\.

The following is an example of the `hadoop-env` classification\.

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

The following is an example of the yarn\-env classification\.

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

The following settings do not belong to a configuration file but are used by Amazon EMR to potentially configure multiple settings on your behalf\.


**Settings curated by Amazon EMR**  

| Application | Release label classification | Valid properties | When to use | 
| --- | --- | --- | --- | 
| Spark | spark | maximizeResourceAllocation | Configure executors to utilize the maximum resources of each node\. | 

**Topics**
+ [Configure Applications when You Create a Cluster](emr-configure-apps-create-cluster.md)
+ [Reconfigure an Instance Group in a Running Cluster](emr-configure-apps-running-cluster.md)
+ [Configure Applications to Use a Specific Java Virtual Machine](configuring-java8.md)