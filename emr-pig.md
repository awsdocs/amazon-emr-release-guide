# Apache Pig<a name="emr-pig"></a>

Apache Pig is an open\-source Apache library that runs on top of Hadoop, providing a scripting language that you can use to transform large data sets without having to write complex code in a lower level computer language like Java\. The library takes SQL\-like commands written in a language called Pig Latin and converts those commands into Tez jobs based on directed acyclic graphs \(DAGs\) or MapReduce programs\. Pig works with structured and unstructured data in a variety of formats\. For more information about Pig, see [http://pig\.apache\.org/](http://pig.apache.org/)\.

You can execute Pig commands interactively or in batch mode\. To use Pig interactively, create an SSH connection to the master node and submit commands using the Grunt shell\. To use Pig in batch mode, write your Pig scripts, upload them to Amazon S3, and submit them as cluster steps\. For more information on submitting work to a cluster, see [Submit Work to a Cluster](https://docs.aws.amazon.com/emr/latest/ManagementGuide/AddingStepstoaJobFlow.html) in the *Amazon EMR Management Guide*\.

 When you use Pig to write output to an HCatalog table in Amazon S3, disable Amazon EMR direct write by setting the `mapred.output.direct.NativeS3FileSystem` and `mapred.output.direct.EmrFileSystem` properties to `false`\. For more information, see [Using HCatalog](emr-hcatalog-using.md)\. Within a Pig script, you can use the `SET mapred.output.direct.NativeS3FileSystem false` and `SET mapred.output.direct.EmrFileSystem false` commands\.

The following table lists the version of Pig included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Pig\.

For the version of components installed with Pig in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**Pig Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | Pig Version | Components Installed With Pig | 
| --- | --- | --- | 
| emr\-5\.23\.0 | Pig 0\.17\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, pig\-client, tez\-on\-yarn | 

**Topics**
+ [Submit Pig Work](emr-pig-launch.md)
+ [Call User Defined Functions from Pig](emr-pig-udf.md)
+ [Pig Release History](Pig-release-history.md)