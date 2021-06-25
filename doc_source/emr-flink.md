# Apache Flink<a name="emr-flink"></a>

[Apache Flink](https://flink.apache.org/) is a streaming dataflow engine that you can use to run real\-time stream processing on high\-throughput data sources\. Flink supports event time semantics for out\-of\-order events, exactly\-once semantics, backpressure control, and APIs optimized for writing both streaming and batch applications\.

Additionally, Flink has connectors for third\-party data sources, such as the following:
+ [Amazon Kinesis Data Streams](https://ci.apache.org/projects/flink/flink-docs-master/apis/streaming/connectors/kinesis.html)
+ [Apache Kafka](https://ci.apache.org/projects/flink/flink-docs-master/apis/streaming/connectors/kafka.html)
+ [Elasticsearch](https://ci.apache.org/projects/flink/flink-docs-master/apis/streaming/connectors/elasticsearch2.html)
+ [Twitter Streaming API](https://ci.apache.org/projects/flink/flink-docs-release-1.2/dev/connectors/twitter.html)
+ [Cassandra](https://ci.apache.org/projects/flink/flink-docs-master/apis/streaming/connectors/cassandra.html)

Amazon EMR supports Flink as a YARN application so that you can manage resources along with other applications within a cluster\. Flink\-on\-YARN allows you to submit transient Flink jobs, or you can create a long\-running cluster that accepts multiple jobs and allocates resources according to the overall YARN reservation\.

Flink is included in Amazon EMR release versions 5\.1\.0 and later\.

**Note**  
Support for the `FlinkKinesisConsumer` class was added in Amazon EMR release version 5\.2\.1\.

The following table lists the version of Flink included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Flink\.

For the version of components installed with Flink in this release, see [Release 5\.33\.0 Component Versions](emr-release-5x.md#emr-5330-release)\.


**Flink version information for emr\-5\.33\.0**  

| Amazon EMR release label | Flink version | Components installed with Flink | 
| --- | --- | --- | 
| emr\-5\.33\.0 | Flink 1\.12\.1 | emrfs, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, flink\-client, flink\-jobmanager\-config | 

**Topics**
+ [Creating a cluster with Flink](flink-create-cluster.md)
+ [Configuring Flink](flink-configure.md)
+ [Working with Flink jobs in Amazon EMR](flink-jobs.md)
+ [Using the Scala shell](flink-scala.md)
+ [Finding the Flink web interface](flink-web-interface.md)
+ [Flink release history](Flink-release-history.md)