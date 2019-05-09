# Configuring Tez<a name="tez-configure"></a>

You can customize Tez by setting values using the `tez-site` configuration classification, which configures settings in the `tez-site.xml` configuration file\. For more information, see [TezConfiguration](https://tez.apache.org/releases/0.8.2/tez-api-javadocs/configs/TezConfiguration.html) in the Apache Tez documentation\. To change Hive or Pig to use the Tez execution engine, use the `hive-site` and `pig-properties` configuration classifications as appropriate\. Examples are shown below\.

**Example Example: Customizing the Tez Root Logging Level and Setting Tez as the Execution Engine for Hive and Pig**  
The example `create-cluster` command shown below creates a cluster with Tez, Hive, and Pig installed\. The command references a file stored in Amazon S3, `myConfig.json`, which specifies properties for the `tez-site` classification that sets `tez.am.log.level` to `DEBUG`, and sets the execution engine to Tez for Hive and Pig using the `hive-site` and `pig-properties` configuration classifications\.  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --release-label emr-5.23.0 \
--applications Name=Tez Name=Hive Name=Pig --ec2-attributes KeyName=myKey \
--instance-type m4.large --instance-count 3 \
--configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json --use-default-roles
```
Example contents of `myConfig.json` are shown below\.  

```
[
    {
      "Classification": "tez-site",
      "Properties": {
        "tez.am.log.level": "DEBUG"
      }
    },
    {
      "Classification": "hive-site",
      "Properties": {
        "hive.execution.engine": "tez"
      }
    },
    {
      "Classification": "pig-properties",
      "Properties": {
        "exectype": "tez"
      }
    }
  ]
```

**Note**  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.