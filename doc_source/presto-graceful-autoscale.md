# Using Presto automatic scaling with Graceful Decommission<a name="presto-graceful-autoscale"></a>

Amazon EMR release versions 5\.30\.0 and later include a feature you can use to set a grace period for certain scaling actions\. The grace period allows Presto tasks to keep running before the node terminates because of a scale\-in resize action or an automatic scaling policy request\. For more information about scaling rules, see [Understanding automatic scaling rules](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-automatic-scaling.html#emr-scaling-rules) in the *Amazon EMR Management Guide*\. Presto autoscaling with Graceful Decommission prevents new tasks from being scheduled on a node that is decommissioning, while at the same time allowing tasks that are already running to complete before the shut down timeout is reached\. Queries that are running will complete execution before the node is decommissioned\. Autoscaling is not supported on instance fleets\.

You can control how much time to allow for Presto tasks to complete after an autoscale shut down request is received\. By default, the shut down timeout for Amazon EMR is `0` minutes, which means that Amazon EMR immediately terminates the node and any Presto tasks running on it, if required by a scale\-in request\. To set a longer timeout for Presto tasks on Amazon EMR to allow running queries to complete before scaling down a cluster, use the `presto-config` configuration classification to set the `graceful-shutdown-timeout` parameter to a value in seconds or minutes greater than zero\. For more information, see [Configure applications](emr-configure-apps.md)\.

For example, increasing the `graceful-shutdown-timeout` value to `"30m"` specifies a timeout period of 30 minutes\. After the shut down timeout period ends, the node marked for decommissioning is forcefully terminated if it is waiting for query tasks to complete, and the query fails\. If the query tasks finish in five minutes, the node marked for decommissioning terminates at five minutes, provided other YARN applications have completed execution\.

**Example Presto autoscale configuration with Graceful Decommission**  
Replace the `graceful-shutdown-timeout` value with the number of minutes appropriate for your setup\. There's no maximum value\. The example below sets a timeout value of `1800` seconds \(30 minutes\)\.  

```
[
    {
        "classification": "presto-config",
        "properties": {
            "graceful-shutdown-timeout": "1800s"
        }
    }
]
```

**Limitations**

PrestoDB Graceful Decommission does not work on EMR clusters where HTTP connectivity is disabled, such as when `http-server.http.enabled` is set to `false`\. Trino does not support Graceful Decommission at all, regardless of the `http-server.http.enabled` setting\.