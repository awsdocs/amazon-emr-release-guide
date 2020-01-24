# Connectors and Utilities<a name="emr-connectors"></a>

Amazon EMR provides several connectors and utilities to access other AWS services as data sources\. You can usually access data in these services within a program\. For example, you can specify an Kinesis stream in a Hive query, Pig script, or MapReduce application and then operate on that data\.

**Topics**
+ [Export, Import, Query, and Join Tables in DynamoDB Using Amazon EMR](EMRforDynamoDB.md)
+ [Kinesis](emr-kinesis.md)
+ [S3DistCp \(s3\-dist\-cp\)](UsingEMR_s3distcp.md)
+ [Cleaning Up After Failed S3DistCp Jobs](#s3distcp-cleanup)

## Cleaning Up After Failed S3DistCp Jobs<a name="s3distcp-cleanup"></a>

If S3DistCp cannot copy some or all of the specified files, the command or cluster step fails and returns a non\-zero error code\. If this occurs, S3DistCp does not clean up partially copied files\. You must delete them manually\.

Partially copied files are saved to the HDFS `tmp` directory in sub\-directories with the unique identifier of the S3DistCp job\. You can find this ID in the standard output of the job\.

For example, for an S3DistCp job with the ID `4b1c37bb-91af-4391-aaf8-46a6067085a6`, you can connect to the master node of the cluster and run the following command to view output files associated with the job\.

```
hdfs dfs -ls /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output
```

The command returns a list of files similar to the following:

```
Found 8 items
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:03 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/_SUCCESS
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:02 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00000
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:02 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00001
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:02 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00002
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:03 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00003
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:03 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00004
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:03 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00005
-rw-r--r--   1 hadoop hadoop          0 2018-12-10 06:03 /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6/output/part-r-00006
```

You can then run the following command to delete the directory and all contents\.

```
hdfs dfs rm -rf /tmp/4b1c37bb-91af-4391-aaf8-46a6067085a6
```