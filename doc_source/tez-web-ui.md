# Tez web UI<a name="tez-web-ui"></a>

Tez has its own web user interface\. To view the web UI, see the following URL\.

```
http://masterDNS:8080/tez-ui
```

To enable the Hive Queries tab on the Tez web UI, set the following configuration\.

```
[
  {
    "Classification": "hive-site",
    "Properties": {
      "hive.exec.pre.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.post.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook",
      "hive.exec.failure.hooks": "org.apache.hadoop.hive.ql.hooks.ATSHook"
    }
  }
]
```

You can also view Tez, Spark, and YARN application UI details using links on the **Application user interfaces** tab of a cluster's detail page in the console\. Amazon EMR application user interfaces \(UI\) are hosted off\-cluster and are available after the cluster has terminated\. They don't require you to set up a SSH connection or web proxy, making it easier for you to troubleshoot and analyze active jobs and job history\.

For more information, see [View application history](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.