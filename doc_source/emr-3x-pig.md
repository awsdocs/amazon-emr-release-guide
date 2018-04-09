# Pig Application Specifics for Earlier AMI Versions of Amazon EMR<a name="emr-3x-pig"></a>

## Supported Pig Versions<a name="emr-3x-Pig_SupportedVersions"></a>

The Pig version you can add to your cluster depends on the version of the Amazon EMR AMI and the version of Hadoop you are using\. The table below shows which AMI versions and versions of Hadoop are compatible with the different versions of Pig\. We recommend using the latest available version of Pig to take advantage of performance enhancements and new functionality\. 

When you use the API to install Pig, the default version is used unless you specify `--pig-versions` as an argument to the step that loads Pig onto the cluster during the call to [RunJobFlow](http://docs.aws.amazon.com/ElasticMapReduce/latest/API/API_RunJobFlow.html)\. 


| Pig Version | AMI Version | Configuration Parameters | Pig Version Details | 
| --- | --- | --- | --- | 
| <a name="pig12"></a>0\.12\.0[Release Notes](http://pig.apache.org/releases.html#14+October%2C+2013%3A+release+0.12.0+available)[Documentation](http://pig.apache.org/docs/r0.12.0/) | 3\.1\.0 and later |  `--ami-version 3.1` `--ami-version 3.2` `--ami-version 3.3`  |  Adds support for the following: [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-pig.html)  | 
| <a name="pig1111"></a>0\.11\.1\.1[Release Notes](http://pig.apache.org/releases.html#1+April%2C+2013%3A+release+0.11.1+available)[Documentation](http://pig.apache.org/docs/r0.11.1/) | 2\.2 and later |  `--pig-versions 0.11.1.1` `--ami-version 2.2`  |  Improves performance of LOAD command with PigStorage if input resides in Amazon S3\.  | 
| <a name="pig0111"></a>0\.11\.1[Release Notes](http://pig.apache.org/releases.html#1+April%2C+2013%3A+release+0.11.1+available)[Documentation](http://pig.apache.org/docs/r0.11.1/) | 2\.2 and later |  `--pig-versions 0.11.1` `--ami-version 2.2`  |  Adds support for JDK 7, Hadoop 2, Groovy User Defined Functions, SchemaTuple optimization, new operators, and more\. For more information, see [Pig 0\.11\.1 Change Log](http://svn.apache.org/repos/asf/pig/tags/release-0.11.1/CHANGES.txt)\.  | 
| <a name="pig0922"></a>0\.9\.2\.2[Release Notes](http://pig.apache.org/releases.html#22+January%2C+2012%3A+release+0.9.2+available)[Documentation](http://pig.apache.org/docs/r0.9.2/index.html) | 2\.2 and later |  `--pig-versions 0.9.2.2` `--ami-version 2.2`  |  Adds support for Hadoop 1\.0\.3\.  | 
| <a name="pig0921"></a>0\.9\.2\.1[Release Notes](http://pig.apache.org/releases.html#22+January%2C+2012%3A+release+0.9.2+available)[Documentation](http://pig.apache.org/docs/r0.9.2/index.html) | 2\.2 and later |  `--pig-versions 0.9.2.1` `--ami-version 2.2`  |  Adds support for MapR\.  | 
| <a name="pig092"></a>0\.9\.2[Release Notes](http://pig.apache.org/releases.html#22+January%2C+2012%3A+release+0.9.2+available)[Documentation](http://pig.apache.org/docs/r0.9.2/index.html) | 2\.2 and later |  `--pig-versions 0.9.2` `--ami-version 2.2`  |  Includes several performance improvements and bug fixes\. For complete information about the changes for Pig 0\.9\.2, go to the [Pig 0\.9\.2 Change Log](http://svn.apache.org/repos/asf/pig/tags/release-0.9.2/CHANGES.txt)\.  | 
| <a name="pig091"></a>0\.9\.1[Release Notes](http://pig.apache.org/releases.html#5+October%2C+2011%3A+release+0.9.1+available)[Documentation](http://pig.apache.org/docs/r0.9.1/) | 2\.0 |  `--pig-versions 0.9.1` `--ami-version 2.0`  | 
| <a name="pig06"></a>0\.6[Release Notes](http://pig.apache.org/releases.html#1+March%2C+2010%3A+release+0.6.0+available) | 1\.0 |  `--pig-versions 0.6` `--ami-version 1.0`  | 
| <a name="pig03"></a>0\.3[Release Notes](http://pig.apache.org/releases.html#25+June%2C+2009%3A+release+0.3.0+available) | 1\.0 |  `--pig-versions 0.3` `--ami-version 1.0`  | 

## Pig Version Details<a name="emr-pig-version-details"></a>

Amazon EMR supports certain Pig releases that might have additional Amazon EMR patches applied\. You can configure which version of Pig to run on Amazon EMR clusters\. For more information about how to do this, see [Apache Pig](emr-pig.md)\. The following sections describe different Pig versions and the patches applied to the versions loaded on Amazon EMR\. 

### Pig Patches<a name="EnvironmentConfig_AMIPigPatches"></a>

This section describes the custom patches applied to Pig versions available with Amazon EMR\.

#### Pig 0\.11\.1\.1 Patches<a name="EnvironmentConfig_AMIPigPatches-0.11.1.1"></a>

The Amazon EMR version of Pig 0\.11\.1\.1 is a maintenance release that improves performance of LOAD command with PigStorage if the input resides in Amazon S3\.

#### Pig 0\.11\.1 Patches<a name="EnvironmentConfig_AMIPigPatches-0.11.1"></a>

The Amazon EMR version of Pig 0\.11\.1 contains all the updates provided by the Apache Software Foundation and the cumulative Amazon EMR patches from Pig version 0\.9\.2\.2\. However, there are no new Amazon EMR\-specific patches in Pig 0\.11\.1\.

#### Pig 0\.9\.2 Patches<a name="EnvironmentConfig_AMIPigPatches-0.9.2"></a>

Apache Pig 0\.9\.2 is a maintenance release of Pig\. The Amazon EMR team has applied the following patches to the Amazon EMR version of Pig 0\.9\.2\. 


| Patch | Description | 
| --- | --- | 
|  PIG\-1429  |   Add the Boolean data type to Pig as a first class data type\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-1429](https://issues.apache.org/jira/browse/PIG-1429)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.10   | 
|  PIG\-1824  |   Support import modules in Jython UDF\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-1824](https://issues.apache.org/jira/browse/PIG-1824)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.10   | 
|  PIG\-2010  |   Bundle registered JARs on the distributed cache\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-2010](https://issues.apache.org/jira/browse/PIG-2010)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.11   | 
|  PIG\-2456  |   Add a \~/\.pigbootup file where the user can specify default Pig statements\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-2456](https://issues.apache.org/jira/browse/PIG-2456)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.11   | 
|  PIG\-2623  |   Support using Amazon S3 paths to register UDFs\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-2623](https://issues.apache.org/jira/browse/PIG-2623)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.10, 0\.11   | 

#### Pig 0\.9\.1 Patches<a name="EnvironmentConfig_AMIPigPatches-0.9.1"></a>

The Amazon EMR team has applied the following patches to the Amazon EMR version of Pig 0\.9\.1\. 


| Patch | Description | 
| --- | --- | 
|  Support JAR files and Pig scripts in dfs  |   Add support for running scripts and registering JAR files stored in HDFS, Amazon S3, or other distributed file systems\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-1505](https://issues.apache.org/jira/browse/PIG-1505)\.   **Status:** Committed   **Fixed in Apache Pig Version:** 0\.8\.0   | 
|  Support multiple file systems in Pig  |   Add support for Pig scripts to read data from one file system and write it to another\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-1564](https://issues.apache.org/jira/browse/PIG-1564)\.   **Status:** Not Committed   **Fixed in Apache Pig Version:** n/a   | 
|  Add Piggybank datetime and string UDFs  |   Add datetime and string UDFs to support custom Pig scripts\. For more information, go to [https://issues\.apache\.org/jira/browse/PIG\-1565](https://issues.apache.org/jira/browse/PIG-1565)\.   **Status:** Not Committed   **Fixed in Apache Pig Version:** n/a   | 

## Interactive and Batch Pig Clusters<a name="emr-3x-pig-interactive-batch"></a>

Amazon EMR enables you to run Pig scripts in two modes:
+ Interactive
+ Batch

When you launch a long\-running cluster using the console or the AWS CLI, you can connect using ssh into the master node as the Hadoop user and use the Grunt shell to develop and run your Pig scripts interactively\. Using Pig interactively enables you to revise the Pig script more easily than batch mode\. After you successfully revise the Pig script in interactive mode, you can upload the script to Amazon S3 and use batch mode to run the script in production\. You can also submit Pig commands interactively on a running cluster to analyze and transform data as needed\.

In batch mode, you upload your Pig script to Amazon S3, and then submit the work to the cluster as a step\. Pig steps can be submitted to a long\-running cluster or a transient cluster\.