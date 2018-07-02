# What's New?<a name="emr-whatsnew"></a>

This topic covers features and issues resolved in the current release of Amazon EMR\. These release notes are also available on the [Release 5\.15\.0 Tab](emr-release-5x.md#emr-5150-release), along with the application versions, component versions, and available configuration classifications for this release\.

Subscribe to the RSS feed for Amazon EMR release notes at [http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

For earlier\-version release notes back to release version 4\.2\.0, see [Amazon EMR What's New History](emr-whatsnew-history.md)\.

## Release 5\.15\.0 \(Latest\)<a name="emr-5150-whatsnew"></a>

The following release notes include information for Amazon EMR release version 5\.15\.0\. Changes are relative to 5\.14\.0\.

Initial release date: June 21, 2018

**Upgrades**
+ Upgraded HBase to 1\.4\.4
+ Upgraded Hive to 2\.3\.3
+ Upgraded Hue to 4\.2\.0
+ Upgraded Oozie to 5\.0\.0
+ Upgraded Zookeeper to 3\.4\.12
+ Upgraded AWS SDK to 1\.11\.333

**Changes, Enhancements, and Resolved Issues**
+ Hive
  + Backported [HIVE\-18069](https://issues.apache.org/jira/browse/HIVE-18069)
+ Hue
  + Updated Hue to correctly authenticate with Livy when Kerberos is enabled\. Livy is now supported when using Kerberos with Amazon EMR\.
+ JupyterHub
  + Updated JupyterHub so that Amazon EMR installs LDAP client libraries by default\.
  + Fixed an error in the script that generates self\-signed certificates\. For more information about the issue, see [Release Notes](emr-release-5x.md#emr-5140-relnotes)