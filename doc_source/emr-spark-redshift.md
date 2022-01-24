# Use Spark on Amazon Redshift with a connector<a name="emr-spark-redshift"></a>

With Amazon EMR release versions 6\.4\.0 and later, every Amazon EMR cluster created with Apache Spark includes a connector between Spark and Amazon Redshift\. This connector allows you to easily use Spark on Amazon EMR to process data stored in Amazon Redshift\.

The connector is based on the `spark-redshift` open\-source connector, which you can find on [Github](https://github.com/spark-redshift-community/spark-redshift/blob/master/tutorial/SparkRedshiftTutorial.scala)\. This connector is installed on each Amazon EMR cluster as a library used by Spark\.

To get started with this connector and learn about the supported parameters, please refer to the [README file](https://github.com/spark-redshift-community/spark-redshift/blob/master/README.md) on the `spark-redshift` Github repository\. The repository also includes a [tutorial](https://github.com/spark-redshift-community/spark-redshift/blob/master/tutorial/SparkRedshiftTutorial.scala) for those new to Amazon Redshift\.

Amazon EMR always reviews open\-source code when importing it into your cluster\. Due to security concerns, we don't support the following authentication methods from Spark to Amazon S3: 
+ Setting AWS access keys in the `hadoop-env` configuration classification
+ Encoding AWS access keys in the `tempdir` URI

## Considerations and limitations<a name="emr-spark-redshift-considerations"></a>
+ The parameter `tempformat` currently doesn't support the Parquet format\.
+ The `tempdir` URI points to an Amazon S3 location\. This temp directory is not cleaned up automatically and hence could add additional cost\. We recommend using [Amazon S3 lifecycle policies](https://docs.aws.amazon.com/AmazonS3/latest/userguide/object-lifecycle-mgmt.html) to define the retention rules for the Amazon S3 bucket\.
+ We recommend using [Amazon S3 server\-side encryption](https://docs.aws.amazon.com/AmazonS3/latest/userguide/serv-side-encryption.html) to encrypt the Amazon S3 buckets used\.
+ We recommend [blocking public access to Amazon S3 buckets](https://docs.aws.amazon.com/AmazonS3/latest/userguide/access-control-block-public-access.html)\.
+ We recommend that the Amazon Redshift cluster should not be publicly accessible\.
+ We recommend enabling [Amazon Redshift audit logging](https://docs.aws.amazon.com/redshift/latest/mgmt/db-auditing.html)\.
+ We recommend enabling [Amazon Redshift at\-rest encryption](https://docs.aws.amazon.com/redshift/latest/mgmt/security-server-side-encryption.html)\.
+ We recommend enabling SSL for the JDBC connection from Spark on Amazon EMR to Amazon Redshift\.
+ We recommend passing an IAM role using the parameter `aws_iam_role` for the Amazon Redshift authentication parameter\.
+  We recommend managing Amazon Redshift credentials \(username and password for the Amazon Redshift cluster\) in AWS Secrets Manager as a best practice\. The code sample below shows how you can use AWS Secrets Manager to retrieve credentials to connect to an Amazon Redshift cluster using pyspark: 

  ```
  from pyspark.sql import SQLContext
  import boto3
  
  sc = # existing SparkContext
  sql_context = SQLContext(sc)
  
  secretsmanager_client = boto3.client('secretsmanager')
  secret_manager_response = secretsmanager_client.get_secret_value(
      SecretId='string',
      VersionId='string',
      VersionStage='string'
  )
  username = # get username from secret_manager_response
  password = # get password from secret_manager_response
  url = "jdbc:redshift://redshifthost:5439/database?user=" + username + "&password=" + password
  
  # Read data from a table
  df = sql_context.read \
      .format("io.github.spark_redshift_community.spark.redshift") \
      .option("url", url) \
      .option("dbtable", "my_table") \
      .option("tempdir", "s3://path/for/temp/data") \
      .load()
  ```