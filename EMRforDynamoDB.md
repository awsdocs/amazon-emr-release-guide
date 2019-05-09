# Export, Import, Query, and Join Tables in DynamoDB Using Amazon EMR<a name="EMRforDynamoDB"></a>

**Note**  
The Amazon EMR\-DynamoDB Connector is open\-sourced on GitHub\. For more information, see [https://github\.com/awslabs/emr\-dynamodb\-connector](https://github.com/awslabs/emr-dynamodb-connector)\.

DynamoDB is a fully managed NoSQL database service that provides fast and predictable performance with seamless scalability\. Developers can create a database table and grow its request traffic or storage without limit\. DynamoDB automatically spreads the data and traffic for the table over a sufficient number of servers to handle the request capacity specified by the customer and the amount of data stored, while maintaining consistent, fast performance\. Using Amazon EMR and Hive you can quickly and efficiently process large amounts of data, such as data stored in DynamoDB\. For more information about DynamoDB go to the [DynamoDB Developer Guide](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Introduction.html)\. 

Apache Hive is a software layer that you can use to query map reduce clusters using a simplified, SQL\-like query language called HiveQL\. It runs on top of the Hadoop architecture\. For more information about Hive and HiveQL, go to the [HiveQL Language Manual](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)\. For more information about Hive and Amazon EMR, see [Apache Hive](emr-hive.md) \.

 You can use Amazon EMR with a customized version of Hive that includes connectivity to DynamoDB to perform operations on data stored in DynamoDB:
+ Loading DynamoDB data into the Hadoop Distributed File System \(HDFS\) and using it as input into an Amazon EMR cluster\.
+ Querying live DynamoDB data using SQL\-like statements \(HiveQL\)\.
+ Joining data stored in DynamoDB and exporting it or querying against the joined data\.
+ Exporting data stored in DynamoDB to Amazon S3\.
+ Importing data stored in Amazon S3 to DynamoDB\.

**Note**  
The Amazon EMR\-DynamoDB Connector does not support clusters configured to use [Kerberos authentication](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-kerberos.html)\.

 To perform each of the following tasks, you'll launch an Amazon EMR cluster, specify the location of the data in DynamoDB, and issue Hive commands to manipulate the data in DynamoDB\. 

There are several ways to launch an Amazon EMR cluster: you can use the Amazon EMR console, the command line interface \(CLI\), or you can program your cluster using an AWS SDK or the Amazon EMR API\. You can also choose whether to run a Hive cluster interactively or from a script\. In this section, we will show you how to launch an interactive Hive cluster from the Amazon EMR console and the CLI\. 

 Using Hive interactively is a great way to test query performance and tune your application\. After you have established a set of Hive commands that will run on a regular basis, consider creating a Hive script that Amazon EMR can run for you\. 

**Warning**  
 Amazon EMR read or write operations on an DynamoDB table count against your established provisioned throughput, potentially increasing the frequency of provisioned throughput exceptions\. For large requests, Amazon EMR implements retries with exponential backoff to manage the request load on the DynamoDB table\. Running Amazon EMR jobs concurrently with other traffic may cause you to exceed the allocated provisioned throughput level\. You can monitor this by checking the **ThrottleRequests** metric in Amazon CloudWatch\. If the request load is too high, you can relaunch the cluster and set the [Read Percent Setting](EMR_Hive_Optimizing.md#ReadPercent) or [Write Percent Setting](EMR_Hive_Optimizing.md#WritePercent) to a lower value to throttle the Amazon EMR operations\. For information about DynamoDB throughput settings, see [Provisioned Throughput](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/WorkingWithDDTables.html#ProvisionedThroughput)\. 

**Topics**
+ [Set Up a Hive Table to Run Hive Commands](EMR_Interactive_Hive.md)
+ [Hive Command Examples for Exporting, Importing, and Querying Data in DynamoDB](EMR_Hive_Commands.md)
+ [Optimizing Performance for Amazon EMR Operations in DynamoDB](EMR_Hive_Optimizing.md)