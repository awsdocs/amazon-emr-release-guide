# Using Tez<a name="tez-using"></a>

The following examples show you how to use Tez for the data and scripts used in the tutorial [Getting Started: Analyzing Big Data with Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-gs.html) shown in [Step 3](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-gs-prepare-data-and-script.html)\.

**Compare the Hive runtimes of MapReduce vs\. Tez**

1. Create a cluster as shown in the procedure called [To create a cluster with Tez installed using the console](tez-create-cluster.md#emr-tez-create)\. Choose **Hive** as an application in addition to **Tez**\.

1. Connect to the cluster master node using SSH\. For more information, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html)\.

1. Run the `Hive_CloudFront.q` script using MapReduce with the following command, where *region* is the region in which your cluster is located:

   ```
   hive -f s3://region.elasticmapreduce.samples/cloudfront/code/Hive_CloudFront.q \
   -d INPUT=s3://region.elasticmapreduce.samples -d OUTPUT=s3://myBucket/mr-test/
   ```

   The output should look something like the following:

   ```
   <snip>
   Starting Job = job_1464200677872_0002, Tracking URL = http://ec2-host:20888/proxy/application_1464200677872_0002/
   Kill Command = /usr/lib/hadoop/bin/hadoop job  -kill job_1464200677872_0002
   Hadoop job information for Stage-1: number of mappers: 1; number of reducers: 1
   2016-05-27 04:53:11,258 Stage-1 map = 0%,  reduce = 0%
   2016-05-27 04:53:25,820 Stage-1 map = 13%,  reduce = 0%, Cumulative CPU 10.45 sec
   2016-05-27 04:53:32,034 Stage-1 map = 33%,  reduce = 0%, Cumulative CPU 16.06 sec
   2016-05-27 04:53:35,139 Stage-1 map = 40%,  reduce = 0%, Cumulative CPU 18.9 sec
   2016-05-27 04:53:37,211 Stage-1 map = 53%,  reduce = 0%, Cumulative CPU 21.6 sec
   2016-05-27 04:53:41,371 Stage-1 map = 100%,  reduce = 0%, Cumulative CPU 25.08 sec
   2016-05-27 04:53:49,675 Stage-1 map = 100%,  reduce = 100%, Cumulative CPU 29.93 sec
   MapReduce Total cumulative CPU time: 29 seconds 930 msec
   Ended Job = job_1464200677872_0002
   Moving data to: s3://myBucket/mr-test/os_requests
   MapReduce Jobs Launched: 
   Stage-Stage-1: Map: 1  Reduce: 1   Cumulative CPU: 29.93 sec   HDFS Read: 599 HDFS Write: 0 SUCCESS
   Total MapReduce CPU Time Spent: 29 seconds 930 msec
   OK
   Time taken: 49.699 seconds
   ```

1. Using a text editor, replace the `hive.execution.engine` value with `tez` in `/etc/hive/conf/hive-site.xml`\.

1. Kill the HiveServer2 process with the following command:

   ```
   sudo kill -9 $(pgrep -f HiveServer2)
   ```

   Upstart automatically restarts the Hive server with your configuration changes loaded\.

1. Now run the job with the Tez execution engine using the following command:

   ```
   hive -f s3://region.elasticmapreduce.samples/cloudfront/code/Hive_CloudFront.q \
   -d INPUT=s3://region.elasticmapreduce.samples -d OUTPUT=s3://myBucket/tez-test/
   ```

   The output should look something like the following:

   ```
   Time taken: 0.517 seconds
   Query ID = hadoop_20160527050505_dcdc075f-8338-4041-adc3-d2ffe69dfcdd
   Total jobs = 1
   Launching Job 1 out of 1
   
   
   Status: Running (Executing on YARN cluster with App id application_1464200677872_0003)
   
   --------------------------------------------------------------------------------
           VERTICES      STATUS  TOTAL  COMPLETED  RUNNING  PENDING  FAILED  KILLED
   --------------------------------------------------------------------------------
   Map 1 ..........   SUCCEEDED      1          1        0        0       0       0
   Reducer 2 ......   SUCCEEDED      1          1        0        0       0       0
   --------------------------------------------------------------------------------
   VERTICES: 02/02  [==========================>>] 100%  ELAPSED TIME: 27.61 s    
   --------------------------------------------------------------------------------
   Moving data to: s3://myBucket/tez-test/os_requests
   OK
   Time taken: 30.711 seconds
   ```

   The time to run the same application took approximately 20 seconds \(40%\) less time using Tez\.