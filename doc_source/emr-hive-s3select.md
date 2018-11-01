# Using S3 Select with Hive to Improve Performance<a name="emr-hive-s3select"></a>

With Amazon EMR release version 5\.18\.0 and later, you can use [S3 Select](https://aws.amazon.com/blogs/aws/s3-glacier-select/) with Hive on Amazon EMR\. S3 Select allows applications to retrieve only a subset of data from an object\. For Amazon EMR, the computational work of filtering large data sets for processing is "pushed down" from the cluster to Amazon S3, which can improve performance in some applications and reduces the amount of data transferred between Amazon EMR and Amazon S3\.

S3 Select is supported with Hive tables based on CSV and JSON files and by setting the `s3select.filter` configuration variable to `true` during your Hive session\. For more information and examples, see [Specifying S3 Select in Your Code](#emr-hive-s3select-specify)\.

## Is S3 Select Right For My Application?<a name="emr-hive-s3select-apps"></a>

We recommend that you benchmark your applications with and without S3 Select to see if using it may be suitable for your application\.

Use the following guidelines to determine if your application is a candidate for using S3 Select:
+ Your query filters out more than half of the original data set\.
+ Your query filter predicates use columns that have a data type supported by Amazon S3 Select\. For more information, see [Data Types](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-glacier-select-sql-reference-data-types.html) in the *Amazon Simple Storage Service Developer Guide*\.
+ Your network connection between Amazon S3 and the Amazon EMR cluster has good transfer speed and available bandwidth\. Amazon S3 does not compress HTTP responses, so the response size is likely to increase for compressed input files\.

## Considerations and Limitations<a name="emr-hive-s3select-considerations"></a>
+ Amazon S3 server\-side encryption with customer\-provided encryption keys \(SSE\-C\) and client\-side encryption are not supported\. 
+ The `AllowQuotedRecordDelimiters` property is not supported\. If this property is specified, the query fails\.
+ Only CSV and JSON files in UTF\-8 format are supported\. Multi\-line CSVs and JSON are not supported\.
+ Only uncompressed or gzip or bzip2 files are supported\.
+ Comment characters in the last line are not supported\.
+ Empty lines at the end of a file are not processed\.
+ Hive on Amazon EMR supports the primitive data types that S3 Select supports\. For more information, see [Data Types](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-glacier-select-sql-reference-data-types.html) in the *Amazon Simple Storage Service Developer Guide*\.

## Specifying S3 Select in Your Code<a name="emr-hive-s3select-specify"></a>

To use S3 select in your Hive table, create the table by specifying `com.amazonaws.emr.s3select.hive.S3SelectableTextInputFormat` as the `INPUTFORMAT` class name, and specify a value for the `s3select.format` property using the `TBLPROPERTIES` clause\.

By default, S3 Select is disabled when you run queries\. Enable S3 Select by setting `s3select.filter` to `true` in your Hive session as shown below\. The examples below demonstrate how to specify S3 Select when creating a table from underlying CSV and JSON files and then querying the table using a simple select statement\.

**Example CREATE TABLE Statement for CSV\-Based Table**  

```
CREATE TABLE mys3selecttable (
col1 string,
col2 int,
col3 boolean
)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
STORED AS
INPUTFORMAT
  'com.amazonaws.emr.s3select.hive.S3SelectableTextInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION 's3://path/to/mycsvfile/'
TBLPROPERTIES (
  "s3select.format" = "csv",
  "s3select.headerInfo" = "ignore"
);
```

**Example CREATE TABLE Statement for JSON\-Based Table**  

```
CREATE TABLE mys3selecttable (
col1 string,
col2 int,
col3 boolean
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
STORED AS
INPUTFORMAT
  'com.amazonaws.emr.s3select.hive.S3SelectableTextInputFormat'
OUTPUTFORMAT
  'org.apache.hadoop.hive.ql.io.HiveIgnoreKeyTextOutputFormat'
LOCATION 's3://path/to/json/'
TBLPROPERTIES (
  "s3select.format" = "json"
);
```

**Example SELECT TABLE Statement**  

```
SET s3select.filter=true;
SELECT * FROM mys3selecttable WHERE col2 > 10;
```