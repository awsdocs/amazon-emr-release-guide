# View HBase Log Files<a name="emr-hbase-log-files"></a>

As part of its operation, HBase writes log files with details about configuration settings, daemon actions, and exceptions\. These log files can be useful for debugging issues with HBase as well as for tracking performance\. 

If you configure your cluster to persist log files to Amazon S3, you should know that logs are written to Amazon S3 every five minutes, so there may be a slight delay before the latest log files are available\. 

**To view HBase logs on the master node**
+ You can view the current HBase logs by using SSH to connect to the master node, and navigating to the `/var/log/hbase` directory\. These logs are not available after the cluster is terminated unless you enable logging to Amazon S3 when the cluster is launched\.

**To view HBase logs on Amazon S3**
+ To access HBase logs and other cluster logs on Amazon S3, and to have them available after the cluster terminates, specify an Amazon S3 bucket to receive these logs when you create the cluster\. This is done using the `--log-uri` option\. For more information about enabling logging for your cluster, see [Configure Logging and Debugging \(Optional\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-debugging.html) in the *Amazon EMR Management Guide*\. 