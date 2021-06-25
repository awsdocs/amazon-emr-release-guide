# Amazon EMR 2\.x and 3\.x AMI versions<a name="emr-release-3x"></a>

**Note**  
This topic replaces the Amazon EMR Developer Guide, which has been retired\.

Amazon EMR 2\.x and 3\.x releases, called *AMI versions*, are made available for pre\-existing solutions that require them for compatibility reasons\. We do not recommend creating new clusters or new solutions with these release versions\. They lack features of newer releases and include outdated application packages\.

We recommend that you build solutions using the most recent Amazon EMR release version\.

The scope of differences between the 2\.x and 3\.x series release versions and recent Amazon EMR release versions is significant\. Those differences range from how you create and configure a cluster to the ports and directory structure of applications on the cluster\.

This section attempts to cover the most significant differences for Amazon EMR, as well as specific application configuration and management differences\. It is not comprehensive\. If you create and use clusters in the 2\.x or 3\.x series, you may encounter differences not covered in this section\.

**Topics**
+ [Creating a cluster with earlier AMI versions of Amazon EMR](emr-3x-create.md)
+ [Installing applications with earlier AMI versions of Amazon EMR](emr-3x-install-apps.md)
+ [Customizing cluster and application configuration with earlier AMI versions of Amazon EMR](emr-3x-customizeappconfig.md)
+ [Hive application specifics for earlier AMI versions of Amazon EMR](emr-3x-hive.md)
+ [HBase application specifics for earlier AMI versions of Amazon EMR](emr-3x-hbase.md)
+ [Pig application specifics for earlier AMI versions of Amazon EMR](emr-3x-pig.md)
+ [Spark application specifics with earlier AMI versions of Amazon EMR](emr-3x-spark.md)
+ [S3DistCp utility differences with earlier AMI versions of Amazon EMR](emr-3x-s3distcp.md)