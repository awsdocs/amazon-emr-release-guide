# About Amazon EMR Releases<a name="emr-release-components"></a>

An Amazon EMR release is a set of open\-source applications from the big\-data ecosystem\. Each release comprises different big\-data applications, components, and features that you select to have Amazon EMR install and configure when you create a cluster\. Applications are packaged using a system based on [Apache BigTop](http://bigtop.apache.org/), which is an open\-source project associated with the Hadoop ecosystem\. This guide provides information for applications included in Amazon EMR releases\.

For more information about getting started and working with Amazon EMR, see the [Amazon EMR Management Guide](https://docs.aws.amazon.com/emr/latest/ManagementGuide/)\.

When you launch a cluster, you can choose from multiple release versions of Amazon EMR\. This allows you to test and use application versions that fit your compatibility requirements\. You specify the release version using the *release label*\. Release labels are in the form `emr-x.x.x. For example, emr-5.29.0.`

Beginning with Amazon EMR 5\.18\.0, you can use the Amazon EMR artifact repository to build your job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions\. For more information, see [Checking Dependencies Using the Amazon EMR Artifact Repository](emr-artifact-repository.md)\.

Subscribe to the RSS feed for Amazon EMR release notes at [https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/amazon-emr-release-notes.rss) to receive updates when a new Amazon EMR release version is available\.

**Latest Amazon EMR release** details, including application versions, release notes, components, and configuration classifications:
+ [Amazon EMR Release 5\.29\.0](emr-release-5x.md#emr-5290-release)
**Note**  
New Amazon EMR release versions are made available in different regions over a period of several days, beginning with the first region on the initial release date\. The latest release version may not be available in your region during this period\.

**Release notes** for the latest Amazon EMR releases and a history of all releases:
+ [What's New?](emr-whatsnew.md)
+ [Amazon EMR What's New History](emr-whatsnew-history.md)

**A comprehensive history of application versions** in each Amazon EMR release:
+ [Application Versions in Amazon EMR 5\.x Releases \(PNG\)](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/emr-releases-5x.png)
+ [Application Versions in Amazon EMR 4\.x Releases \(PNG\)](https://docs.aws.amazon.com//emr/latest/ReleaseGuide/images/emr-releases-4x.png)

**Details for each Amazon EMR release** and differences between release series, where applicable:
+ [Amazon EMR 5\.x Release Versions](emr-release-5x.md)
+ [Amazon EMR 4\.x Release Versions](emr-release-4x.md)
+ [Amazon EMR 2\.x and 3\.x AMI Versions](emr-release-3x.md)