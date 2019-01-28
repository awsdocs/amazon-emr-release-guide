# S3DistCp Utility Differences With Earlier AMI Versions of Amazon EMR<a name="emr-3x-s3distcp"></a>

## S3DistCp Versions Supported in Amazon EMR<a name="emr-s3distcp-verisons"></a>

The following S3DistCp versions are supported in Amazon EMR AMI releases\. S3DistCp versions after 1\.0\.7 are found on directly on the clusters\. Use the JAR in `/home/hadoop/lib` for the latest features\.


| Version | Description | Release Date | 
| --- | --- | --- | 
| 1\.0\.8 | Adds the \-\-appendToLastFile, \-\-requirePreviousManifest, and \-\-storageClass options\. | 3 January 2014 | 
| 1\.0\.7 | Adds the \-\-s3ServerSideEncryption option\. | 2 May 2013 | 
| 1\.0\.6 | Adds the \-\-s3Endpoint option\. | 6 August 2012 | 
| 1\.0\.5 | Improves the ability to specify which version of S3DistCp to run\. | 27 June 2012 | 
| 1\.0\.4 | Improves the \-\-deleteOnSuccess option\. | 19 June 2012 | 
| 1\.0\.3 | Adds support for the \-\-numberFiles and \-\-startingIndex options\. | 12 June 2012 | 
| 1\.0\.2 | Improves file naming when using groups\. | 6 June 2012 | 
| 1\.0\.1 | Initial release of S3DistCp\. | 19 January 2012 | 

## Add an S3DistCp Copy Step to a Cluster<a name="emr-3x-s3distcp-add-step"></a>

To add an S3DistCp copy step to a running cluster, type the following command, replace *j\-3GYXXXXXX9IOK* with your cluster ID, and replace *mybucket* with your Amazon S3 bucket name\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr add-steps --cluster-id j-3GYXXXXXX9IOK \
--steps Type=CUSTOM_JAR,Name="S3DistCp step",Jar=/home/hadoop/lib/emr-s3distcp-1.0.jar,\
Args=["--s3Endpoint,s3-eu-west-1.amazonaws.com",\
"--src,s3://mybucket/logs/j-3GYXXXXXX9IOJ/node/",\
"--dest,hdfs:///output",\
"--srcPattern,.*[a-zA-Z,]+"]
```

**Example Load Amazon CloudFront logs into HDFS**  
This example loads Amazon CloudFront logs into HDFS by adding a step to a running cluster\. In the process, it changes the compression format from Gzip \(the CloudFront default\) to LZO\. This is useful because data compressed using LZO can be split into multiple maps as it is decompressed, so you don't have to wait until the compression is complete, as you do with Gzip\. This provides better performance when you analyze the data using Amazon EMR\. This example also improves performance by using the regular expression specified in the `--groupBy` option to combine all of the logs for a given hour into a single file\. Amazon EMR clusters are more efficient when processing a few, large, LZO\-compressed files than when processing many, small, Gzip\-compressed files\. To split LZO files, you must index them and use the hadoop\-lzo third\-party library\.   
To load Amazon CloudFront logs into HDFS, type the following command, replace *j\-3GYXXXXXX9IOK* with your cluster ID, and replace *mybucket* with your Amazon S3 bucket name\.   
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr add-steps --cluster-id j-3GYXXXXXX9IOK \
--steps Type=CUSTOM_JAR,Name="S3DistCp step",Jar=/home/hadoop/lib/emr-s3distcp-1.0.jar,\
Args=["--src,s3://mybucket/cf","--dest,hdfs:///local",\
"--groupBy,.*XABCD12345678.([0-9]+-[0-9]+-[0-9]+-[0-9]+).*",\
"--targetSize,128",
"--outputCodec,lzo","--deleteOnSuccess"]
```
Consider the case in which the preceding example is run over the following CloudFront log files\.   

```
s3://myawsbucket/cf/XABCD12345678.2012-02-23-01.HLUS3JKx.gz
s3://myawsbucket/cf/XABCD12345678.2012-02-23-01.I9CNAZrg.gz
s3://myawsbucket/cf/XABCD12345678.2012-02-23-02.YRRwERSA.gz
s3://myawsbucket/cf/XABCD12345678.2012-02-23-02.dshVLXFE.gz
s3://myawsbucket/cf/XABCD12345678.2012-02-23-02.LpLfuShd.gz
```
S3DistCp copies, concatenates, and compresses the files into the following two files, where the file name is determined by the match made by the regular expression\.   

```
hdfs:///local/2012-02-23-01.lzo
hdfs:///local/2012-02-23-02.lzo
```