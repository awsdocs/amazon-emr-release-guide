# Example: Create an HCatalog Table and Write to it Using Pig<a name="emr-hcatalog-pig"></a>

You can create an HCatalog table and use Apache Pig to write to it by way of HCatStorer using a data source in Amazon S3\. HCatalog requires that you disable direct write, or the operation fails silently\. Set both the `mapred.output.direct.NativeS3FileSystem `and the `mapred.output.direct.EmrFileSystem` configurations to `false` either using the `mapred-site` classification, or manually from within the Grunt shell\. The following example shows a table created using the HCat CLI, followed by commands executed in the Grunt shell to populate the table from a sample data file in Amazon S3\. 

To run this example, [connect to the Master node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html)\.

Create an HCatalog script file, `wikicount.q`, with the following contents, which creates an HCatalog table nameed `wikicount`\.

```
CREATE EXTERNAL TABLE IF NOT EXISTS wikicount( 
col1 string, 
col2 bigint 
) 
ROW FORMAT DELIMITED FIELDS TERMINATED BY '\001' 
STORED AS ORC 
LOCATION 's3://MyBucket/hcat/wikicount';
```

Use an HCat CLI command to execute the script from the file\.

```
hcat -f wikicount.q
```

Next, start the Grunt shell with the `-useHCatalog` option, set configurations to disable direct write, load data from an S3 location, and then write the results to the wikicount table\.

```
pig -useHCatalog
SET mapred.output.direct.NativeS3FileSystem false; 
SET mapred.output.direct.EmrFileSystem false; 
A = LOAD 's3://support.elasticmapreduce/training/datasets/wikistats_tiny/' USING PigStorage(' ') AS (Site:chararray, page:chararray, views:int, total_bytes:long); 
B = GROUP A BY Site; 
C = FOREACH B GENERATE group as col1, COUNT(A) as col2; 
STORE C INTO 'wikicount' USING org.apache.hive.hcatalog.pig.HCatStorer();
```