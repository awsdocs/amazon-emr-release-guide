# Set Up a Hive Table to Run Hive Commands<a name="EMR_Interactive_Hive"></a>

Apache Hive is a data warehouse application you can use to query data contained in Amazon EMR clusters using a SQL\-like language\. For more information about Hive, see [http://hive\.apache\.org/](http://hive.apache.org/)\.

The following procedure assumes you have already created a cluster and specified an Amazon EC2 key pair\. To learn how to get started creating clusters, see [Step 3: Launch an Amazon EMR Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/gsg-launch-cluster.html) in the *Amazon EMR Management Guide*\.

## Configure Hive to Use MapReduce<a name="w40aac67b7c25b7"></a>

When use Hive on Amazon EMR to query DynamoDB tables, errors can occur if Hive is using the default execution engine, Tez\. For this reason, when you create a cluster with Hive that integrates with DynamoDB as described in this section, we recommend that you use a configuration classification that sets Hive to use MapReduce\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

The following snippet shows the configuration classification and property to use to set MapReduce as the execution engine for Hive:

```
[
                {
                    "Classification": "hive-site",
                    "Properties": {
                        "hive.execution.engine": "mr"
                    }
                }
             ]
```<a name="EMR_Interactive_Hive_session"></a>

**To run Hive commands interactively**

1. Connect to the master node\. For more information, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. At the command prompt for the current master node, type `hive`\.

   You should see a hive prompt: `hive>`

1.  Enter a Hive command that maps a table in the Hive application to the data in DynamoDB\. This table acts as a reference to the data stored in Amazon DynamoDB; the data is not stored locally in Hive and any queries using this table run against the live data in DynamoDB, consuming the table’s read or write capacity every time a command is run\. If you expect to run multiple Hive commands against the same dataset, consider exporting it first\. 

    The following shows the syntax for mapping a Hive table to a DynamoDB table\. 

   ```
   CREATE EXTERNAL TABLE hive_tablename (hive_column1_name column1_datatype, hive_column2_name column2_datatype...)
   STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   TBLPROPERTIES ("dynamodb.table.name" = "dynamodb_tablename", 
   "dynamodb.column.mapping" = "hive_column1_name:dynamodb_attribute1_name,hive_column2_name:dynamodb_attribute2_name...");
   ```

    When you create a table in Hive from DynamoDB, you must create it as an external table using the keyword `EXTERNAL`\. The difference between external and internal tables is that the data in internal tables is deleted when an internal table is dropped\. This is not the desired behavior when connected to Amazon DynamoDB, and thus only external tables are supported\. 

    For example, the following Hive command creates a table named *hivetable1* in Hive that references the DynamoDB table named *dynamodbtable1*\. The DynamoDB table *dynamodbtable1* has a hash\-and\-range primary key schema\. The hash key element is `name` \(string type\), the range key element is `year` \(numeric type\), and each item has an attribute value for `holidays` \(string set type\)\. 

   ```
   CREATE EXTERNAL TABLE hivetable1 (col1 string, col2 bigint, col3 array<string>)
   STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
   "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");
   ```

    Line 1 uses the HiveQL `CREATE EXTERNAL TABLE` statement\. For *hivetable1*, you need to establish a column for each attribute name\-value pair in the DynamoDB table, and provide the data type\. These values are not case\-sensitive, and you can give the columns any name \(except reserved words\)\. 

    Line 2 uses the `STORED BY` statement\. The value of `STORED BY` is the name of the class that handles the connection between Hive and DynamoDB\. It should be set to `'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'`\. 

    Line 3 uses the `TBLPROPERTIES` statement to associate "hivetable1" with the correct table and schema in DynamoDB\. Provide `TBLPROPERTIES` with values for the `dynamodb.table.name` parameter and `dynamodb.column.mapping` parameter\. These values *are* case\-sensitive\.
**Note**  
 All DynamoDB attribute names for the table must have corresponding columns in the Hive table\. Depending on your Amazon EMR version, the following scenarios occur if the one\-to\-one mapping does not exist:  
On Amazon EMR version 5\.27\.0 and later, the connector has validations that ensure a one\-to\-one mapping between DynamoDB attribute names and columns in the Hive table\. An error will occur if the one\-to\-one mapping does not exist\.
On Amazon EMR version 5\.26\.0 and earlier, the Hive table won't contain the name\-value pair from DynamoDB\. If you do not map the DynamoDB primary key attributes, Hive generates an error\. If you do not map a non\-primary key attribute, no error is generated, but you won't see the data in the Hive table\. If the data types do not match, the value is null\. 

Then you can start running Hive operations on *hivetable1*\. Queries run against *hivetable1* are internally run against the DynamoDB table *dynamodbtable1* of your DynamoDB account, consuming read or write units with each execution\.

When you run Hive queries against a DynamoDB table, you need to ensure that you have provisioned a sufficient amount of read capacity units\.

For example, suppose that you have provisioned 100 units of read capacity for your DynamoDB table\. This will let you perform 100 reads, or 409,600 bytes, per second\. If that table contains 20GB of data \(21,474,836,480 bytes\), and your Hive query performs a full table scan, you can estimate how long the query will take to run:

 * 21,474,836,480 / 409,600 = 52,429 seconds = 14\.56 hours * 

The only way to decrease the time required would be to adjust the read capacity units on the source DynamoDB table\. Adding more Amazon EMR nodes will not help\.

In the Hive output, the completion percentage is updated when one or more mapper processes are finished\. For a large DynamoDB table with a low provisioned read capacity setting, the completion percentage output might not be updated for a long time; in the case above, the job will appear to be 0% complete for several hours\. For more detailed status on your job's progress, go to the Amazon EMR console; you will be able to view the individual mapper task status, and statistics for data reads\. You can also log on to Hadoop interface on the master node and see the Hadoop statistics\. This will show you the individual map task status and some data read statistics\. For more information, see the following topics:
+ [Web Interfaces Hosted on the Master Node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html)
+ [View the Hadoop Web Interfaces](https://docs.aws.amazon.com/emr/latest/ManagementGuide/UsingtheHadoopUserInterface.html)

For more information about sample HiveQL statements to perform tasks such as exporting or importing data from DynamoDB and joining tables, see [Hive Command Examples for Exporting, Importing, and Querying Data in DynamoDB](EMR_Hive_Commands.md)\.<a name="EMR_Hive_Cancel"></a>

**To cancel a Hive request**

When you execute a Hive query, the initial response from the server includes the command to cancel the request\. To cancel the request at any time in the process, use the **Kill Command** from the server response\.

1. Enter `Ctrl+C` to exit the command line client\.

1.  At the shell prompt, enter the **Kill Command** from the initial server response to your request\. 

    Alternatively, you can run the following command from the command line of the master node to kill the Hadoop job, where *job\-id* is the identifier of the Hadoop job and can be retrieved from the Hadoop user interface\.

   ```
   hadoop job -kill job-id
   ```

## Data Types for Hive and DynamoDB<a name="EMR_Hive_Properties"></a>

The following table shows the available Hive data types, the default DynamoDB type that they correspond to, and the alternate DynamoDB types that they can also map to\. 


| Hive type | Default DynamoDB type | Alternate DynamoDB type\(s\) | 
| --- | --- | --- | 
| string | string \(S\) |  | 
| bigint or double | number \(N\) |  | 
| binary | binary \(B\) |  | 
| boolean | boolean \(BOOL\) |  | 
| array | list \(L\) | number set \(NS\), string set \(SS\), or binary set \(BS\) | 
| map<string,string> | item | map \(M\) | 
| map<string,?> | map \(M\) |  | 
|  | null \(NULL\) |  | 

If you want to write your Hive data as a corresponding alternate DynamoDB type, or if your DynamoDB data contains attribute values of an alternate DynamoDB type, you can specify the column and the DynamoDB type with the `dynamodb.type.mapping` parameter\. The following example shows the syntax for specifying an alternate type mapping\.

```
CREATE EXTERNAL TABLE hive_tablename (hive_column1_name column1_datatype, hive_column2_name column2_datatype...)
STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
TBLPROPERTIES ("dynamodb.table.name" = "dynamodb_tablename",
"dynamodb.column.mapping" = "hive_column1_name:dynamodb_attribute1_name,hive_column2_name:dynamodb_attribute2_name...",
"dynamodb.type.mapping" = "hive_column1_name:dynamodb_attribute1_datatype");
```

The type mapping parameter is optional, and only has to be specified for the columns that use alternate types\.

For example, the following Hive command creates a table named `hivetable2` that references the DynamoDB table `dynamodbtable2`\. It is similar to `hivetable1`, except that it maps the `col3` column to the string set \(SS\) type\. 

```
CREATE EXTERNAL TABLE hivetable2 (col1 string, col2 bigint, col3 array<string>)
STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable2",
"dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays",
"dynamodb.type.mapping" = "col3:SS");
```

In Hive, `hivetable1` and `hivetable2` are identical\. However, when data from those tables are written to their corresponding DynamoDB tables, `dynamodbtable1` will contain lists, while `dynamodbtable2` will contain string sets\.

If you want to write Hive `null` values as attributes of DynamoDB `null` type, you can do so with the `dynamodb.null.serialization` parameter\. The following example shows the syntax for specifying `null` serialization\.

```
CREATE EXTERNAL TABLE hive_tablename (hive_column1_name column1_datatype, hive_column2_name column2_datatype...)
STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
TBLPROPERTIES ("dynamodb.table.name" = "dynamodb_tablename",
"dynamodb.column.mapping" = "hive_column1_name:dynamodb_attribute1_name,hive_column2_name:dynamodb_attribute2_name...",
"dynamodb.null.serialization" = "true");
```

The null serialization parameter is optional, and is set to `false` if not specified\. Note that DynamoDB `null` attributes are read as `null` values in Hive regardless of the parameter setting\. Hive collections with `null` values can be written to DynamoDB only if the null serialization parameter is specified as `true`\. Otherwise, a Hive error occurs\.

The bigint type in Hive is the same as the Java long type, and the Hive double type is the same as the Java double type in terms of precision\. This means that if you have numeric data stored in DynamoDB that has precision higher than is available in the Hive datatypes, using Hive to export, import, or reference the DynamoDB data could lead to a loss in precision or a failure of the Hive query\. 

 Exports of the binary type from DynamoDB to Amazon Simple Storage Service \(Amazon S3\) or HDFS are stored as a Base64\-encoded string\. If you are importing data from Amazon S3 or HDFS into the DynamoDB binary type, it should be encoded as a Base64 string\. 

## Hive Options<a name="EMR_Hive_Options"></a>

 You can set the following Hive options to manage the transfer of data out of Amazon DynamoDB\. These options only persist for the current Hive session\. If you close the Hive command prompt and reopen it later on the cluster, these settings will have returned to the default values\. 


| Hive Options | Description | 
| --- | --- | 
| dynamodb\.throughput\.read\.percent |   Set the rate of read operations to keep your DynamoDB provisioned throughput rate in the allocated range for your table\. The value is between `0.1` and `1.5`, inclusively\.   The value of 0\.5 is the default read rate, which means that Hive will attempt to consume half of the read provisioned throughout resources in the table\. Increasing this value above 0\.5 increases the read request rate\. Decreasing it below 0\.5 decreases the read request rate\. This read rate is approximate\. The actual read rate will depend on factors such as whether there is a uniform distribution of keys in DynamoDB\.   If you find your provisioned throughput is frequently exceeded by the Hive operation, or if live read traffic is being throttled too much, then reduce this value below `0.5`\. If you have enough capacity and want a faster Hive operation, set this value above `0.5`\. You can also oversubscribe by setting it up to 1\.5 if you believe there are unused input/output operations available\.   | 
| dynamodb\.throughput\.write\.percent |   Set the rate of write operations to keep your DynamoDB provisioned throughput rate in the allocated range for your table\. The value is between `0.1` and `1.5`, inclusively\.   The value of 0\.5 is the default write rate, which means that Hive will attempt to consume half of the write provisioned throughout resources in the table\. Increasing this value above 0\.5 increases the write request rate\. Decreasing it below 0\.5 decreases the write request rate\. This write rate is approximate\. The actual write rate will depend on factors such as whether there is a uniform distribution of keys in DynamoDB   If you find your provisioned throughput is frequently exceeded by the Hive operation, or if live write traffic is being throttled too much, then reduce this value below `0.5`\. If you have enough capacity and want a faster Hive operation, set this value above `0.5`\. You can also oversubscribe by setting it up to 1\.5 if you believe there are unused input/output operations available or this is the initial data upload to the table and there is no live traffic yet\.   | 
| dynamodb\.endpoint | Specify the endpoint for the DynamoDB service\. For more information about the available DynamoDB endpoints, see [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#ddb_region)\.  | 
| dynamodb\.max\.map\.tasks |   Specify the maximum number of map tasks when reading data from DynamoDB\. This value must be equal to or greater than 1\.   | 
| dynamodb\.retry\.duration |   Specify the number of minutes to use as the timeout duration for retrying Hive commands\. This value must be an integer equal to or greater than 0\. The default timeout duration is two minutes\.   | 

 These options are set using the `SET` command as shown in the following example\. 

```
SET dynamodb.throughput.read.percent=1.0; 

INSERT OVERWRITE TABLE s3_export SELECT * 
FROM hiveTableName;
```