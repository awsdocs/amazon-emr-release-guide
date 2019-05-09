# Access the Spark Shell<a name="emr-spark-shell"></a>

The Spark shell is based on the Scala REPL \(Read\-Eval\-Print\-Loop\)\. It allows you to create Spark programs interactively and submit work to the framework\. You can access the Spark shell by connecting to the master node with SSH and invoking `spark-shell`\. For more information about connecting to the master node, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\. The following examples use Apache HTTP Server access logs stored in Amazon S3\.

**Note**  
The bucket used in these examples is available to clients that can access US East \(N\. Virginia\)\.

 By default, the Spark shell creates its own [SparkContext](https://spark.apache.org/docs/1.3.1/api/scala/index.html#org.apache.spark.SparkContext) object called `sc`\. You can use this context if it is required within the REPL\. sqlContext is also available in the shell and it is a [HiveContext](https://spark.apache.org/docs/latest/api/scala/index.html#org.apache.spark.sql.hive.HiveContext)\. 

**Example Using the Spark shell to count the occurrences of a string in a file stored in Amazon S3**  
This example uses `sc` to read a textFile in Amazon S3\.  

```
scala> sc
res0: org.apache.spark.SparkContext = org.apache.spark.SparkContext@404721db

scala> val textFile = sc.textFile("s3://elasticmapreduce/samples/hive-ads/tables/impressions/dt=2009-04-13-08-05/ec2-0-51-75-39.amazon.com-2009-04-13-08-05.log")
```
Spark creates the textFile and associated [data structure](https://spark.apache.org/docs/latest/programming-guide.html#resilient-distributed-datasets-rdds)\. Next, the example counts the number of lines in the log file with the string "cartoonnetwork\.com":  

```
scala> val linesWithCartoonNetwork = textFile.filter(line => line.contains("cartoonnetwork.com")).count()
linesWithCartoonNetwork: org.apache.spark.rdd.RDD[String] = MapPartitionsRDD[2] at filter at <console>:23
<snip>
<Spark program runs>
scala> linesWithCartoonNetwork
res2: Long = 9
```

**Example Using the Python\-based Spark shell to count the occurrences of a string in a file stored in Amazon S3**  
Spark also includes a Python\-based shell, `pyspark`, that you can use to prototype Spark programs written in Python\. Just as with `spark-shell`, invoke `pyspark` on the master node; it also has the same [SparkContext](https://spark.apache.org/docs/latest/api/python/pyspark.html#pyspark.SparkContext) object\.   

```
>>> sc
<pyspark.context.SparkContext object at 0x7fe7e659fa50>
>>> textfile = sc.textFile("s3://elasticmapreduce/samples/hive-ads/tables/impressions/dt=2009-04-13-08-05/ec2-0-51-75-39.amazon.com-2009-04-13-08-05.log")
```
Spark creates the textFile and associated [data structure](https://spark.apache.org/docs/latest/programming-guide.html#resilient-distributed-datasets-rdds)\. Next, the example counts the number of lines in the log file with the string "cartoonnetwork\.com"\.  

```
>>> linesWithCartoonNetwork = textfile.filter(lambda line: "cartoonnetwork.com" in line).count()
15/06/04 17:12:22 INFO lzo.GPLNativeCodeLoader: Loaded native gpl library from the embedded binaries
15/06/04 17:12:22 INFO lzo.LzoCodec: Successfully loaded & initialized native-lzo library [hadoop-lzo rev EXAMPLE]
15/06/04 17:12:23 INFO fs.EmrFileSystem: Consistency disabled, using com.amazon.ws.emr.hadoop.fs.s3n.S3NativeFileSystem as filesystem implementation
<snip>
<Spark program continues>
>>> linesWithCartoonNetwork
9
```