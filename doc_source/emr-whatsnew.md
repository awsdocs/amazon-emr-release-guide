# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.14\.0 Tab](emr-release-5x.md#emr-5140-release), along with the application versions, component versions, and available configuration classifications for this release\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.14\.0 \(Latest\)<a name="emr-5140-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.14\.0\. Changes are relative to 5\.13\.0\.

Initial release date: June 4, 2018

**Upgrades**
+ Upgraded Apache Flink to 1\.4\.2
+ Upgraded Apache MXnet to 1\.1\.0
+ Upgraded Apache Sqoop to 1\.4\.7

**New Features**
+ Added JupyterHub support\. For more information, see [JupyterHub](emr-jupyterhub.md)\.

**Changes, Enhancements, and Resolved Issues**
+ EMRFS
  + The userAgent string in requests to Amazon S3 has been updated to contain the user and group information of the invoking principal\. This can be used with AWS CloudTrail logs for more comprehensive request tracking\.
+ MXnet
  + Added OpenCV libraries\.
+ Spark
  + When Spark writes Parquet files to an Amazon S3 location using EMRFS, the FileOutputCommitter algorithm has been updated to use version 2 instead of version 1\. This reduces the number of renames, which improves application performance\. This change does not affect: 
    + Applications other than Spark\. 
    + Applications that write to other file systems, such as HDFS \(which still use version 1 of FileOutputCommitter\)\.
    + Applications that use other output formats, such as text or csv, that already use EMRFS direct write\.

**Known Issues**
+ Using configuration classifications to set up JupyterHub and individual Jupyter notebooks when you create a cluster is not supported\. Edit the jupyterhub\_config\.py file and jupyter\_notebook\_config\.py files for each user manually\. For more information, see [Configuring JupyterHub](emr-jupyterhub-configure.md)\.