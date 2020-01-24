# Hudi \(Incubating\)<a name="emr-hudi"></a>

[Apache Hudi](https://hudi.apache.org/) is an open\-source data management framework used to simplify incremental data processing and data pipeline development by providing record\-level insert, update, upsert, and delete capabilities\. *Upsert* refers to the ability to insert records into an existing dataset if they do not already exist or to update them if they do\. By efficiently managing how data is laid out in Amazon S3, Hudi allows data to be ingested and updated in near real time\. Hudi carefully maintains metadata of the actions performed on the dataset to help ensure that the actions are atomic and consistent\.

Hudi is integrated with [Apache Spark](https://aws.amazon.com/emr/features/spark/), [Apache Hive](https://hive.apache.org/), and [Presto](https://prestodb.github.io)\. With Amazon EMR release version 5\.28\.0 and later, Amazon EMR installs Hudi components by default when Spark, Hive, or Presto are installed\. You can use Spark or the Hudi DeltaStreamer utility to create or update Hudi datasets\. You can use Hive, Spark, or Presto to query a Hudi dataset interactively or build data processing pipelines using *incremental pull*\. Incremental pull refers to the ability to pull only the data that changed between two actions\.

These features make Hudi suitable for the following use cases:
+ Working with streaming data from sensors and other Internet of Things \(IoT\) devices that require specific data insertion and update events\.
+ Complying with data privacy regulations in applications where users might choose to be forgotten or modify their consent for how their data can be used\.
+ Implementing a [change data capture \(CDC\) system](https://en.wikipedia.org/wiki/Change_data_capture) that allows you to apply changes to a dataset over time\.

The version of Hudi installed with Amazon EMR 5\.29\.0 is 0\.5\.0\-incubating\.

**Topics**
+ [How Hudi Works](emr-hudi-how-it-works.md)
+ [Considerations and Limitations for Using Hudi on Amazon EMR](emr-hudi-considerations.md)
+ [Creating a Cluster with Hudi Installed](emr-hudi-installation-and-configuration.md)
+ [Working With a Hudi Dataset](emr-hudi-work-with-dataset.md)
+ [Using the Hudi CLI](emr-hudi-cli.md)