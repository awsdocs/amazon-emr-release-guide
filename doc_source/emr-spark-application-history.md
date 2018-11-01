# View Spark Application History<a name="emr-spark-application-history"></a>

Amazon EMR collects information from YARN applications on your cluster and keeps historical information for up to seven days after applications have completed\. Detailed information is available for Spark applications\. This feature enables you to view data that is otherwise available in the Spark History Server's web interface, but without having to establish a potentially complicated SSH tunnel for connecting to the cluster's master node\. You can also identify and open relevant log files more easily than you would by connecting to the master node and searching the file structure\.

**To view Spark application history**

1. From the **Clusters** list, select the **Name** of a cluster and then select **Application history**\.

   Each application is listed by **Application ID**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/app-history-app.png)

1. Expand a row to see basic diagnostic information for the application or select the **Application ID** to view additional details\.

For more information, see [View Application History](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-cluster-application-history.html) in the *Amazon EMR Management Guide*\.