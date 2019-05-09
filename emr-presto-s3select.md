# Using S3 Select Pushdown with Presto to Improve Performance<a name="emr-presto-s3select"></a>

With Amazon EMR release version 5\.18\.0 and later, you can use [S3 Select](https://aws.amazon.com/blogs/aws/s3-glacier-select/) Pushdown with Presto on Amazon EMR\. This feature allows Presto to "push down" the computational work of projection operations \(for example, `SELECT`\) and predicate operations \(for example, `WHERE`\) to Amazon S3\. This allows queries to retrieve only required data from Amazon S3, which can improve performance and reduce the amount of data transferred between Amazon EMR and Amazon S3 in some applications\.

## Is S3 Select Pushdown Right For My Application?<a name="emr-presto-s3select-apps"></a>

We recommend that you benchmark your applications with and without S3 Select Pushdown to see if using it may be suitable for your application\.

Use the following guidelines to determine if your application is a candidate for using S3 Select:
+ Your query filters out more than half of the original data set\.
+ Your query filter predicates use columns that have a data type supported by Presto and S3 Select\. The timestamp, real, and double data types are not supported by S3 Select Pushdown\. We recommend using the decimal data type for numerical data\. For more information about supported data types for S3 Select, see [Data Types](https://docs.aws.amazon.com/AmazonS3/latest/dev/s3-glacier-select-sql-reference-data-types.html) in the *Amazon Simple Storage Service Developer Guide*\.
+ Your network connection between Amazon S3 and the Amazon EMR cluster has good transfer speed and available bandwidth\. Amazon S3 does not compress HTTP responses, so the response size is likely to increase for compressed input files\.

## Considerations and Limitations<a name="emr-presto-s3select-considerations"></a>
+ Only objects stored in CSV format are supported\. Objects can be uncompressed or optionally compressed with gzip or bzip2\.
+ The `AllowQuotedRecordDelimiters` property is not supported\. If this property is specified, the query fails\.
+ Amazon S3 server\-side encryption with customer\-provided encryption keys \(SSE\-C\) and client\-side encryption are not supported\. 
+ S3 Select Pushdown is not a substitute for using columnar or compressed file formats such as ORC or Parquet\.

## Enabling S3 Select Pushdown With Presto<a name="emr-presto-s3select-specify"></a>

To enable S3 Select Pushdown for Presto on Amazon EMR, use the `presto-connector-hive` configuration classification to set `hive.s3select-pushdown.enabled` to `true` as shown in the example below\. For more information, see [Configuring Applications](emr-configure-apps.md)\. The hive\.s3select\-pushdown\.max\-connections value must also be set\. For most applications, the default setting of `500` should be adequate\. For more information, see [Understanding and tuning hive\.s3select\-pushdown\.max\-connections](#emr-presto-s3select-max) below\.

```
[
    {
        "classification": "presto-connector-hive",
        "properties": {
            "hive.s3select-pushdown.enabled": "true",
            "hive.s3select-pushdown.max-connections": "500"
        }
    }
]
```

### Understanding and tuning hive\.s3select\-pushdown\.max\-connections<a name="emr-presto-s3select-max"></a>

By default, Presto uses EMRFS as its file system\. The setting `fs.s3.maxConnections` in the `emrfs-site` configuration classification specifies the maximum allowable client connections to Amazon S3 through EMRFS for Presto\. By default, this is 500\. S3 Select Pushdown bypasses EMRFS when accessing Amazon S3 for predicate operations\. In this case, the value of `hive.s3select-pushdown.max-connections` determines the maximum number of client connections allowed for those operations from worker nodes\. However, any requests to Amazon S3 that Presto initiates that are not pushed down—for example, GET operations—continue to be governed by the value of `fs.s3.maxConnections`\.

If your application experiences the error "Timeout waiting for connection from pool," increase the value of both `hive.s3select-pushdown.max-connections` and `fs.s3.maxConnections`\.