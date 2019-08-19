# S3DistCp \(s3\-dist\-cp\)<a name="UsingEMR_s3distcp"></a>

Apache DistCp is an open\-source tool you can use to copy large amounts of data\. *S3DistCp* is an extension of DistCp that is optimized to work with AWS, particularly Amazon S3\. The command for S3DistCp in Amazon EMR version 4\.0 and later is `s3-dist-cp`, which you add as a step in a cluster or at the command line\. Using S3DistCp, you can efficiently copy large amounts of data from Amazon S3 into HDFS where it can be processed by subsequent steps in your Amazon EMR cluster\. You can also use S3DistCp to copy data between Amazon S3 buckets or from HDFS to Amazon S3\. S3DistCp is more scalable and efficient for parallel copying large numbers of objects across buckets and across AWS accounts\.

For specific commands that demonstrate the flexibility of S3DistCP in real\-world scenarios, see [Seven Tips for Using S3DistCp](http://aws.amazon.com/blogs/big-data/seven-tips-for-using-s3distcp-on-amazon-emr-to-move-data-efficiently-between-hdfs-and-amazon-s3/) on the AWS Big Data blog\.

Like DistCp, S3DistCp uses MapReduce to copy in a distributed manner\. It shares the copy, error handling, recovery, and reporting tasks across several servers\. For more information about the Apache DistCp open source project, see the [DistCp Guide](http://hadoop.apache.org/docs/stable/hadoop-distcp/DistCp.html) in the Apache Hadoop documentation\.

If S3DistCp is unable to copy some or all of the specified files, the cluster step fails and returns a non\-zero error code\. If this occurs, S3DistCp does not clean up partially copied files\. 

**Important**  
S3DistCp does not support Amazon S3 bucket names that contain the underscore character\.

## S3DistCp Options<a name="UsingEMR_s3distcp.options"></a>

When you call S3DistCp, you can specify options that change how it copies and compresses data\. These are described in the following table\. The options are added to the step using the arguments list\. Examples of the S3DistCp arguments are shown in the following table\. 


| Option  | Description  | Required  | 
| --- | --- | --- | 
| \-\-src=LOCATION  |  Location of the data to copy\. This can be either an HDFS or Amazon S3 location\.  Example: `--src=s3://myawsbucket/logs/j-3GYXXXXXX9IOJ/node`  S3DistCp does not support Amazon S3 bucket names that contain the underscore character\.  | Yes  | 
| \-\-dest=LOCATION  |  Destination for the data\. This can be either an HDFS or Amazon S3 location\.  Example: `--dest=hdfs:///output`  S3DistCp does not support Amazon S3 bucket names that contain the underscore character\.  | Yes  | 
| \-\-srcPattern=PATTERN  |  A [regular expression](http://en.wikipedia.org/wiki/Regular_expression) that filters the copy operation to a subset of the data at `--src`\. If neither `--srcPattern` nor `--groupBy` is specified, all data at `--src` is copied to `--dest`\.  If the regular expression argument contains special characters, such as an asterisk \(\*\), either the regular expression or the entire `--args` string must be enclosed in single quotes \('\)\.  Example: `--srcPattern=.*daemons.*-hadoop-.*`   | No  | 
| \-\-groupBy=PATTERN  |  A [regular expression](http://en.wikipedia.org/wiki/Regular_expression) that causes S3DistCp to concatenate files that match the expression\. For example, you could use this option to combine all of the log files written in one hour into a single file\. The concatenated filename is the value matched by the regular expression for the grouping\.  Parentheses indicate how files should be grouped, with all of the items that match the parenthetical statement being combined into a single output file\. If the regular expression does not include a parenthetical statement, the cluster fails on the S3DistCp step and return an error\.  If the regular expression argument contains special characters, such as an asterisk \(\*\), either the regular expression or the entire `--args` string must be enclosed in single quotes \('\)\.  When `--groupBy` is specified, only files that match the specified pattern are copied\. You do not need to specify `--groupBy` and `--srcPattern` at the same time\.  Example: `--groupBy=.*subnetid.*([0-9]+-[0-9]+-[0-9]+-[0-9]+).*`  | No  | 
| \-\-targetSize=SIZE  |  The size, in mebibytes \(MiB\), of the files to create based on the `--groupBy` option\. This value must be an integer\. When `--targetSize` is set, S3DistCp attempts to match this size; the actual size of the copied files may be larger or smaller than this value\. Jobs are aggregated based on the size of the data file, thus it is possible that the target file size will match the source data file size\.  If the files concatenated by `--groupBy` are larger than the value of `--targetSize`, they are broken up into part files, and named sequentially with a numeric value appended to the end\. For example, a file concatenated into `myfile.gz` would be broken into parts as: `myfile0.gz`, `myfile1.gz`, etc\.  Example: `--targetSize=2`   | No  | 
| \-\-appendToLastFile |  Specifies the behavior of S3DistCp when copying to files from Amazon S3 to HDFS which are already present\. It appends new file data to existing files\. If you use `--appendToLastFile` with `--groupBy`, new data is appended to files which match the same groups\. This option also respects the `--targetSize` behavior when used with `--groupBy.`  | No  | 
| \-\-outputCodec=CODEC  |  Specifies the compression codec to use for the copied files\. This can take the values: `gzip`, `gz`, `lzo`, `snappy`, or `none`\. You can use this option, for example, to convert input files compressed with Gzip into output files with LZO compression, or to uncompress the files as part of the copy operation\. If you choose an output codec, the filename will be appended with the appropriate extension \(e\.g\. for `gz` and `gzip`, the extension is `.gz`\) If you do not specify a value for `--outputCodec`, the files are copied over with no change in their compression\.  Example: `--outputCodec=lzo`   | No  | 
| \-\-s3ServerSideEncryption  |  Ensures that the target data is transferred using SSL and automatically encrypted in Amazon S3 using an AWS service\-side key\. When retrieving data using S3DistCp, the objects are automatically unencrypted\. If you attempt to copy an unencrypted object to an encryption\-required Amazon S3 bucket, the operation fails\. For more information, see [Using Data Encryption](https://docs.aws.amazon.com/AmazonS3/latest/dev//UsingEncryption.html)\.  Example: `--s3ServerSideEncryption`   | No  | 
| \-\-deleteOnSuccess  |  If the copy operation is successful, this option causes S3DistCp to delete the copied files from the source location\. This is useful if you are copying output files, such as log files, from one location to another as a scheduled task, and you don't want to copy the same files twice\.  Example: `--deleteOnSuccess`   | No  | 
| \-\-disableMultipartUpload  |  Disables the use of multipart upload\.  Example: `--disableMultipartUpload`   | No  | 
| \-\-multipartUploadChunkSize=SIZE  |  The size, in MiB, of the multipart upload part size\. By default, it uses multipart upload when writing to Amazon S3\. The default chunk size is 16 MiB\.  Example: `--multipartUploadChunkSize=32`   | No  | 
| \-\-numberFiles  |  Prepends output files with sequential numbers\. The count starts at 0 unless a different value is specified by `--startingIndex`\.  Example: `--numberFiles`   | No  | 
| \-\-startingIndex=INDEX  |  Used with `--numberFiles` to specify the first number in the sequence\.  Example: `--startingIndex=1`   | No  | 
| \-\-outputManifest=FILENAME  |  Creates a text file, compressed with Gzip, that contains a list of all the files copied by S3DistCp\.  Example: `--outputManifest=manifest-1.gz`   | No  | 
| \-\-previousManifest=PATH  |  Reads a manifest file that was created during a previous call to S3DistCp using the `--outputManifest` flag\. When the `--previousManifest` flag is set, S3DistCp excludes the files listed in the manifest from the copy operation\. If `--outputManifest` is specified along with `--previousManifest`, files listed in the previous manifest also appear in the new manifest file, although the files are not copied\.  Example: `--previousManifest=/usr/bin/manifest-1.gz`   | No  | 
| \-\-requirePreviousManifest |  Requires a previous manifest created during a previous call to S3DistCp\. If this is set to false, no error is generated when a previous manifest is not specified\. The default is true\.  | No  | 
| \-\-copyFromManifest  |  Reverses the behavior of `--previousManifest` to cause S3DistCp to use the specified manifest file as a list of files to copy, instead of a list of files to exclude from copying\.  Example: `--copyFromManifest --previousManifest=/usr/bin/manifest-1.gz`   | No  | 
| \-\-s3Endpoint=ENDPOINT |  Specifies the Amazon S3 endpoint to use when uploading a file\. This option sets the endpoint for both the source and destination\. If not set, the default endpoint is `s3.amazonaws.com`\. For a list of the Amazon S3 endpoints, see [Regions and Endpoints](https://docs.aws.amazon.com/general/latest/gr/rande.html#s3_region)\.  Example: `--s3Endpoint=s3-eu-west-1.amazonaws.com`   | No  | 
| \-\-storageClass=CLASS |  The storage class to use when the destination is Amazon S3\. Valid values are STANDARD and REDUCED\_REDUNDANCY\. If this option is not specified, S3DistCp tries to preserve the storage class\. Example: `--storageClass=STANDARD`  | No  | 
| \-\-srcPrefixesFile=PATH |  a text file in Amazon S3 \(s3://\), HDFS \(hdfs:///\) or local file system \(file:/\) that contains a list of `src` prefixes, one prefix per line\.  If `srcPrefixesFile` is provided, S3DistCp will not list the src path\. Instead, it generates a source list as the combined result of listing all prefixes specified in this file\. The relative path as compared to src path, instead of these prefixes, will be used to generate the destination paths\. If `srcPattern` is also specified, it will be applied to the combined list results of the source prefixes to further filter the input\. If `copyFromManifest` is used, objects in the manifest will be copied and `srcPrefixesFile` will be ignored\. Example: `--srcPrefixesFile=PATH`  | No  | 

In addition to the options above, S3DistCp implements the [Tool interface](https://hadoop.apache.org/docs/current/api/org/apache/hadoop/util/Tool.html) which means that it supports the generic options\. 

## Adding S3DistCp as a Step in a Cluster<a name="UsingEMR_s3distcp.step"></a>

You can call S3DistCp by adding it as a step in your cluster\. Steps can be added to a cluster at launch or to a running cluster using the console, CLI, or API\. The following examples demonstrate adding an S3DistCp step to a running cluster\. For more information on adding steps to a cluster, see [Submit Work to a Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/AddingStepstoaJobFlow.html) in the *Amazon EMR Management Guide*\.

**To add an S3DistCp step to a running cluster using the AWS CLI**

For more information on using Amazon EMR commands in the AWS CLI, see [https://docs.aws.amazon.com/cli/latest/reference/emr](https://docs.aws.amazon.com/cli/latest/reference/emr)\.
+ To add a step to a cluster that calls S3DistCp, pass the parameters that specify how S3DistCp should perform the copy operation as arguments\. 

  The following example copies daemon logs from Amazon S3 to `hdfs:///output`\. In the following command:
  + `--cluster-id` specifies the cluster 
  + `Jar` is the location of the S3DistCp JAR file 
  + `Args` is a comma\-separated list of the option name\-value pairs to pass in to S3DistCp\. For a complete list of the available options, see [S3DistCp Options](#UsingEMR_s3distcp.options)\. 

  To add an S3DistCp copy step to a running cluster, put the following in a JSON file saved in Amazon S3 or your local file system as `myStep.json` for this example\. Replace *j\-3GYXXXXXX9IOK* with your cluster ID and replace *mybucket* with your Amazon S3 bucket name\.

  ```
  [
      {
          "Name":"S3DistCp step",
          "Args":["s3-dist-cp","--s3Endpoint=s3.amazonaws.com","--src=s3://mybucket/logs/j-3GYXXXXXX9IOJ/node/","--dest=hdfs:///output","--srcPattern=.*[a-zA-Z,]+"],
          "ActionOnFailure":"CONTINUE",
          "Type":"CUSTOM_JAR",
          "Jar":"command-runner.jar"        
      }
  ]
  ```

  ```
  aws emr add-steps --cluster-id j-3GYXXXXXX9IOK --steps file://./myStep.json
  ```

**Example Copy log files from Amazon S3 to HDFS**  
This example also illustrates how to copy log files stored in an Amazon S3 bucket into HDFS by adding a step to a running cluster\. In this example the `--srcPattern` option is used to limit the data copied to the daemon logs\.   
To copy log files from Amazon S3 to HDFS using the `--srcPattern` option, put the following in a JSON file saved in Amazon S3 or your local file system as `myStep.json` for this example\. Replace *j\-3GYXXXXXX9IOK* with your cluster ID and replace *mybucket* with your Amazon S3 bucket name\.  

```
[
    {
        "Name":"S3DistCp step",
        "Args":["s3-dist-cp","--s3Endpoint=s3.amazonaws.com","--src=s3://mybucket/logs/j-3GYXXXXXX9IOJ/node/","--dest=hdfs:///output","--srcPattern=.*daemons.*-hadoop-.*"],
        "ActionOnFailure":"CONTINUE",
        "Type":"CUSTOM_JAR",
        "Jar":"command-runner.jar"        
    }
]
```