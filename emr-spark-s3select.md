# Using S3 Select with Spark to Improve Query Performance<a name="emr-spark-s3select"></a>

With Amazon EMR release version 5\.17\.0 and later, you can use [S3 Select](https://aws.amazon.com/blogs/aws/s3-glacier-select/) with Spark on Amazon EMR\. S3 Select allows applications to retrieve only a subset of data from an object\. For Amazon EMR, the computational work of filtering large data sets for processing is "pushed down" from the cluster to Amazon S3, which can improve performance in some applications and reduces the amount of data transferred between Amazon EMR and Amazon S3\.

S3 Select is supported with CSV and JSON files using `s3selectCSV` and `s3selectJSON` values to specify the data format\. For more information and examples, see [Specifying S3 Select in Your Code](#emr-spark-s3select-specify)\.

## Is S3 Select Right For My Application?<a name="emr-spark-s3select-apps"></a>

We recommend that you benchmark your applications with and without S3 Select to see if using it may be suitable for your application\.

Use the following guidelines to determine if your application is a candidate for using S3 Select:
+ Your query filters out more than half of the original data set\.
+ Your network connection between Amazon S3 and the Amazon EMR cluster has good transfer speed and available bandwidth\. Amazon S3 does not compress HTTP responses, so the response size is likely to increase for compressed input files\.

## Considerations and Limitations<a name="emr-spark-s3select-considerations"></a>
+ Amazon S3 server\-side encryption with customer\-provided encryption keys \(SSE\-C\) and client\-side encryption are not supported\. 
+ The `AllowQuotedRecordDelimiters` property is not supported\. If this property is specified, the query fails\.
+ Only CSV and JSON files in UTF\-8 format are supported\. Multi\-line CSVs are not supported\.
+ Only uncompressed or gzip files are supported\.
+ Spark CSV and JSON options such as `nanValue`, `positiveInf`, `negativeInf`, and options related to corrupt records \(for example, failfast and dropmalformed mode\) are not supported\.
+ Using commas \(,\) within decimals is not supported\. For example, `10,000` is not supported and `10000` is\.
+ Comment characters in the last line are not supported\.
+ Empty lines at the end of a file are not processed\.
+ The following filters are not pushed down to Amazon S3:
  + Aggregate functions such as `COUNT()` and `SUM()`\.
  + Filters that `CAST()` an attribute\. For example, `CAST(stringColumn as INT) = 1`\.
  + Filters with an attribute that is an object or is complex\. For example, `intArray[1] = 1, objectColumn.objectNumber = 1`\.
  + Filters for which the value is not a literal value\. For example, `intColumn1 = intColumn2`
  + Only [S3 Select Supported Data Types](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-glacier-select-sql-reference-data-types.html) are supported with the documented limitations\.

## Specifying S3 Select in Your Code<a name="emr-spark-s3select-specify"></a>

The following examples demonstrate how to specify S3 Select for CSV using Scala, SQL, R, and PySpark\. You can use S3 Select for JSON in the same way\. For a listing of options, their default values, and limitations, see [Options](#emr-spark-s3select-specify-options)\.

------
#### [ PySpark ]

```
spark
  .read
  .format("s3selectCSV") // "s3selectJson" for Json
  .schema(...) // optional, but recommended
  .options(...) // optional
  .load("s3://path/to/my/datafiles")
```

------
#### [ R ]

```
read.df("s3://path/to/my/datafiles", "s3selectCSV", schema, header = "true", delimiter = "\t")
```

------
#### [ Scala ]

```
spark
  .read
  .format("s3selectCSV") // "s3selectJson" for Json
  .schema(...) // optional, but recommended
  .options(...) // optional. Examples:  
  // .options(Map("quote" -> "\'", "header" -> "true")) or
  // .option("quote", "\'").option("header", "true")
  .load("s3://path/to/my/datafiles")
```

------
#### [ SQL ]

```
CREATE TEMPORARY VIEW MyView (number INT, name STRING) USING s3selectCSV OPTIONS (path "s3://path/to/my/datafiles", header "true", delimiter "\t")
```

------

### Options<a name="emr-spark-s3select-specify-options"></a>

The following options are available when using `s3selectCSV` and `s3selectJSON`\. If not specified, default values are used\.

#### Options with S3selectCSV<a name="emr-spark-s3select-specify-options-csv"></a>


| Option | Default | Usage | 
| --- | --- | --- | 
|  `compression`  |  `"none"`  |  Indicates whether compression is used\. `"gzip"` is the only setting supported besides `"none"`\.  | 
|  `delimiter`  |  ","  |  Specifies the field delimiter\.  | 
|  `quote`  |  `'\"'`  |  Specifies the quote character\. Specifying an empty string is not supported and results in a malformed XML error\.  | 
|  `escape`  |  `'\\'`  |  Specifies the escape character\.  | 
|  `header`  |  `"false"`  |  `"false"` specifies that there is no header\. `"true"` specifies that a header is in the first line\. Only headers in the first line are supported, and empty lines before a header are not supported\.  | 
|  comment  |  `"#"`  |  Specifies the comment character\. The comment indicator cannot be disabled\. In other words, a value of `\u0000` is not supported\.  | 
|  `nullValue`  |  ""  |   | 

#### Options with S3selectJSON<a name="emr-spark-s3select-specify-options-json"></a>


| Option | Default | Usage | 
| --- | --- | --- | 
|  `compression`  |  `"none"`  |  Indicates whether compression is used\. `"gzip"` is the only setting supported besides `"none"`\.  | 
|  `multiline`  |  "false"  |  `"false"` specifies that the JSON is in S3 Select `LINES` format, meaning that each line in the input data contains a single JSON object\. `"true"` specifies that the JSON is in S3 Select `DOCUMENT` format, meaning that a JSON object can span multiple lines in the input data\.  | 