# Supplying a Configuration for an Instance Group in a Running Cluster<a name="emr-configure-apps-running-cluster"></a>

With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\.

**Note**  
You cannot delete the initial cluster configurations that you specified when you created a cluster\. You can only override them\. In contrast, you can delete the configurations that you specified for each instance group\. Whenever you update configurations for each instance group, the new version of configurations are merged with the inherited cluster configurations, and become the active configurations for each instance group\. 

## Supplying a Configuration for an Instance Group in the Console<a name="emr-configure-apps-running-cluster-console"></a>

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. In the cluster list, choose the active cluster that you want to reconfigure under **Name**\.

1. Open the cluster details page for the cluster and go to **Configurations** tab\. 

1. In the **Filter** drop\-down list, select the instance group that you want to reconfigure\. 

1. In **Reconfigure** drop\-down menu, choose either **Edit in table**, or **Edit in JSON file**\.
   + **Edit in table** \-\- In the configuration classification table, edit the property and value for existing configurations, or choose **Add configuration** to supply property and value for additional configuration classifications\. 
   + **Edit in JSON file** \-\- You can enter the configuration directly in JSON, or by using shorthand syntax demonstrated in shadow text\. Otherwise, provide an Amazon S3 URI for a file with a JSON `Configurations` object\.
**Note**  
The **Source** column in the configuration classification table shows whether the configuration is supplied when you create a cluster, or when you specify additional configurations for this instance group\. You can edit the configurations for an instance group from both sources\. You cannot delete initial cluster configurations, but you can override them for an instance group\.   
You can also add or edit nested configuration classifications directly in the table\. For example, to supply an additional `export` sub\-classification of `hadoop-env`, add a `hadoop.export` configuration classification in the table\. Then, provide a specific property and value for this classification\. 

1. \(Optional\) Select **Apply this configuration to all active instance groups**\.

1. Save the changes\.

## Supplying a Configuration for an Instance Group Using the CLI<a name="emr-configure-apps-running-cluster-cli"></a>

You can use the modify\-instance\-groups command from the AWS CLI to specify configurations for each instance group in a running cluster\.

**Note**  
In the following examples, replace *j\-2AL4XXXXXX5T9* with your cluster ID and replace *ig\-1xxxxxxx9* with your instance group ID\.

**Example –Supplying a Configuration for an Instance Group**  
The following example demonstrates how to edit the property of the YARN NodeManager disk health checker for an instance group by referencing a configuration object in a JSON file\.  

1. Provide the following contents in instanceGroups\.json and save it in the same directory where you run the command: 

   ```
   [
      {
         "InstanceGroupId":"ig-1xxxxxxx9",
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

1. Run the following command:

   ```
   aws emr modify-instance-groups --cluster-id j-2AL4XXXXXX5T9 \
   --instance-groups file://instanceGroups.json
   ```

**Example –Supplying an Additional Configuration for an Instance Group**  
If you want to provide additional configurations for an instance group, you must also include the previously specified configurations for the instance group in your new `ModifyInstanceGroup` request\. Otherwise, the previously specified configurations for the instance group are removed\.  
The following example demonstrates how to edit the property for the YARN NodeManager virtual memory checker, in addition to the previously specified configuration for YARN NodeManager disk health checker\.  

1. Provide the following contents in instanceGroups\.json and save it in the same directory where you run the command:

   ```
   [
      {
         "InstanceGroupId":"ig-1xxxxxxx9",
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

1. Run the following command: 

   ```
   aws emr modify-instance-groups --cluster-id j-2AL4XXXXXX5T9 \
   --instance-groups file://instanceGroups.json
   ```

**Example – Deleting a Configuration for an Instance Group**  
To delete a previously specified configuration for an instance group, submit a new reconfiguration request that excludes the previous configuration\.   
You can only override initial cluster configuration\. You cannot delete it\.
For example, you can submit a new instanceGroups\.json with the following contents to delete the configuration for the YARN NodeManager disk health checker that was specified in the previous example\.   

```
[
   {
      "InstanceGroupId":"ig-1xxxxxxx9",
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
      "InstanceGroupId":"ig-1xxxxxxx9",
      "Configurations":[]
   }
]
```

**Example – Reconfiguring and Resizing an Instance Group in One Request**  
The following example JSON demonstrates how to reconfigure and resize an instance group in one request:   

```
[
   {
      "InstanceGroupId":"ig-1xxxxxxx9",
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

## Supplying a Configuration for an Instance Group Using the Java SDK<a name="emr-configure-apps-running-cluster-sdk"></a>

**Note**  
In the following examples, replace *j\-2AL4XXXXXX5T9* with your cluster ID and replace *ig\-1xxxxxxx9* with your instance group ID\.

The following program excerpt shows how to provide a new configuration for an instance group using the AWS SDK for Java:

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
    .withInstanceGroupId("ig-1xxxxxxx9")
    .withConfigurations(configuration);

ModifyInstanceGroupsRequest migRequest = new ModifyInstanceGroupsRequest()
    .withClusterId("j-2AL4XXXXXX5T9")
    .withInstanceGroups(igConfig);

emr.modifyInstanceGroups(migRequest);
```

Another program excerpt below shows how to delete a previously specified configuration for an instance group by supplying an empty array of configurations:

```
List<Configuration> configurations = new ArrayList<Configuration>();

InstanceGroupModifyConfig igConfig = new InstanceGroupModifyConfig()
    .withInstanceGroupId("ig-1xxxxxxx9")
    .withConfigurations(configurations);

ModifyInstanceGroupsRequest migRequest = new ModifyInstanceGroupsRequest()
    .withClusterId("j-2AL4XXXXXX5T9")
    .withInstanceGroups(igConfig);

emr.modifyInstanceGroups(migRequest);
```

## Considerations when Supplying Configurations for an Instance Group<a name="emr-configure-apps-running-cluster-considerations"></a>

When supplying configurations for instance groups in a running cluster, consider the following points: 
+ Amazon EMR currently doesn't support application reconfiguration requests in a cluster with multiple master nodes\.
+ Reconfiguring and resizing an instance group cannot occur at the same time\. If a reconfiguration is initiated while an instance group is resizing, reconfiguration cannot start until the instance group has completed resizing, and vice versa\. 
+ Amazon EMR follows a “rolling” process to reconfigure the instances in the Task and Core instance groups\. Only 10 percent of the instances in an instance group are modified and restarted at a time\. This process takes longer to finish but reduces the chance of potential application failure in a running cluster\. 
+ After reconfiguring an instance group, Amazon EMR restarts the applications to allow the new configurations to take effect\. Job failure or other unexpected application behavior might occur if the applications are in use during reconfiguration\. 
+ Amazon EMR assigns a version number for the new configuration specification after you submit a reconfiguration request for an instance group\. You can track the version number of configuration or the state of an instance group by viewing the CloudWatch events\. For more information, see [Monitor CloudWatch Events](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-manage-cloudwatch-events.html)\.
+ If a reconfiguration for an instance group fails, Amazon EMR reverses the configuration parameters to the previous working version\. If the reversion process fails too, you must submit a new `ModifyInstanceGroup` request to recover the instance group from the `ARRESTED` state\.
+ Reconfiguration request for any Phoenix configuration classifications is only supported in Amazon EMR version 5\.23\.0 and later, and is not supported in Amazon EMR version 5\.21\.0 or 5\.22\.0\. 
+ Amazon EMR currently doesn’t support certain reconfiguration requests for the capacity scheduler that requires restarting resource manager, such as completely removing a queue\.