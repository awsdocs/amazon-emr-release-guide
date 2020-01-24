# Adding Database Connectors<a name="presto-adding-db-connectors"></a>

You can use configuration classifications to configure JDBC connector properties when you create a cluster\. Configuration classifications begin with `presto-connector`, for example, `presto-connector-postgresql`\. The available configuration classifications depend on the Amazon EMR release version\. For the configuration classifications available with the most recent release version, see [Configuration Classifications](emr-release-5x.md#emr-5290-class) for Amazon EMR 5\.29\.0\. If you are using a different version of Amazon EMR, see [Amazon EMR 5\.x Release Versions](emr-release-5x.md) for the configuration classifications\. For more information about the properties that can be configured with each connector, see [https://prestodb\.io/docs/current/connector\.html](https://prestodb.io/docs/current/connector.html)\. 

**Example —Configuring a Cluster with the PostgreSQL JDBC Connector**  
To launch a cluster with the PostgreSQL connector installed and configured, first create a JSON file that specifies the configuration classification—for example, `myConfig.json`—with the following content, and save it locally\.  
Replace the connection properties as appropriate for your setup and as shown in the [PostgreSQL Connector](https://prestodb.io/docs/current/connector/postgresql.html) topic in Presto Documentation\.  

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
When you create the cluster, reference the path to the JSON file using the `--configurations` option as shown in the following example, where `myConfig.json` is in the same directory where you run the command:  

```
aws emr create-cluster --name PrestoConnector --release-label emr-5.29.0 --instance-type m5.xlarge \
--instance-count 2 --applications Name=Hadoop Name=Hive Name=Pig Name=Presto \
--use-default-roles --ec2-attributes KeyName=myKey \
--log-uri s3://my-bucket/logs --enable-debugging \
--configurations file://myConfig.json
```