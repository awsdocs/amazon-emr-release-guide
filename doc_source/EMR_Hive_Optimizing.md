# Optimizing Performance for Amazon EMR Operations in DynamoDB<a name="EMR_Hive_Optimizing"></a>

 Amazon EMR operations on a DynamoDB table count as read operations, and are subject to the table's provisioned throughput settings\. Amazon EMR implements its own logic to try to balance the load on your DynamoDB table to minimize the possibility of exceeding your provisioned throughput\. At the end of each Hive query, Amazon EMR returns information about the cluster used to process the query, including how many times your provisioned throughput was exceeded\. You can use this information, as well as CloudWatch metrics about your DynamoDB throughput, to better manage the load on your DynamoDB table in subsequent requests\. 

 The following factors influence Hive query performance when working with DynamoDB tables\. 

## Provisioned Read Capacity Units<a name="ProvisionedReadCapacityUnits"></a>

 When you run Hive queries against a DynamoDB table, you need to ensure that you have provisioned a sufficient amount of read capacity units\. 

 For example, suppose that you have provisioned 100 units of Read Capacity for your DynamoDB table\. This will let you perform 100 reads, or 409,600 bytes, per second\. If that table contains 20GB of data \(21,474,836,480 bytes\), and your Hive query performs a full table scan, you can estimate how long the query will take to run: 

 * 21,474,836,480 / 409,600 = 52,429 seconds = 14\.56 hours * 

 The only way to decrease the time required would be to adjust the read capacity units on the source DynamoDB table\. Adding more nodes to the Amazon EMR cluster will not help\. 

 In the Hive output, the completion percentage is updated when one or more mapper processes are finished\. For a large DynamoDB table with a low provisioned Read Capacity setting, the completion percentage output might not be updated for a long time; in the case above, the job will appear to be 0% complete for several hours\. For more detailed status on your job's progress, go to the Amazon EMR console; you will be able to view the individual mapper task status, and statistics for data reads\. 

 You can also log on to Hadoop interface on the master node and see the Hadoop statistics\. This shows you the individual map task status and some data read statistics\. For more information, see [Web Interfaces Hosted on the Master Node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html) in the *Amazon EMR Management Guide*\.

## Read Percent Setting<a name="ReadPercent"></a>

 By default, Amazon EMR manages the request load against your DynamoDB table according to your current provisioned throughput\. However, when Amazon EMR returns information about your job that includes a high number of provisioned throughput exceeded responses, you can adjust the default read rate using the `dynamodb.throughput.read.percent` parameter when you set up the Hive table\. For more information about setting the read percent parameter, see [Hive Options](EMR_Interactive_Hive.md#EMR_Hive_Options)\. 

## Write Percent Setting<a name="WritePercent"></a>

 By default, Amazon EMR manages the request load against your DynamoDB table according to your current provisioned throughput\. However, when Amazon EMR returns information about your job that includes a high number of provisioned throughput exceeded responses, you can adjust the default write rate using the `dynamodb.throughput.write.percent` parameter when you set up the Hive table\. For more information about setting the write percent parameter, see [Hive Options](EMR_Interactive_Hive.md#EMR_Hive_Options)\. 

## Retry Duration Setting<a name="emr-ddb-retry-duration"></a>

 By default, Amazon EMR re\-runs a Hive query if it has not returned a result within two minutes, the default retry interval\. You can adjust this interval by setting the `dynamodb.retry.duration` parameter when you run a Hive query\. For more information about setting the write percent parameter, see [Hive Options](EMR_Interactive_Hive.md#EMR_Hive_Options)\. 

## Number of Map Tasks<a name="NumberMapTasks"></a>

 The mapper daemons that Hadoop launches to process your requests to export and query data stored in DynamoDB are capped at a maximum read rate of 1 MiB per second to limit the read capacity used\. If you have additional provisioned throughput available on DynamoDB, you can improve the performance of Hive export and query operations by increasing the number of mapper daemons\. To do this, you can either increase the number of EC2 instances in your cluster *or* increase the number of mapper daemons running on each EC2 instance\. 

 You can increase the number of EC2 instances in a cluster by stopping the current cluster and re\-launching it with a larger number of EC2 instances\. You specify the number of EC2 instances in the **Configure EC2 Instances** dialog box if you're launching the cluster from the Amazon EMR console, or with the `--num-instances` option if you're launching the cluster from the CLI\. 

 The number of map tasks run on an instance depends on the EC2 instance type\. For more information about the supported EC2 instance types and the number of mappers each one provides, see [Task Configuration](emr-hadoop-task-config.md)\. There, you will find a "Task Configuration" section for each of the supported configurations\. 

 Another way to increase the number of mapper daemons is to change the `mapreduce.tasktracker.map.tasks.maximum` configuration parameter of Hadoop to a higher value\. This has the advantage of giving you more mappers without increasing either the number or the size of EC2 instances, which saves you money\. A disadvantage is that setting this value too high can cause the EC2 instances in your cluster to run out of memory\. To set `mapreduce.tasktracker.map.tasks.maximum`, launch the cluster and specify a value for `mapreduce.tasktracker.map.tasks.maximum` as a property of the mapred\-site configuration classification\. This is shown in the following example\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

```
{
    "configurations": [
    {
        "classification": "mapred-site",
        "properties": {
            "mapred.tasktracker.map.tasks.maximum": "10"
        }
    }
    ]
}
```

## Parallel Data Requests<a name="ParallelDataRequests"></a>

 Multiple data requests, either from more than one user or more than one application to a single table may drain read provisioned throughput and slow performance\. 

## Process Duration<a name="ProcessDuration"></a>

 Data consistency in DynamoDB depends on the order of read and write operations on each node\. While a Hive query is in progress, another application might load new data into the DynamoDB table or modify or delete existing data\. In this case, the results of the Hive query might not reflect changes made to the data while the query was running\. 

## Avoid Exceeding Throughput<a name="AvoidExceedingThroughput"></a>

 When running Hive queries against DynamoDB, take care not to exceed your provisioned throughput, because this will deplete capacity needed for your application's calls to `DynamoDB::Get`\. To ensure that this is not occurring, you should regularly monitor the read volume and throttling on application calls to `DynamoDB::Get` by checking logs and monitoring metrics in Amazon CloudWatch\. 

## Request Time<a name="RequestTime"></a>

 Scheduling Hive queries that access a DynamoDB table when there is lower demand on the DynamoDB table improves performance\. For example, if most of your application's users live in San Francisco, you might choose to export daily data at 4 a\.m\. PST, when the majority of users are asleep, and not updating records in your DynamoDB database\. 

## Time\-Based Tables<a name="TimeBasedTables"></a>

 If the data is organized as a series of time\-based DynamoDB tables, such as one table per day, you can export the data when the table becomes no longer active\. You can use this technique to back up data to Amazon S3 on an ongoing fashion\. 

## Archived Data<a name="ArchivedData"></a>

 If you plan to run many Hive queries against the data stored in DynamoDB and your application can tolerate archived data, you may want to export the data to HDFS or Amazon S3 and run the Hive queries against a copy of the data instead of DynamoDB\. This conserves your read operations and provisioned throughput\. 