# Kinesis<a name="emr-kinesis"></a>

Amazon EMR clusters can read and process Amazon Kinesis streams directly, using familiar tools in the Hadoop ecosystem such as Hive, Pig, MapReduce, the Hadoop Streaming API, and Cascading\. You can also join real\-time data from Amazon Kinesis with existing data on Amazon S3, Amazon DynamoDB, and HDFS in a running cluster\. You can directly load the data from Amazon EMR to Amazon S3 or DynamoDB for post\-processing activities\. For information about Amazon Kinesis service highlights and pricing, see [Amazon Kinesis](https://aws.amazon.com//kinesis/)\.

## What Can I Do With Amazon EMR and Amazon Kinesis Integration?<a name="kinesis-use-cases"></a>

 Integration between Amazon EMR and Amazon Kinesis makes certain scenarios much easier; for example: 
+ **Streaming log analysis**–You can analyze streaming web logs to generate a list of top 10 error types every few minutes by region, browser, and access domain\. 
+ **Customer engagement**–You can write queries that join clickstream data from Amazon Kinesis with advertising campaign information stored in a DynamoDB table to identify the most effective categories of ads that are displayed on particular websites\. 
+ **Ad\-hoc interactive queries**–You can periodically load data from Amazon Kinesis streams into HDFS and make it available as a local Impala table for fast, interactive, analytic queries\.

## Checkpointed Analysis of Amazon Kinesis Streams<a name="kinesis-checkpoint"></a>

Users can run periodic, batched analysis of Amazon Kinesis streams in what are called *iterations*\. Because Amazon Kinesis stream data records are retrieved by using a sequence number, iteration boundaries are defined by starting and ending sequence numbers that Amazon EMR stores in a DynamoDB table\. For example, when `iteration0` ends, it stores the ending sequence number in DynamoDB so that when the `iteration1` job begins, it can retrieve subsequent data from the stream\. This mapping of iterations in stream data is called *checkpointing*\. For more information, see [Kinesis Connector](https://aws.amazon.com//elasticmapreduce/faqs/#kinesis-connector)\.

If an iteration was checkpointed and the job failed processing an iteration, Amazon EMR attempts to reprocess the records in that iteration, provided that the data records have not reached the 24\-hour limit for Amazon Kinesis streams\. 

Checkpointing is a feature that allows you to: 
+ Start data processing after a sequence number processed by a previous query that ran on same stream and logical name
+ Re\-process the same batch of data from Kinesis that was processed by an earlier query

 To enable checkpointing, set the `kinesis.checkpoint.enabled` parameter to `true` in your scripts\. Also, configure the following parameters:


| Configuration Setting | Description | 
| --- | --- | 
| kinesis\.checkpoint\.metastore\.table\.name | DynamoDB table name where checkpoint information will be stored | 
| kinesis\.checkpoint\.metastore\.hash\.key\.name | Hash key name for the DynamoDB table | 
| kinesis\.checkpoint\.metastore\.hash\.range\.name | Range key name for the DynamoDB table | 
| kinesis\.checkpoint\.logical\.name | A logical name for current processing | 
| kinesis\.checkpoint\.iteration\.no | Iteration number for processing associated with the logical name | 
| kinesis\.rerun\.iteration\.without\.wait | Boolean value that indicates if a failed iteration can be rerun without waiting for timeout; the default is false | 

### Provisioned IOPS Recommendations for Amazon DynamoDB Tables<a name="kinesis-checkpoint-DDB"></a>

The Amazon EMR connector for Amazon Kinesis uses the DynamoDB database as its backing for checkpointing metadata\. You must create a table in DynamoDB before consuming data in an Amazon Kinesis stream with an Amazon EMR cluster in checkpointed intervals\. The table must be in the same region as your Amazon EMR cluster\. The following are general recommendations for the number of IOPS you should provision for your DynamoDB tables; let `j` be the maximum number of Hadoop jobs \(with different logical name\+iteration number combination\) that can run concurrently and `s` be the maximum number of shards that any job will process:

For **Read Capacity Units**: `j`\*`s`/`5`

For **Write Capacity Units**: `j`\*`s`

## Performance Considerations<a name="w3aac63b9b8"></a>

Amazon Kinesis shard throughput is directly proportional to the instance size of nodes in Amazon EMR clusters and record size in the stream\. We recommend that you use m4\.large or larger instances on master and core nodes\.

## Schedule Amazon Kinesis Analysis with Amazon EMR<a name="w3aac63b9c10"></a>

 When you are analyzing data on an active Amazon Kinesis stream, limited by timeouts and a maximum duration for any iteration, it is important that you run the analysis frequently to gather periodic details from the stream\. There are multiple ways to execute such scripts and queries at periodic intervals; we recommend using AWS Data Pipeline for recurrent tasks like these\. For more information, see [AWS Data Pipeline PigActivity](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-object-pigactivity.html) and [AWS Data Pipeline HiveActivity](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-object-hiveactivity.html) in the *AWS Data Pipeline Developer Guide*\.