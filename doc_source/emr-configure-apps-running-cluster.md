# Reconfigure an instance group in a running cluster<a name="emr-configure-apps-running-cluster"></a>

With Amazon EMR version 5\.21\.0 and later, you can reconfigure cluster applications and specify additional configuration classifications for each instance group in a running cluster\. To do so, you can use the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. When you update an application configuration for an instance group, Amazon EMR merges the new configuration with the existing configuration to create a new active configuration\. 

After you submit a reconfiguration request for an instance group, Amazon EMR assigns a version number to the new configuration specification\. You can track the version number of a configuration, or the state of an instance group, by viewing the CloudWatch events\. For more information, see [Monitor CloudWatch Events](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-manage-cloudwatch-events.html)\.

**Note**  
You can only override, and not delete, cluster configurations that were specified during cluster creation\.

## Considerations when you reconfigure an instance group<a name="emr-configure-apps-running-cluster-considerations"></a>

**Reconfiguration actions**  
When you submit a reconfiguration request using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK, Amazon EMR checks the existing on\-cluster configuration file\. If there are differences between the existing configuration and the file that you supply, Amazon EMR initiates reconfiguration actions, restarts some applications, and resets any manually modified configurations to the cluster defaults for the specified instance group\.   
Amazon EMR performs some default actions during every instance group reconfiguration\. These default actions might conflict with cluster customizations that you have made, and result in reconfiguration failures\. For information about how to troubleshoot reconfiguration failures, see [Troubleshoot instance group reconfiguration](#emr-configure-apps-running-cluster-troubleshoot)\.
Amazon EMR also initiates reconfiguration actions for the configuration classifications that you specify in your request\. For a complete list of these actions, see the Configuration Classifications section for the version of Amazon EMR that you use\. For example, [6\.2\.0 Configuration Classifications](emr-release-6x.md#emr-620-class)\.  
The Amazon EMR Release Guide only lists reconfiguration actions starting with Amazon EMR versions 5\.32\.0 and 6\.2\.0\.

**Service disruption**  
Amazon EMR follows a rolling process to reconfigure instances in the Task and Core instance groups\. Only 10 percent of the instances in an instance group are modified and restarted at a time\. This process takes longer to finish but reduces the chance of potential application failure in a running cluster\.   
To run YARN jobs during a YARN restart, you can either create an Amazon EMR cluster with multiple master nodes or set `yarn.resourcemanager.recovery.enabled` to `true` in your `yarn-site` configuration classification\. For more information about using multiple master nodes, see [High availability YARN ResourceManager](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ha-applications.html#emr-plan-ha-applications-YARN)\.

**Application validation**  
Amazon EMR checks that each application on the cluster is running after the reconfiguration restart process\. If any application is unavailable, the overall reconfiguration operation fails\. If a reconfiguration operation fails, Amazon EMR reverses the configuration parameters to the previous working version\.  
To avoid reconfiguration failure, we recommend that you only install applications on your cluster that you plan to use\. We also recommend that you make sure all cluster applications are healthy and running before you submit a reconfiguration request\.

**Limitations**

When you reconfigure an instance group in a running cluster, consider the following limitations:
+ Non\-YARN applications can fail during restart or cause cluster issues, especially if the applications aren't configured properly\. Clusters approaching maximum memory and CPU usage may run into issues after the restart process\. This is especially true for the master instance group\.
+ You can't submit a reconfiguration request when an instance group is being resized\. If a reconfiguration is initiated while an instance group is resizing, reconfiguration cannot start until the instance group has completed resizing, and vice versa\. 
+ After reconfiguring an instance group, Amazon EMR restarts the applications to allow the new configurations to take effect\. Job failure or other unexpected application behavior might occur if the applications are in use during reconfiguration\. 
+ If a reconfiguration for an instance group fails, Amazon EMR reverses the configuration parameters to the previous working version\. If the reversion process fails too, you must submit a new `ModifyInstanceGroup` request to recover the instance group from the `SUSPENDED` state\.
+ Reconfiguration requests for Phoenix configuration classifications are only supported in Amazon EMR version 5\.23\.0 and later, and are not supported in Amazon EMR version 5\.21\.0 or 5\.22\.0\. 
+ Reconfiguration requests for HBase configuration classifications are only supported in Amazon EMR version 5\.30\.0 and later, and are not supported in Amazon EMR versions 5\.23\.0 through 5\.29\.0\. 
+ Amazon EMR supports application reconfiguration requests on an EMR cluster with multiple master nodes only in Amazon EMR versions 5\.27\.0 and later\.
+ Reconfiguring `hdfs-encryption-zones` classification or any of the Hadoop KMS configuration classifications is not supported on an EMR cluster with multiple master nodes\.
+ Amazon EMR currently doesn't support certain reconfiguration requests for the capacity scheduler that require restarting the YARN ResourceManager\. For example, you cannot completely remove a queue\.

## Reconfigure an instance group in the console<a name="emr-configure-apps-running-cluster-console"></a>

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the cluster list under **Name**, choose the active cluster that you want to reconfigure\.

1. Open the cluster details page for the cluster, and go to the **Configurations** tab\. 

1. In the **Filter** drop\-down list, select the instance group that you want to reconfigure\. 

1. In the **Reconfigure** drop\-down menu, choose either **Edit in table** or **Edit in JSON file**\.
   + **Edit in table** \- In the configuration classification table, edit the property and value for existing configurations, or choose **Add configuration** to supply additional configuration classifications\. 
   + **Edit in JSON file** \- Enter the configuration directly in JSON, or use shorthand syntax \(demonstrated in shadow text\)\. Otherwise, provide an Amazon S3 URI for a file with a JSON `Configurations` object\.
**Note**  
The **Source** column in the configuration classification table indicates whether the configuration is supplied when you create a cluster, or when you specify additional configurations for this instance group\. You can edit the configurations for an instance group from both sources\. You cannot delete initial cluster configurations, but you can override them for an instance group\.   
You can also add or edit nested configuration classifications directly in the table\. For example, to supply an additional `export` sub\-classification of `hadoop-env`, add a `hadoop.export` configuration classification in the table\. Then, provide a specific property and value for this classification\. 

1. \(Optional\) Select **Apply this configuration to all active instance groups**\.

1. Save the changes\.

## Reconfigure an instance group using the CLI<a name="emr-configure-apps-running-cluster-cli"></a>

Use the modify\-instance\-groups command to specify a new configuration for an instance group in a running cluster\.

**Note**  
In the following examples, replace *<j\-2AL4XXXXXX5T9>* with your cluster ID and replace *<ig\-1xxxxxxx9>* with your instance group ID\.

**Example – Replace a configuration for an instance group**  
The following example references a configuration JSON file called `instanceGroups.json` to edit the property of the YARN NodeManager disk health checker for an instance group\.  

1. Prepare your configuration classification, and save it as `instanceGroups.json` in the same directory where you will run the command\.

   ```
   [
      {
         "InstanceGroupId":"<ig-1xxxxxxx9>",
         "Configurations":[
            {
               "Classification":"yarn-site",
               "Properties":{
                  "yarn.nodemanager.disk-health-checker.enable":"true",
                  "yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage":"100.0"
               },
               "Configurations":[]
            }
         ]
      }
   ]
   ```

1. Run the following command\.

   ```
   aws emr modify-instance-groups --cluster-id <j-2AL4XXXXXX5T9> \
   --instance-groups file://instanceGroups.json
   ```

**Example – Add a configuration to an instance group**  
If you want to add a configuration to an instance group, you must include all previously specified configurations for that instance group in your new `ModifyInstanceGroup` request\. Otherwise, the previously specified configurations are removed\.  
The following example adds a property for the YARN NodeManager virtual memory checker\. The configuration also includes previously specified values for the YARN NodeManager disk health checker so that the values won't be overwritten\.  

1. Prepare the following contents in `instanceGroups.json` and save it in the same directory where you will run the command\.

   ```
   [
      {
         "InstanceGroupId":"<ig-1xxxxxxx9>",
         "Configurations":[
            {
               "Classification":"yarn-site",
               "Properties":{
                  "yarn.nodemanager.disk-health-checker.enable":"true",
                  "yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage":"100.0",
                  "yarn.nodemanager.vmem-check-enabled":"true",
                  "yarn.nodemanager.vmem-pmem-ratio":"3.0"
               },
               "Configurations":[]
            }
         ]
      }
   ]
   ```

1. Run the following command\.

   ```
   aws emr modify-instance-groups --cluster-id <j-2AL4XXXXXX5T9> \
   --instance-groups file://instanceGroups.json
   ```

**Example – Delete a configuration for an instance group**  
To delete a configuration for an instance group, submit a new reconfiguration request that excludes the previous configuration\.   
You can only override the initial *cluster* configuration\. You cannot delete it\.
For example, to delete the configuration for the YARN NodeManager disk health checker from the previous example, submit a new `instanceGroups.json` with the following contents\.   

```
[
   {
      "InstanceGroupId":"<ig-1xxxxxxx9>",
      "Configurations":[
         {
            "Classification":"yarn-site",
            "Properties":{
               "yarn.nodemanager.vmem-check-enabled":"true",
               "yarn.nodemanager.vmem-pmem-ratio":"3.0"
            },
            "Configurations":[]
         }
      ]
   }
]
```
To delete all of the configurations in your last reconfiguration request, submit a reconfiguration request with an empty array of configurations\. For example,  

```
[
   {
      "InstanceGroupId":"<ig-1xxxxxxx9>",
      "Configurations":[]
   }
]
```

**Example – Reconfigure and resize an instance group in one request**  
The following example JSON demonstrates how to reconfigure and resize an instance group in the same request\.  

```
[
   {
      "InstanceGroupId":"<ig-1xxxxxxx9>",
      "InstanceCount":5,
      "EC2InstanceIdsToTerminate":["i-123"],
      "ForceShutdown":true,
      "ShrinkPolicy":{
         "DecommissionTimeout":10,
         "InstanceResizePolicy":{
            "InstancesToTerminate":["i-123"],
            "InstancesToProtect":["i-345"],
            "InstanceTerminationTimeout":20
         }
      },
      "Configurations":[
         {
            "Classification":"yarn-site",
            "Configurations":[],
            "Properties":{
               "yarn.nodemanager.disk-health-checker.enable":"true",
               "yarn.nodemanager.disk-health-checker.max-disk-utilization-per-disk-percentage":"100.0"
            }
         }
      ]
   }
]
```

## Reconfigure an instance group using the Java SDK<a name="emr-configure-apps-running-cluster-sdk"></a>

**Note**  
In the following examples, replace *<j\-2AL4XXXXXX5T9>* with your cluster ID and replace *<ig\-1xxxxxxx9>* with your instance group ID\.

The following code snippet provides a new configuration for an instance group using the AWS SDK for Java\.

```
AWSCredentials credentials = new BasicAWSCredentials("access-key", "secret-key");
AmazonElasticMapReduce emr = new AmazonElasticMapReduceClient(credentials);

Map<String,String> hiveProperties = new HashMap<String,String>();
hiveProperties.put("hive.join.emit.interval","1000");
hiveProperties.put("hive.merge.mapfiles","true");
        
Configuration configuration = new Configuration()
    .withClassification("hive-site")
    .withProperties(hiveProperties);
    
InstanceGroupModifyConfig igConfig = new InstanceGroupModifyConfig()
    .withInstanceGroupId("<ig-1xxxxxxx9>")
    .withConfigurations(configuration);

ModifyInstanceGroupsRequest migRequest = new ModifyInstanceGroupsRequest()
    .withClusterId("<j-2AL4XXXXXX5T9>")
    .withInstanceGroups(igConfig);

emr.modifyInstanceGroups(migRequest);
```

The following code snippet deletes a previously specified configuration for an instance group by supplying an empty array of configurations\.

```
List<Configuration> configurations = new ArrayList<Configuration>();

InstanceGroupModifyConfig igConfig = new InstanceGroupModifyConfig()
    .withInstanceGroupId("<ig-1xxxxxxx9>")
    .withConfigurations(configurations);

ModifyInstanceGroupsRequest migRequest = new ModifyInstanceGroupsRequest()
    .withClusterId("<j-2AL4XXXXXX5T9>")
    .withInstanceGroups(igConfig);

emr.modifyInstanceGroups(migRequest);
```

## Troubleshoot instance group reconfiguration<a name="emr-configure-apps-running-cluster-troubleshoot"></a>

If the reconfiguration process for an instance group fails, Amazon EMR reverts the reconfiguration and logs a failure message using an Amazon CloudWatch event\. The event provides a brief summary of the reconfiguration failure\. It lists the instances for which reconfiguration has failed and corresponding failure messages\. The following is an example failure message\.

```
The reconfiguration operation for instance group ig-1xxxxxxx9 in Amazon EMR cluster j-2AL4XXXXXX5T9 (ExampleClusterName) 
failed at 2021-01-01 00:00 UTC and took 2 minutes to fail. Failed configuration version is example12345. 
Failure message: Instance i-xxxxxxx1, i-xxxxxxx2, i-xxxxxxx3 failed with message "This is an example failure message".
```

To gather more data about a reconfiguration failure, you can check the node provisioning logs\. Doing so is particularly useful when you receive a message like the following\.

```
i-xxxxxxx1 failed with message “Unable to complete transaction and some changes were applied.”
```

------
#### [ On the node ]

**To access node provisioning logs by connecting to a node**

1. Use SSH to connect to the node on which reconfiguration has failed\. For instructions, see [Connect to your Linux instance](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html) in the *Amazon EC2* *User Guide for Linux Instances*\.

1. Navigate to the following directory, which contains the node provisioning log files\.

   ```
   /mnt/var/log/provision-node/
   ```

1. Open the `reports` subdirectory and search for the node provisioning report for your reconfiguration\. The `reports` directory organizes logs by reconfiguration version number, universally unique identifier \(UUID\), Amazon EC2 instance IP address, and timestamp\. Each report is a compressed YAML file that contains detailed information about the reconfiguration process\.

   The following is an example report file name and path\.

   ```
   /reports/2/ca598xxx-cxxx-4xxx-bxxx-6dbxxxxxxxxx/ip-10-73-xxx-xxx.ec2.internal/202104061715.yaml.gz
   ```

1. You can examine a report using a file viewer like `zless`, as in the following example\.

   ```
   zless 202104061715.yaml.gz
   ```

------
#### [ Amazon S3 ]

**To access node provisioning logs using Amazon S3**

1. Sign in to the AWS Management Console and open the Amazon S3 console at [https://console\.aws\.amazon\.com/s3/](https://console.aws.amazon.com/s3/)\.

1. Open the Amazon S3 bucket that you specified when you configured the cluster to archive log files\.

1. Navigate to the following folder, which contains the node provisioning log files:

   ```
   DOC-EXAMPLE-BUCKET/elasticmapreduce/<cluster id>/node/<instance id>/provision-node/
   ```

1. Open the `reports` folder and search for the node provisioning report for your reconfiguration\. The `reports` folder organizes logs by reconfiguration version number, universally unique identifier \(UUID\), Amazon EC2 instance IP address, and timestamp\. Each report is a compressed YAML file that contains detailed information about the reconfiguration process\.

   The following is an example report file name and path\.

   ```
   /reports/2/ca598xxx-cxxx-4xxx-bxxx-6dbxxxxxxxxx/ip-10-73-xxx-xxx.ec2.internal/202104061715.yaml.gz
   ```

1. To view a log file, you can download it from Amazon S3 to your local machine as a text file\. For instructions, see [Downloading an object](https://docs.aws.amazon.com/AmazonS3/latest/userguide/download-objects.html)\.

------

Each log file contains a detailed provisioning report for the associated reconfiguration\. To find error message information, you can search for the `err` log level of a report\. Report format depends on the version of Amazon EMR on your cluster\. 

The following example shows error information for Amazon EMR release versions earlier than 5\.32\.0 and 6\.2\.0\.

```
- !ruby/object:Puppet::Util::Log
      level: !ruby/sym err
      tags: 
        - err
      message: "Example detailed error message."
      source: Puppet
      time: 2021-01-01 00:00:00.000000 +00:00
```

Amazon EMR release versions 5\.32\.0 and 6\.2\.0 and later use the following format instead\.

```
- level: err
  message: 'Example detailed error message.'
  source: Puppet
  tags:
  - err
  time: '2021-01-01 00:00:00.000000 +00:00'
  file: 
  line:
```