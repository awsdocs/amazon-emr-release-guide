# Iceberg<a name="emr-iceberg"></a>

[Apache Iceberg](https://iceberg.apache.org/) is an open table format for large data sets in Amazon S3 and provides fast query performance over large tables, atomic commits, concurrent writes, and SQL\-compatible table evolution\. Starting with Amazon EMR 6\.5\.0, you can use Apache Spark 3 on Amazon EMR clusters with the Iceberg table format\.

The following table lists the version of Iceberg included in the latest release of the Amazon EMR 6\.x series, along with the components that Amazon EMR installs with Iceberg\.

For the version of components installed with Iceberg in this release, see [Release 6\.5\.0 Component Versions](emr-650-release.md)\.


**Iceberg version information for emr\-6\.5\.0**  

| Amazon EMR Release Label | Iceberg Version | Components Installed With Iceberg | 
| --- | --- | --- | 
| emr\-6\.5\.0 | Iceberg 0\.12\.0 | Not available\. | 

**Topics**
+ [How Iceberg works](emr-iceberg-how-it-works.md)
+ [Create a cluster with Iceberg installed](emr-iceberg-create-cluster.md)
+ [Considerations and limitations for using Iceberg on Amazon EMR](emr-iceberg-considerations.md)
+ [Iceberg release history](Iceberg-release-history.md)