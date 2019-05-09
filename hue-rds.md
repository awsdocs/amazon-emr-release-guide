# Using Hue with a Remote Database in Amazon RDS<a name="hue-rds"></a>

By default, Hue user information and query histories are stored in a local MySQL database on the master node\. Alternatively, you can create one or more Hue\-enabled clusters using a configuration stored in Amazon S3 and a MySQL database in Amazon Relational Database Service\(Amazon RDS\)\. This allows you to persist user information and query history created by Hue without keeping your Amazon EMR cluster running\. We recommend using Amazon S3 server\-side encryption to store the configuration file\.

First create the remote database for Hue\.

**To create the external MySQL database**

1. Open the Amazon RDS console at [https://console\.aws\.amazon\.com/rds/](https://console.aws.amazon.com/rds/)\.

1. Click **Launch a DB Instance**\.

1. Choose MySQL and click **Select**\.

1. Leave the default selection of **Multi\-AZ Deployment and Provisioned IOPS Storage** and click **Next**\.

1. Leave the Instance Specifications at their defaults, specify Settings, and click **Next**\.

1. On the Configure Advanced Settings page, choose a proper security group and database name\. The security group you use must at least allow ingress TCP access for port 3306 from the master node of your cluster\. If you have not created your cluster at this point, you can allow all hosts to connect to port 3306 and adjust the security group after you have launched the cluster\. Click **Launch DB Instance**\.

1. From the RDS Dashboard, select **Instances** and select the instance you have just created\. When your database is available, make a note of the dbname, username, password, and RDS instance hostname\. You use this information when you create and configure your cluster\.

**To specify an external MySQL database for Hue when launching a cluster using the AWS CLI**

To specify an external MySQL database for Hue when launching a cluster using the AWS CLI, use the information you noted when creating your RDS instance for configuring `hue.ini` with a configuration object
**Note**  
You can create multiple clusters that use the same external database, but each cluster will share query history and user information\.
+ Using the AWS CLI, create a cluster with Hue installed, using the external database you created, and referencing a configuration file with a configuration classification for Hue that specifies the database properties\. The following example creates a cluster with Hue installed, referencing a configuration file in Amazon S3, `myConfig.json`, that specifies the database configuration\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --release-label emr-5.23.0 --applications Name=Hue Name=Spark Name=Hive \
  --instance-type m4.large --instance-count 3 \
  --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json --use-default-roles
  ```

  Example contents of the `myConfig.json` file are shown below\. Replace *dbname*, *username*, *password*, and *RDS instance hostname* with the values that you noted earlier in the RDS Dashboard\.

  ```
  [{
    "Classification": "hue-ini",
    "Properties": {},
    "Configurations": [
      {
        "Classification": "desktop",
        "Properties": {},
        "Configurations": [
          {
            "Classification": "database",
            "Properties": {
              "name": "dbname",
              "user": "username",
              "password": "password",
              "host": "RDS instance hostname",
              "port": "3306",
              "engine": "mysql"
            },
            "Configurations": []
          }
        ]
      }
    ]
  }]
  ```

## Troubleshooting<a name="hue-rds-troubleshoot"></a>

**In the event of Amazon RDS failover**  
It is possible users may encounter delays when running a query because the Hue database instance is non\-responsive or is in the process of failover\. The following are some facts and guidelines for this issue: 
+ If you login to the Amazon RDS console, you can search for failover events\. For example, to see if a failover is in process or has occurred, look for events such as "Multi\-AZ instance failover started" and "Multi\-AZ instance failover completed\."
+ It takes about 30 seconds for an RDS instance to complete a failover\.
+ If you are experiencing longer\-than\-normal responses for queries in Hue, try to re\-execute the query\.