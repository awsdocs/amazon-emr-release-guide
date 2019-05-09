# Transparent Encryption in HDFS on Amazon EMR<a name="emr-encryption-tdehdfs"></a>

Transparent encryption is implemented through the use of HDFS *encryption zones*, which are HDFS paths that you define\. Each encryption zone has its own key, which is stored in the key server specified using the `hdfs-site` configuration classification\.

Beginning with Amazon EMR release version 4\.8\.0, you can use Amazon EMR security configurations to configure data encryption settings for clusters more easily\. Security configurations offer settings to enable security for data in\-transit and data at\-rest in Amazon Elastic Block Store \(Amazon EBS\) storage volumes and EMRFS data in Amazon S3\. For more information, see [Encrypt Data in Transit and At Rest](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-data-encryption.html) in the *Amazon EMR Management Guide*\.

Amazon EMR uses the Hadoop KMS by default; however, you can use another KMS that implements the KeyProvider API operation\. Each file in an HDFS encryption zone has its own unique *data encryption key*, which is encrypted by the encryption zone key\. HDFS data is encrypted end\-to\-end \(at\-rest and in\-transit\) when data is written to an encryption zone because encryption and decryption activities only occur in the client\.

You cannot move files between encryptions zones or from an encryption zone to unencrypted paths\.

The NameNode and HDFS client interact with the Hadoop KMS \(or an alternate KMS you configured\) through the KeyProvider API operation\. The KMS is responsible for storing encryption keys in the backing keystore\. Also, Amazon EMR includes the JCE unlimited strength policy, so you can create keys at a desired length\. 

For more information, see [Transparent Encryption in HDFS](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/TransparentEncryption.html) in the Hadoop documentation\.

**Note**  
In Amazon EMR, KMS over HTTPS is not enabled by default with Hadoop KMS\. For more information about how to enable KMS over HTTPS, see the [Hadoop KMS documentation](http://hadoop.apache.org/docs/current/hadoop-kms/index.html)\.

## Configuring HDFS Transparent Encryption<a name="emr-configure-HDFS-transparent-encryption"></a>

You can configure transparent encryption by creating keys and adding encryption zones\. You can do this in several ways: 
+ Using the Amazon EMR configuration API operation when you create a cluster
+ Using a Hadoop JAR step with command\-runner\.jar
+ Logging in to the master node of the Hadoop cluster and using the `hadoop key` and `hdfs crypto` command line clients
+ Using the REST APIs for Hadoop KMS and HDFS

For more information about the REST APIs, see the respective documentation for Hadoop KMS and HDFS\.

**To create encryption zones and their keys at cluster creation using the CLI**

The hdfs\-encryption\-zones classification in the configuration API operation allows you to specify a key name and an encryption zone when you create a cluster\. Amazon EMR creates this key in Hadoop KMS on your cluster and configures the encryption zone\.
+ Create a cluster with the following command:

  ```
  aws emr create-cluster --release-label emr-5.23.0 --instance-type m4.large --instance-count 2 \
  --applications Name=App1 Name=App2 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
    {
      "Classification": "hdfs-encryption-zones",
      "Properties": {
        "/myHDFSPath1": "path1_key",
        "/myHDFSPath2": "path2_key"
      }
    }
  ]
  ```

**To create encryption zones and their keys manually on the master node**

1. Launch your cluster using an Amazon EMR release greater than 4\.1\.0\.

1. Connect to the master node of the cluster using SSH\.

1. Create a key within Hadoop KMS:

   ```
   $ hadoop key create path2_key
   path2_key has been successfully created with options Options{cipher='AES/CTR/NoPadding', bitLength=256, description='null', attributes=null}.
   KMSClientProvider[http://ip-x-x-x-x.ec2.internal:16000/kms/v1/] has been updated.
   ```
**Important**  
Hadoop KMS requires your key names to be lowercase\. If you use a key that has uppercase characters, then your cluster will fail during launch\.

1. Create the encryption zone path in HDFS:

   ```
   $ hadoop fs -mkdir /myHDFSPath2
   ```

1. Make the HDFS path an encryption zone using the key that you created:

   ```
   $ hdfs crypto -createZone -keyName path2_key -path /myHDFSPath2
   Added encryption zone /myHDFSPath2
   ```

**To create encryption zones and their keys manually using the AWS CLI**
+ Add steps to create the KMS keys and encryption zones manually with the following command:

  ```
  aws emr add-steps --cluster-id j-2AXXXXXXGAPLF --steps Type=CUSTOM_JAR,Name="Create First Hadoop KMS Key",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hadoop key create path1_key\""] \
  Type=CUSTOM_JAR,Name="Create First Hadoop HDFS Path",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hadoop fs -mkdir /myHDFSPath1\""] \
  Type=CUSTOM_JAR,Name="Create First Encryption Zone",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hdfs crypto -createZone -keyName path1_key -path /myHDFSPath1\""] \
  Type=CUSTOM_JAR,Name="Create Second Hadoop KMS Key",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hadoop key create path2_key\""] \
  Type=CUSTOM_JAR,Name="Create Second Hadoop HDFS Path",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hadoop fs -mkdir /myHDFSPath2\""] \
  Type=CUSTOM_JAR,Name="Create Second Encryption Zone",Jar="command-runner.jar",ActionOnFailure=CONTINUE,Args=[/bin/bash,-c,"\"hdfs crypto -createZone -keyName path2_key -path /myHDFSPath2\""]
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

## Considerations for HDFS Transparent Encryption<a name="emr-HDFS-transparent-encryption-considerations"></a>

A best practice is to create an encryption zone for each application where they may write files\. Also, you can encrypt all of HDFS by using the hdfs\-encryption\-zones classification in the configuration API and specify the root path \(/\) as the encryption zone\.

## Hadoop Key Management Server<a name="emr-hadoop-kms"></a>

[Hadoop KMS](http://hadoop.apache.org/docs/current/hadoop-kms/index.html) is a key management server that provides the ability to implement cryptographic services for Hadoop clusters, and can serve as the key vendor for [Transparent Encryption in HDFS on Amazon EMR](#emr-encryption-tdehdfs)\. Hadoop KMS in Amazon EMR is installed and enabled by default when you select the Hadoop application while launching an EMR cluster\. The Hadoop KMS does not store the keys itself except in the case of temporary caching\. Hadoop KMS acts as a proxy between the key provider and the client trustee to a backing keystore—it is not a keystore\. The default keystore that is created for Hadoop KMS is the Java Cryptography Extension KeyStore \(JCEKS\)\. The JCE unlimited strength policy is also included, so you can create keys with the desired length\. Hadoop KMS also supports a range of ACLs that control access to keys and key operations independently of other client applications such as HDFS\. The default key length in Amazon EMR is 256 bit\.

To configure Hadoop KMS, use the hadoop\-kms\-site classification to change settings\. To configure ACLs, you use the classification kms\-acls\.

For more information, see the [Hadoop KMS documentation](http://hadoop.apache.org/docs/current/hadoop-kms/index.html)\. Hadoop KMS is used in Hadoop HDFS transparent encryption\. To learn more about HDFS transparent encryption, see the [HDFS Transparent Encryption](http://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/TransparentEncryption.html) topic in the Apache Hadoop documentation\.

**Note**  
In Amazon EMR, KMS over HTTPS is not enabled by default with Hadoop KMS\. To learn how to enable KMS over HTTPS, see the [Hadoop KMS documentation](http://hadoop.apache.org/docs/current/hadoop-kms/index.html)\.

**Important**  
Hadoop KMS requires your key names to be lowercase\. If you use a key that has uppercase characters, then your cluster will fail during launch\.

### Configuring Hadoop KMS in Amazon EMR<a name="emr-hadoop-kms-configure"></a>

Using Amazon EMR release version 4\.6\.0 or later, the `kms-http-port` is 9700 and `kms-admin-port` is 9701\.

You can configure Hadoop KMS at cluster creation time using the configuration API for Amazon EMR releases\. The following are the configuration object classifications available for Hadoop KMS:


**Hadoop KMS Configuration Classifications**  

| Classification | Filename | 
| --- | --- | 
| hadoop\-kms\-site | kms\-site\.xml | 
| hadoop\-kms\-acls | kms\-acls\.xml | 
| hadoop\-kms\-env | kms\-env\.sh | 
| hadoop\-kms\-log4j | kms\-log4j\.properties | 

**To set Hadoop KMS ACLs using the CLI**
+ Create a cluster with Hadoop KMS with ACLs using the following command:

  ```
  aws emr create-cluster --release-label emr-5.23.0 --instance-type m4.large --instance-count 2 \
  --applications Name=App1 Name=App2 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
      {
        "Classification": "hadoop-kms-acls",
        "Properties": {
          "hadoop.kms.blacklist.CREATE": "hdfs,foo,myBannedUser",
          "hadoop.kms.acl.ROLLOVER": "myAllowedUser"       
        }
      }
    ]
  ```

**To disable Hadoop KMS cache using the CLI**
+ Create a cluster with Hadoop KMS `hadoop.kms.cache.enable` set to `false`, using the following command:

  ```
  aws emr create-cluster --release-label emr-5.23.0 --instance-type m4.large --instance-count 2 \
  --applications Name=App1 Name=App2 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
      {
        "Classification": "hadoop-kms-site",
        "Properties": {
          "hadoop.kms.cache.enable": "false"
        }
      }
    ]
  ```

**To set environment variables in the `kms-env.sh` script using the CLI**
+ Change settings in `kms-env.sh` via the `hadoop-kms-env` configuration\. Create a cluster with Hadoop KMS using the following command:

  ```
  aws emr create-cluster --release-label emr-5.23.0 --instance-type m4.large --instance-count 2 \
  --applications Name=App1 Name=App2 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json
  ```
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  `myConfig.json`:

  ```
  [
    {
      "Classification": "hadoop-kms-env",
      "Properties": {     
      },
      "Configurations": [
        {
          "Classification": "export",
          "Properties": {
            "JAVA_LIBRARY_PATH": "/path/to/files",
            "KMS_SSL_KEYSTORE_FILE": "/non/Default/Path/.keystore",
            "KMS_SSL_KEYSTORE_PASS": "myPass"
          },
          "Configurations": [        
          ]
        }
      ]
    }
  ]
  ```

For information about configuring Hadoop KMS, see the [Hadoop KMS documentation](http://hadoop.apache.org/docs/current/hadoop-kms/index.html)\.