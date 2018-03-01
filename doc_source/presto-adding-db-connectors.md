# Adding Database Connectors<a name="presto-adding-db-connectors"></a>

You can add JDBC connectors at cluster launch using the configuration classifications\. For more information about connectors, see [https://prestodb\.io/docs/current/connector\.html](https://prestodb.io/docs/current/connector.html)\. 

These classifications are named as follows:

+ presto\-connector\-blackhole

+ presto\-connector\-cassandra

+ presto\-connector\-hive

+ presto\-connector\-jmx

+ presto\-connector\-kafka

+ presto\-connector\-localfile

+ presto\-connector\-mongodb

+ presto\-connector\-mysql

+ presto\-connector\-postgresql

+ presto\-connector\-raptor

+ presto\-connector\-redis

+ presto\-connector\-tpch

**Example Configuring a Cluster with the PostgreSQL JDBC**  
To launch a cluster with the PostgreSQL connector installed and configured, create a file, `myConfig.json`, with the following content:  

```
[
  {
    "Classification": "presto-connector-postgresql",
    "Properties": {
      "connection-url": "jdbc:postgresql://example.net:5432/database",
      "connection-user": "MYUSER",
      "connection-password": "MYPASS"
    },
    "Configurations": []
  }
]
```
Use the following command to create the cluster:  

```
aws emr create-cluster --name PrestoConnector --release-label emr-5.12.0 --instance-type m3.xlarge \
--instance-count 2 --applications Name=Hadoop Name=Hive Name=Pig Name=Presto \
--use-default-roles --no-auto-terminate --ec2-attributes KeyName=myKey \
--log-uri s3://my-bucket/logs --enable-debugging \
--configurations file://./myConfig.json
```