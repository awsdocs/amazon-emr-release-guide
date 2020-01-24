# Using Oozie with a Remote Database in Amazon RDS<a name="oozie-rds"></a>

By default, Oozie user information and query histories are stored in a local MySQL database on the master node\. Alternatively, you can create one or more Oozie\-enabled clusters using a configuration stored in Amazon S3 and a MySQL database in Amazon Relational Database Service\(Amazon RDS\)\. This allows you to persist user information and query history created by Oozie without keeping your Amazon EMR cluster running\. We recommend using Amazon S3 server\-side encryption to store the configuration file\.

First, create the remote database for Oozie\.

**To create the external MySQL database**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Choose **Launch a DB Instance**\.

1. Choose MySQL and then choose **Select**\.

1. Leave the default selection of **Multi\-AZ Deployment and Provisioned IOPS Storage** and choose **Next**\.

1. Leave the Instance Specifications at their defaults, specify Settings, and choose **Next**\.

1. On the Configure Advanced Settings page, choose proper security group and database names\. The security group you use must at least allow inbound TCP access for port 3306 from the master node of your cluster\. If you have not created your cluster at this point, you can allow all hosts to connect to port 3306 and adjust the security group after you have launched the cluster\. Choose **Launch DB Instance**\.

1. From the RDS Dashboard, select **Instances** and select the instance you have just created\. When your database is available, make a note of the dbname, username, password, and RDS instance hostname\. You use this information when you create and configure your cluster\.

**To specify an external MySQL database for Oozie when launching a cluster using the AWS CLI**

To specify an external MySQL database for Oozie when launching a cluster using the AWS CLI, use the information you noted when creating your RDS instance for configuring `oozie-site` with a configuration object\.
**Note**  
You can create multiple clusters that use the same external database, but each cluster will share query history and user information\.
+ Using the AWS CLI, create a cluster with Oozie installed, using the external database you created, and referencing a configuration file with a configuration classification for Oozie that specifies the database properties\. The following example creates a cluster with Oozie installed, referencing a configuration file in Amazon S3, `myConfig.json`, that specifies the database configuration\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --release-label emr-5.29.0 --applications Name=Oozie Name=Spark Name=Hive \
  --instance-type m5.xlarge --instance-count 3 \
  --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json --use-default-roles
  ```

  Example contents of the `myConfig.json` file are shown below\. Replace *JDBC URL*, *username*, and *password* with the JDBC URL, user name, and password of your RDS instance\. 
**Important**  
The JDBC URL must include the database name as a suffix\. For example, jdbc:mysql://oozie\-external\-db\.xxxxxxxxxx\.us\-east\-1\.rds\.amazonaws\.com:3306/**dbname**\.

  ```
  [{
    "Classification": "oozie-site",
      "Properties": {
          "oozie.service.JPAService.jdbc.driver": "com.mysql.jdbc.Driver",
          "oozie.service.JPAService.jdbc.url": "JDBC URL",                               
          "oozie.service.JPAService.jdbc.username": "username",
          "oozie.service.JPAService.jdbc.password": "password"
      },
      "Configurations": []
  }]
  ```