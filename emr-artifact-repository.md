# Checking Dependencies Using the Amazon EMR Artifact Repository<a name="emr-artifact-repository"></a>

You can use the Amazon EMR artifact repository to build Apache Hive and Apache Hadoop job code against the exact versions of libraries and dependencies that are available with specific Amazon EMR release versions, beginning with Amazon EMR release version 5\.18\.0\. Building against Amazon EMR artifacts in the repository helps avoid runtime class path issues by ensuring that the versions of the libraries that the job is built against are exactly the same versions provided at runtime on the cluster\. Currently, Amazon EMR artifacts are only available for Maven builds\.

To access the artifact repository, add the repository URL to your Maven settings file or to a specific project's `pom.xml` configuration file\. You can then specify the dependencies in your project configuration\. For dependency versions, use the version listed under *Component Versions* for the desired release on [Amazon EMR 5\.x Release Versions](emr-release-5x.md)\. For example, component versions for the most recent Amazon EMR release are available at [Component Versions](emr-release-5x.md#emr-5230-components)\. If an artifact for your project is not listed under *Component Versions*, specify the version that is listed for Hive and Hadoop in that release\. For example, for Hadoop components in Amazon EMR release version 5\.18\.0, the version is `2.8.4-amzn-1`\.

The artifact repository URL has the following syntax:

```
https://s3-endpoint/region-ID-emr-artifacts/emr-release-label/repos/maven/
```
+ *s3\-endpoint* is the Amazon Simple Storage Service \(Amazon S3\) endpoint of the region for the repository and *region\-ID* is the corresponding region\. For example, `s3.us-west-1.amazonaws.com` and `us-west-1`\. For more information, see Amazon S3 endpoints in the *Amazon Web Services General Reference*\. There is no difference in artifacts between regions, so you can specify the most convenient region for your development environment\.
+ *emr\-release\-label* is the release label for the Amazon EMR cluster that will run your code\. Release labels are in the form `emr-x.x.x. For example, emr-5.23.0.` 

**Example Configuration for Maven pom\.xml**  

The pom\.xml example below configures a Maven project to build against the emr\-5\.18\.0 Apache Hadoop and Apache Hive artifacts, using the artifact repository in us\-west\-1\. Snapshot versions are not available in the artifact repository, so snapshots are disabled in the pom\.xml\. Ellipses \(*\.\.\.*\) in the example below indicate omission of other configuration parameters\. Do not copy these into your Maven project\.

```
<project>
	...
	<repositories>
		...
		<repository>
			<id>emr-5.18.0-artifacts</id>
			<name>EMR 5.18.0 Releases Repository</name>
			<releases>
				<enabled>true</enabled>
			</releases>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
			<url>https://s3.us-west-1.amazonaws.com/us-west-1-emr-artifacts/emr-5.18.0/repos/maven/</url>
		</repository>
		...
	</repositories>
	...
	<dependencies>
		...
		<dependency>
			<groupId>org.apache.hive</groupId>
			<artifactId>hive-exec</artifactId>
			<version>2.3.3-amzn-2</version>
		</dependency>
		<dependency>
			<groupId>org.apache.hadoop</groupId>
			<artifactId>hadoop-common</artifactId>
			<version>2.8.4-amzn-1</version>
		</dependency>
		...
	</dependencies>
	
</project>
```