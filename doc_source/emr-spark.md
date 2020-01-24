# Apache Spark<a name="emr-spark"></a>

[Apache Spark](https://aws.amazon.com/emr/features/spark/) is a distributed processing framework and programming model that helps you do machine learning, stream processing, or graph analytics using Amazon EMR clusters\. Similar to Apache Hadoop, Spark is an open\-source, distributed processing system commonly used for big data workloads\. However, Spark has several notable differences from Hadoop MapReduce\. Spark has an optimized directed acyclic graph \(DAG\) execution engine and actively caches data in\-memory, which can boost performance, especially for certain algorithms and interactive queries\.

Spark natively supports applications written in Scala, Python, and Java\. It also includes several tightly integrated libraries for SQL \([Spark SQL](https://spark.apache.org/sql/)\), machine learning \([MLlib](https://spark.apache.org/mllib/)\), stream processing \([Spark Streaming](https://spark.apache.org/streaming/)\), and graph processing \([GraphX](https://spark.apache.org/graphx/)\)\. These tools make it easier to leverage the Spark framework for a wide variety of use cases\. 

You can install Spark on an EMR cluster along with other Hadoop applications, and it can also leverage the EMR file system \(EMRFS\) to directly access data in Amazon S3\. Hive is also integrated with Spark so that you can use a HiveContext object to run Hive scripts using Spark\. A Hive context is included in the spark\-shell as `sqlContext`\. 

For an example tutorial of setting up an EMR cluster with Spark and analyzing a sample data set, see [New — Apache Spark on Amazon EMR](https://aws.amazon.com/blogs/aws/new-apache-spark-on-amazon-emr/) on the AWS News blog\.

To view a machine learning example using Spark on Amazon EMR, see the [Large\-Scale Machine Learning with Spark on Amazon EMR](http://aws.amazon.com/blogs/big-data/large-scale-machine-learning-with-spark-on-amazon-emr/) on the AWS Big Data blog\.

**Important**  
Apache Spark version 2\.3\.1, available beginning with Amazon EMR release version 5\.16\.0, addresses [CVE\-2018\-8024](https://nvd.nist.gov/vuln/detail/CVE-2018-8024) and [CVE\-2018\-1334](https://nvd.nist.gov/vuln/detail/CVE-2018-1334)\. We recommend that you migrate earlier versions of Spark to Spark version 2\.3\.1 or later\.

The following table lists the version of Spark included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Spark\.

For the version of components installed with Spark in this release, see [Release 5\.29\.0 Component Versions](emr-release-5x.md#emr-5290-release)\.


**Spark Version Information for emr\-5\.29\.0**  

| Amazon EMR Release Label | Spark Version | Components Installed With Spark | 
| --- | --- | --- | 
| emr\-5\.29\.0 | Spark 2\.4\.4 | aws\-sagemaker\-spark\-sdk, emrfs, emr\-goodies, emr\-ddb, emr\-s3\-select, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, hudi, livy\-server, nginx, r, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave | 

**Topics**
+ [Create a Cluster With Spark](emr-spark-launch.md)
+ [Using the AWS Glue Data Catalog as the Metastore for Spark SQL](emr-spark-glue.md)
+ [Configure Spark](emr-spark-configure.md)
+ [Optimizing Spark Performance](emr-spark-performance.md)
+ [Access the Spark Shell](emr-spark-shell.md)
+ [Using Amazon SageMaker Spark for Machine Learning](emr-spark-sagemaker.md)
+ [Write a Spark Application](emr-spark-application.md)
+ [Improving Spark Performance With Amazon S3](emr-spark-s3-performance.md)
+ [Adding a Spark Step](emr-spark-submit-step.md)
+ [View Spark Application History](emr-spark-application-history.md)
+ [Accessing the Spark Web UIs](emr-spark-webui.md)
+ [Spark Release History](Spark-release-history.md)