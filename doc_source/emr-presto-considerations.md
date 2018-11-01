# Considerations with Presto on Amazon EMR<a name="emr-presto-considerations"></a>

Consider the following differences and limitations when you run [Presto](https://aws.amazon.com/big-data/what-is-presto/) on Amazon EMR\.

## Presto Command Line Executable<a name="emr-presto-command-line-cli"></a>

In Amazon EMR, the Presto command line executable is `presto-cli`\. For example:

```
presto-cli --catalog hive
```

## Some Presto Deployment Properties not Configurable<a name="emr-presto-deployment-config"></a>

Depending on the version of Amazon EMR that you use, some Presto deployment configurations may not be available\. For more information about these properties, see [Deploying Presto](https://prestodb.io/docs/current/installation/deployment.html) in Presto Documentation\. The following table shows the configuration status for Presto `properties` files\.


| File | Configurable | 
| --- | --- | 
|  `log.properties`  |  Configurable in all Amazon EMR release versions\. Use the `presto-log` configuration classification in Amazon EMR release version 4\.0\.0 and later\.  | 
|  `config.properties`  |  Configurable in all Amazon EMR release versions\. Use the `presto-config` configuration classification in Amazon EMR release version 4\.0\.0 and later\.  | 
|  `hive.properties`  |  Configurable in Amazon EMR release version 4\.1\.0 and later\. Use the `presto-connector-hive` configuration classification\.  | 
|  `node.properties`  |  Configurable in Amazon EMR release version 5\.6\.0 and later\. Use the `presto-node` configuration classification\.  | 
|  `jvm.config`  |  Not configurable\.  | 

## EMRFS and PrestoS3FileSystem Configuration<a name="emr-presto-prestos3"></a>

With Amazon EMR release version 5\.12\.0 and later, Presto can use EMRFS, and this is the default configuration\. For more information, see [Using EMR File System \(EMRFS\)](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-fs.html) in the *Amazon EMR Management Guide*\. With earlier release versions, PrestoS3FileSystem is the only option\.

Using EMRFS has benefits\. You can use a security configuration to set up encryption for EMRFS data in Amazon S3\. You can also use IAM roles for EMRFS requests to Amazon S3\. For more information, see [Understanding Encryption Options](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-data-encryption-options.html) and [Configure IAM Roles for EMRFS Requests to Amazon S3](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-emrfs-iam-roles.html) in the *Amazon EMR Management Guide*\.

**Note**  
A configuration issue can cause Presto errors when querying underlying data in Amazon S3 with Amazon EMR release version 5\.12\.0\. This is because Presto fails to pick up configuration classification values from `emrfs-site.xml`\. As a workaround, create an `emrfs` subdirectory under `usr/lib/presto/plugin/hive-hadoop2/`, create a symlink in `usr/lib/presto/plugin/hive-hadoop2/emrfs` to the existing `/usr/share/aws/emr/emrfs/conf/emrfs-site.xml` file, and then restart the presto\-server process \(`sudo presto-server stop` followed by `sudo presto-server start`\)\.

You can override the EMRFS default and use the PrestoS3FileSystem instead\. To do this, use the `presto-connector-hive` configuration classification to set `hive.s3-file-system-type` to `PRESTO` as shown in the following example\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

```
[
   {
      "Classification": "presto-connector-hive",
      "Properties": {
         "hive.s3-file-system-type": "PRESTO"
      }
   }
]
```

If you use PrestoS3FileSystem, use the `presto-connector-hive` configuration classification to configure PrestoS3FileSystem properties\. For more information about available properties, see [Amazon S3 Configuration](https://prestodb.io/docs/current/connector/hive.html#amazon-s3-configuration) in the Hive Connector section of Presto documentation\. These settings do not apply to EMRFS\.

## Default Setting for End User Impersonation<a name="emr-presto-end-user-impersonation"></a>

By default, Amazon EMR version 5\.12\.0 and later enables end user impersonation for accessing HDFS\. For more information, see [End User Impersonation](https://prestodb.io/docs/current/connector/hive-security.html#end-user-impersonation) in the Presto documentation\. You can change this setting using the `presto-config` configuration classification to set the `hive.hdfs.impersonation.enabled` property to `false`\.

## Default Port for Presto Web Interface<a name="emr-presto-default-web-port"></a>

By default, Amazon EMR configures the Presto web interface on the Presto coordinator to use port 8889\. You can change this using the `presto-config` configuration classification to set the `http-server.http.port` property\. For more information, see [Config Properties](https://prestodb.io/docs/current/installation/deployment.html#config-properties) in the Deploying Presto section of Presto Documentation\.

## Issue with Hive Bucket Execution in Some Releases<a name="emr-presto-bucket-execution"></a>

Presto version 152\.3 has an issue with Hive bucket execution that causes significantly slower Presto query performance in some circumstances\. This version is included with Amazon EMR release versions 5\.0\.3, 5\.1\.0, and 5\.2\.0\. To mitigate this issue, use the `presto-connector-hive` configuration classification to set the `hive.bucket-execution` property to `false` as shown in the following example\.

```
[
   {
      "Classification": "presto-connector-hive",
      "Properties": {
         "hive.bucket-execution": "false"
      }
   }
]
```