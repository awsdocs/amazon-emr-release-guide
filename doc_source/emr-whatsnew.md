# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.13\.0 Tab](emr-release-5x.md#emr-5130-release), along with the application versions, component versions, and available configuration classifications for this release\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.13\.0 \(Latest\)<a name="emr-5130-whatsnew"></a>

The following release notes include information for the Amazon EMR release version 5\.13\.0\. Changes are relative to 5\.12\.0\.

**Upgrades**
+ Upgraded Spark to 2\.3\.0
+ Upgraded HBase to 1\.4\.2
+ Upgraded Presto to 0\.194
+ Upgraded AWS Java SDK to 1\.11\.297

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Backported [HIVE\-15436](https://issues.apache.org/jira/browse/HIVE-15436)\. Enhanced Hive APIs to return only views\.

**Known Issues**
+ MXNet does not currently have OpenCV libraries\.