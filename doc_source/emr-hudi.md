# Hudi<a name="emr-hudi"></a>

[Apache Hudi](https://hudi.apache.org/) is an open\-source data management framework used to simplify incremental data processing and data pipeline development by providing record\-level insert, update, upsert, and delete capabilities\. *Upsert* refers to the ability to insert records into an existing dataset if they do not already exist or to update them if they do\. By efficiently managing how data is laid out in Amazon S3, Hudi allows data to be ingested and updated in near real time\. Hudi carefully maintains metadata of the actions performed on the dataset to help ensure that the actions are atomic and consistent\.

Hudi is integrated with [Apache Spark](https://aws.amazon.com/emr/features/spark/), [Apache Hive](https://hive.apache.org/), and [Presto](https://prestodb.github.io)\. In Amazon EMR release versions 6\.1\.0 and later, Hudi is also integrated with [Trino \(PrestoSQL\)](https://trino.io/)\. 

With Amazon EMR release version 5\.28\.0 and later, EMR installs Hudi components by default when Spark, Hive, or Presto are installed\. You can use Spark or the Hudi DeltaStreamer utility to create or update Hudi datasets\. You can use Hive, Spark, or Presto to query a Hudi dataset interactively or build data processing pipelines using *incremental pull*\. Incremental pull refers to the ability to pull only the data that changed between two actions\.

These features make Hudi suitable for the following use cases:
+ Working with streaming data from sensors and other Internet of Things \(IoT\) devices that require specific data insertion and update events\.
+ Complying with data privacy regulations in applications where users might choose to be forgotten or modify their consent for how their data can be used\.
+ Implementing a [change data capture \(CDC\) system](https://en.wikipedia.org/wiki/Change_data_capture) that allows you to apply changes to a dataset over time\.

The following table lists the version of Hudi included in the latest release of Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Hudi\.

For the version of components installed with Hudi in this release, see [Release 6\.4\.0 Component Versions](emr-640-release.md)\.


**Hudi version information for emr\-6\.4\.0**  

| Amazon EMR Release Label | Hudi Version | Components Installed With Hudi | 
| --- | --- | --- | 
| emr\-6\.4\.0 | Hudi 0\.8\.0\-amzn\-0 | Not available\. | 

The following table lists the version of Hudi included in the latest release of Amazon EMR 5\.x series, along with the components that Amazon EMR installs with Hudi\.

For the version of components installed with Hudi in this release, see [Release 5\.33\.0 Component Versions](emr-5330-release.md)\.


**Hudi version information for emr\-5\.33\.0**  

| Amazon EMR Release Label | Hudi Version | Components Installed With Hudi | 
| --- | --- | --- | 
| emr\-5\.33\.0 | Hudi 0\.7\.0\-amzn\-1 | Not available\. | 

**Topics**
+ [How Hudi works](emr-hudi-how-it-works.md)
+ [Considerations and limitations for using Hudi on Amazon EMR](emr-hudi-considerations.md)
+ [Create a cluster with Hudi installed](emr-hudi-installation-and-configuration.md)
+ [Work with a Hudi dataset](emr-hudi-work-with-dataset.md)
+ [Use the Hudi CLI](emr-hudi-cli.md)
+ [Hudi release history](Hudi-release-history.md)