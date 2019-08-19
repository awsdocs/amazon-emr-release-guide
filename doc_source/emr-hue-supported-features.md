# Supported and Unsupported Features of Hue on Amazon EMR<a name="emr-hue-supported-features"></a>
+ Amazon S3 and Hadoop File System \(HDFS\) Browser
  + With the appropriate permissions, you can browse and move data between the ephemeral HDFS storage and S3 buckets belonging to your account\. 
  + By default, superusers in Hue can access all files that Amazon EMR IAM roles are allowed to access\. Newly created users do not automatically have permissions to access the Amazon S3 filebrowser and must have the `filebrowser.s3_access` permissions enabled for their group\.
+ Hive—Run interactive queries on your data\. This is also a useful way to prototype programmatic or batched querying\.
+ Pig—Run scripts on your data or issue interactive commands\.
+ Oozie—Create and monitor Oozie workflows\.
+ Metastore Manager—View and manipulate the contents of the Hive metastore \(import/create, drop, and so on\)\. 
+ Job browser—See the status of your submitted Hadoop jobs\.
+ User management—Manage Hue user accounts and integrate LDAP users with Hue\.
+ AWS Samples—There are several "ready\-to\-run" examples that process sample data from various AWS services using applications in Hue\. When you log in to Hue, you are taken to the Hue Home application where the samples are pre\-installed\.
+ Livy Server is supported only in Amazon EMR version 5\.9\.0 and later\.
+ To use the Hue Notebook for Spark, you must install Hue with Livy and Spark\.
+ The Hue Dashboard is not supported\.