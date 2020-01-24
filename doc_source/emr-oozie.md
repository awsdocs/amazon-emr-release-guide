# Apache Oozie<a name="emr-oozie"></a>

Use the Apache Oozie Workflow Scheduler to manage and coordinate Hadoop jobs\. For more information, see [http://oozie\.apache\.org/](http://oozie.apache.org/)\.

The Oozie native web interface is not supported on Amazon EMR\. To use a front\-end interface for Oozie, try the Hue Oozie application\. For more information, see [Hue](emr-hue.md)\. Oozie is included with Amazon EMR release version 5\.0\.0 and later\. Oozie is included as a sandbox application in earlier releases\. For more information, see [Amazon EMR 4\.x Release Versions](emr-release-4x.md)\.

If you use a custom Amazon Linux AMI based on an Amazon Linux AMI with a creation date of 2018\-08\-11, the Oozie server fails to start\. If you use Oozie, create a custom AMI based on an Amazon Linux AMI ID with a different creation date\. You can use the following AWS CLI command to return a list of Image IDs for all HVM Amazon Linux AMIs with a 2018\.03 version, along with the release date, so that you can choose an appropriate Amazon Linux AMI as your base\. Replace MyRegion with your region identifier, such as us\-west\-2\.

```
aws ec2 --region MyRegion describe-images --owner amazon --query 'Images[?Name!=`null`]|[?starts_with(Name, `amzn-ami-hvm-2018.03`) == `true`].[CreationDate,ImageId,Name]' --output text | sort -rk1
```

The following table lists the version of Oozie included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with Oozie\.

For the version of components installed with Oozie in this release, see [Release 5\.29\.0 Component Versions](emr-release-5x.md#emr-5290-release)\.


**Oozie Version Information for emr\-5\.29\.0**  

| Amazon EMR Release Label | Oozie Version | Components Installed With Oozie | 
| --- | --- | --- | 
| emr\-5\.29\.0 | Oozie 5\.1\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, oozie\-client, oozie\-server, tez\-on\-yarn | 

**Topics**
+ [Using Oozie with a Remote Database in Amazon RDS](oozie-rds.md)
+ [Oozie Release History](Oozie-release-history.md)