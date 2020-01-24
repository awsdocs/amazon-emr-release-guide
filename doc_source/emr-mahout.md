# Apache Mahout<a name="emr-mahout"></a>

Amazon EMR supports Apache Mahout, a machine learning framework for Apache Hadoop\. For more information about Mahout, go to [http://mahout\.apache\.org/](http://mahout.apache.org/)\.

Mahout is a machine learning library with tools for clustering, classification, and several types of recommenders, including tools to calculate most\-similar items or build item recommendations for users\. Mahout employs the Hadoop framework to distribute calculations across a cluster, and now includes additional work distribution methods, including Spark\.

For more information and an example of how to use Mahout with Amazon EMR, see the [Building a Recommender with Apache Mahout on Amazon EMR](https://aws.amazon.com/blogs/big-data/building-a-recommender-with-apache-mahout-on-amazon-elastic-mapreduce-emr/) post on the AWS Big Data blog\.

**Note**  
Only Mahout version 0\.13\.0 and later are compatible with Spark version 2\.x in Amazon EMR release version 5\.0\.0 and later\.

The following table lists the version of Mahout included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Mahout\.

For the version of components installed with Mahout in this release, see [Release 5\.29\.0 Component Versions](emr-release-5x.md#emr-5290-release)\.


**Mahout Version Information for emr\-5\.29\.0**  

| Amazon EMR Release Label | Mahout Version | Components Installed With Mahout | 
| --- | --- | --- | 
| emr\-5\.29\.0 | Mahout 0\.13\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, mahout\-client | 

**Topics**
+ [Mahout Release History](Mahout-release-history.md)