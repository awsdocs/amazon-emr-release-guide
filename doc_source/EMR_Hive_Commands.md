# Hive Command Examples for Exporting, Importing, and Querying Data in DynamoDB<a name="EMR_Hive_Commands"></a>

The following examples use Hive commands to perform operations such as exporting data to Amazon S3 or HDFS, importing data to DynamoDB, joining tables, querying tables, and more\. 

Operations on a Hive table reference data stored in DynamoDB\. Hive commands are subject to the DynamoDB table's provisioned throughput settings, and the data retrieved includes the data written to the DynamoDB table at the time the Hive operation request is processed by DynamoDB\. If the data retrieval process takes a long time, some data returned by the Hive command may have been updated in DynamoDB since the Hive command began\. 

Hive commands `DROP TABLE` and `CREATE TABLE` only act on the local tables in Hive and do not create or drop tables in DynamoDB\. If your Hive query references a table in DynamoDB, that table must already exist before you run the query\. For more information about creating and deleting tables in DynamoDB, see [Working with Tables in DynamoDB](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide//WorkingWithTables.html) in the *Amazon DynamoDB Developer Guide*\. 

**Note**  
 When you map a Hive table to a location in Amazon S3, do not map it to the root path of the bucket, s3://mybucket, as this may cause errors when Hive writes the data to Amazon S3\. Instead map the table to a subpath of the bucket, s3://mybucket/mypath\. 

## Exporting Data from DynamoDB<a name="EMR_Hive_Commands_exporting"></a>

 You can use Hive to export data from DynamoDB\. 

**To export a DynamoDB table to an Amazon S3 bucket**
+  Create a Hive table that references data stored in DynamoDB\. Then you can call the INSERT OVERWRITE command to write the data to an external directory\. In the following example, *s3://bucketname/path/subpath/* is a valid path in Amazon S3\. Adjust the columns and datatypes in the CREATE command to match the values in your DynamoDB\. You can use this to create an archive of your DynamoDB data in Amazon S3\. 

  ```
  1. CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
  2. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
  3. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
  4. "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");                   
  5.                     
  6. INSERT OVERWRITE DIRECTORY 's3://bucketname/path/subpath/' SELECT * 
  7. FROM hiveTableName;
  ```

**To export a DynamoDB table to an Amazon S3 bucket using formatting**
+  Create an external table that references a location in Amazon S3\. This is shown below as s3\_export\. During the CREATE call, specify row formatting for the table\. Then, when you use INSERT OVERWRITE to export data from DynamoDB to s3\_export, the data is written out in the specified format\. In the following example, the data is written out as comma\-separated values \(CSV\)\. 

  ```
   1. CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
   2. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   3. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
   4. "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");                      
   5.                     
   6. CREATE EXTERNAL TABLE s3_export(a_col string, b_col bigint, c_col array<string>)
   7. ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
   8. LOCATION 's3://bucketname/path/subpath/';
   9.                     
  10. INSERT OVERWRITE TABLE s3_export SELECT * 
  11. FROM hiveTableName;
  ```

**To export a DynamoDB table to an Amazon S3 bucket without specifying a column mapping**
+  Create a Hive table that references data stored in DynamoDB\. This is similar to the preceding example, except that you are not specifying a column mapping\. The table must have exactly one column of type `map<string, string>`\. If you then create an `EXTERNAL` table in Amazon S3 you can call the `INSERT OVERWRITE` command to write the data from DynamoDB to Amazon S3\. You can use this to create an archive of your DynamoDB data in Amazon S3\. Because there is no column mapping, you cannot query tables that are exported this way\. Exporting data without specifying a column mapping is available in Hive 0\.8\.1\.5 or later, which is supported on Amazon EMR AMI 2\.2\.*x* and later\. 

  ```
   1. CREATE EXTERNAL TABLE hiveTableName (item map<string,string>)
   2. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   3. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1");  
   4.     
   5. CREATE EXTERNAL TABLE s3TableName (item map<string, string>)
   6. ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' LINES TERMINATED BY '\n'
   7. LOCATION 's3://bucketname/path/subpath/'; 
   8.                 
   9. INSERT OVERWRITE TABLE s3TableName SELECT * 
  10. FROM hiveTableName;
  ```

**To export a DynamoDB table to an Amazon S3 bucket using data compression**
+  Hive provides several compression codecs you can set during your Hive session\. Doing so causes the exported data to be compressed in the specified format\. The following example compresses the exported files using the Lempel\-Ziv\-Oberhumer \(LZO\) algorithm\. 

  ```
   1. SET hive.exec.compress.output=true;
   2. SET io.seqfile.compression.type=BLOCK;
   3. SET mapred.output.compression.codec = com.hadoop.compression.lzo.LzopCodec;                    
   4.                     
   5. CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
   6. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   7. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
   8. "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");                    
   9.                     
  10. CREATE EXTERNAL TABLE lzo_compression_table (line STRING)
  11. ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' LINES TERMINATED BY '\n'
  12. LOCATION 's3://bucketname/path/subpath/';
  13.                     
  14. INSERT OVERWRITE TABLE lzo_compression_table SELECT * 
  15. FROM hiveTableName;
  ```

   The available compression codecs are: 
  +  org\.apache\.hadoop\.io\.compress\.GzipCodec 
  +  org\.apache\.hadoop\.io\.compress\.DefaultCodec 
  +  com\.hadoop\.compression\.lzo\.LzoCodec 
  +  com\.hadoop\.compression\.lzo\.LzopCodec 
  +  org\.apache\.hadoop\.io\.compress\.BZip2Codec 
  +  org\.apache\.hadoop\.io\.compress\.SnappyCodec 

**To export a DynamoDB table to HDFS**
+  Use the following Hive command, where *hdfs:///directoryName* is a valid HDFS path and *hiveTableName* is a table in Hive that references DynamoDB\. This export operation is faster than exporting a DynamoDB table to Amazon S3 because Hive 0\.7\.1\.1 uses HDFS as an intermediate step when exporting data to Amazon S3\. The following example also shows how to set `dynamodb.throughput.read.percent` to 1\.0 in order to increase the read request rate\. 

  ```
  1. CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
  2. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
  3. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
  4. "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays"); 
  5.                     
  6. SET dynamodb.throughput.read.percent=1.0;                    
  7.                     
  8. INSERT OVERWRITE DIRECTORY 'hdfs:///directoryName' SELECT * FROM hiveTableName;
  ```

   You can also export data to HDFS using formatting and compression as shown above for the export to Amazon S3\. To do so, simply replace the Amazon S3 directory in the examples above with an HDFS directory\. <a name="EMR_Hive_non-printable-utf8"></a>

**To read non\-printable UTF\-8 character data in Hive**
+ You can read and write non\-printable UTF\-8 character data with Hive by using the `STORED AS SEQUENCEFILE` clause when you create the table\. A SequenceFile is Hadoop binary file format; you need to use Hadoop to read this file\. The following example shows how to export data from DynamoDB into Amazon S3\. You can use this functionality to handle non\-printable UTF\-8 encoded characters\. 

  ```
   1. CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
   2. STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
   3. TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
   4. "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");                      
   5.                     
   6. CREATE EXTERNAL TABLE s3_export(a_col string, b_col bigint, c_col array<string>)
   7. STORED AS SEQUENCEFILE
   8. LOCATION 's3://bucketname/path/subpath/';
   9.                     
  10. INSERT OVERWRITE TABLE s3_export SELECT * 
  11. FROM hiveTableName;
  ```

## Importing Data to DynamoDB<a name="EMR_Hive_Commands_importing"></a>

 When you write data to DynamoDB using Hive you should ensure that the number of write capacity units is greater than the number of mappers in the cluster\. For example, clusters that run on m1\.xlarge EC2 instances produce 8 mappers per instance\. In the case of a cluster that has 10 instances, that would mean a total of 80 mappers\. If your write capacity units are not greater than the number of mappers in the cluster, the Hive write operation may consume all of the write throughput, or attempt to consume more throughput than is provisioned\. For more information about the number of mappers produced by each EC2 instance type, see [Configure Hadoop](emr-hadoop-config.md)\.

 The number of mappers in Hadoop are controlled by the input splits\. If there are too few splits, your write command might not be able to consume all the write throughput available\. 

 If an item with the same key exists in the target DynamoDB table, it is overwritten\. If no item with the key exists in the target DynamoDB table, the item is inserted\. 

**To import a table from Amazon S3 to DynamoDB**
+  You can use Amazon EMR \(Amazon EMR\) and Hive to write data from Amazon S3 to DynamoDB\. 

  ```
  CREATE EXTERNAL TABLE s3_import(a_col string, b_col bigint, c_col array<string>)
  ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
  LOCATION 's3://bucketname/path/subpath/';                    
                      
  CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
  TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
  "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");  
                      
  INSERT OVERWRITE TABLE hiveTableName SELECT * FROM s3_import;
  ```

**To import a table from an Amazon S3 bucket to DynamoDB without specifying a column mapping**
+  Create an `EXTERNAL` table that references data stored in Amazon S3 that was previously exported from DynamoDB\. Before importing, ensure that the table exists in DynamoDB and that it has the same key schema as the previously exported DynamoDB table\. In addition, the table must have exactly one column of type `map<string, string>`\. If you then create a Hive table that is linked to DynamoDB, you can call the `INSERT OVERWRITE` command to write the data from Amazon S3 to DynamoDB\. Because there is no column mapping, you cannot query tables that are imported this way\. Importing data without specifying a column mapping is available in Hive 0\.8\.1\.5 or later, which is supported on Amazon EMR AMI 2\.2\.3 and later\. 

  ```
  CREATE EXTERNAL TABLE s3TableName (item map<string, string>)
  ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t' LINES TERMINATED BY '\n'
  LOCATION 's3://bucketname/path/subpath/'; 
                          
  CREATE EXTERNAL TABLE hiveTableName (item map<string,string>)
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
  TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1");  
                   
  INSERT OVERWRITE TABLE hiveTableName SELECT * 
  FROM s3TableName;
  ```

**To import a table from HDFS to DynamoDB**
+  You can use Amazon EMR and Hive to write data from HDFS to DynamoDB\. 

  ```
  CREATE EXTERNAL TABLE hdfs_import(a_col string, b_col bigint, c_col array<string>)
  ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
  LOCATION 'hdfs:///directoryName';                    
                      
  CREATE EXTERNAL TABLE hiveTableName (col1 string, col2 bigint, col3 array<string>)
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler' 
  TBLPROPERTIES ("dynamodb.table.name" = "dynamodbtable1", 
  "dynamodb.column.mapping" = "col1:name,col2:year,col3:holidays");  
                      
  INSERT OVERWRITE TABLE hiveTableName SELECT * FROM hdfs_import;
  ```

## Querying Data in DynamoDB<a name="EMR_Hive_Commands_querying"></a>

 The following examples show the various ways you can use Amazon EMR to query data stored in DynamoDB\. 

**To find the largest value for a mapped column \(`max`\)**
+  Use Hive commands like the following\. In the first command, the CREATE statement creates a Hive table that references data stored in DynamoDB\. The SELECT statement then uses that table to query data stored in DynamoDB\. The following example finds the largest order placed by a given customer\. 

  ```
  CREATE EXTERNAL TABLE hive_purchases(customerId bigint, total_cost double, items_purchased array<String>) 
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
  TBLPROPERTIES ("dynamodb.table.name" = "Purchases",
  "dynamodb.column.mapping" = "customerId:CustomerId,total_cost:Cost,items_purchased:Items");
  
  SELECT max(total_cost) from hive_purchases where customerId = 717;
  ```

**To aggregate data using the `GROUP BY` clause**
+  You can use the `GROUP BY` clause to collect data across multiple records\. This is often used with an aggregate function such as sum, count, min, or max\. The following example returns a list of the largest orders from customers who have placed more than three orders\. 

  ```
  CREATE EXTERNAL TABLE hive_purchases(customerId bigint, total_cost double, items_purchased array<String>) 
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
  TBLPROPERTIES ("dynamodb.table.name" = "Purchases",
  "dynamodb.column.mapping" = "customerId:CustomerId,total_cost:Cost,items_purchased:Items");
  
  SELECT customerId, max(total_cost) from hive_purchases GROUP BY customerId HAVING count(*) > 3;
  ```

**To join two DynamoDB tables**
+  The following example maps two Hive tables to data stored in DynamoDB\. It then calls a join across those two tables\. The join is computed on the cluster and returned\. The join does not take place in DynamoDB\. This example returns a list of customers and their purchases for customers that have placed more than two orders\. 

  ```
  CREATE EXTERNAL TABLE hive_purchases(customerId bigint, total_cost double, items_purchased array<String>) 
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
  TBLPROPERTIES ("dynamodb.table.name" = "Purchases",
  "dynamodb.column.mapping" = "customerId:CustomerId,total_cost:Cost,items_purchased:Items");
  
  CREATE EXTERNAL TABLE hive_customers(customerId bigint, customerName string, customerAddress array<String>) 
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
  TBLPROPERTIES ("dynamodb.table.name" = "Customers",
  "dynamodb.column.mapping" = "customerId:CustomerId,customerName:Name,customerAddress:Address");
  
  Select c.customerId, c.customerName, count(*) as count from hive_customers c 
  JOIN hive_purchases p ON c.customerId=p.customerId 
  GROUP BY c.customerId, c.customerName HAVING count > 2;
  ```

**To join two tables from different sources**
+  In the following example, Customer\_S3 is a Hive table that loads a CSV file stored in Amazon S3 and hive\_purchases is a table that references data in DynamoDB\. The following example joins together customer data stored as a CSV file in Amazon S3 with order data stored in DynamoDB to return a set of data that represents orders placed by customers who have "Miller" in their name\. 

  ```
  CREATE EXTERNAL TABLE hive_purchases(customerId bigint, total_cost double, items_purchased array<String>) 
  STORED BY 'org.apache.hadoop.hive.dynamodb.DynamoDBStorageHandler'
  TBLPROPERTIES ("dynamodb.table.name" = "Purchases",
  "dynamodb.column.mapping" = "customerId:CustomerId,total_cost:Cost,items_purchased:Items");
  
  CREATE EXTERNAL TABLE Customer_S3(customerId bigint, customerName string, customerAddress array<String>)
  ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' 
  LOCATION 's3://bucketname/path/subpath/';
  
  Select c.customerId, c.customerName, c.customerAddress from 
  Customer_S3 c 
  JOIN hive_purchases p 
  ON c.customerid=p.customerid 
  where c.customerName like '%Miller%';
  ```

**Note**  
 In the preceding examples, the CREATE TABLE statements were included in each example for clarity and completeness\. When running multiple queries or export operations against a given Hive table, you only need to create the table one time, at the beginning of the Hive session\. 