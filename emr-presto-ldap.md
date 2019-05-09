# Using LDAP Authentication for Presto on Amazon EMR<a name="emr-presto-ldap"></a>

Follow the steps in this section to configure LDAP\. See each step for examples and links to more information\.

**Topics**
+ [Step 1: Gather information about your LDAP server and copy the server certificate to Amazon S3](#emr-presto-ldap-server-prereq)
+ [Step 2: Set up a security configuration](#emr-presto-ldap-seccfg)
+ [Step 3: Create a configuration JSON with Presto properties for LDAP](#emr-presto-ldap-prestoconfig)
+ [Step 4: Create the script to copy the LDAP server certificate and upload it to Amazon S3](#emr-presto-ldap-servercert)
+ [Step 5: Create the cluster](#emr-presto-ldap-createcluster)

## Step 1: Gather information about your LDAP server and copy the server certificate to Amazon S3<a name="emr-presto-ldap-server-prereq"></a>

You'll need the information and items in the following section from your LDAP server to configure LDAP authentication\.

### The IP Address or host name of the LDAP Server<a name="w3aac47c21c13b7b5"></a>

The Presto coordinator on the Amazon EMR master node must be able to reach the LDAP server at the specified IP address or host name\. By default, Presto communicates with the LDAP server using LDAPS over port 636\. If your LDAP implementation requires a custom port, you can specify it using the `ldap.url` property with Amazon EMR 5\.16\.0 or later, or using `authentication.ldap.url` with earlier versions\. Substitute the custom port for `636` as shown in the `presto-config` configuration classification examples in [Step 3: Create a configuration JSON with Presto properties for LDAP](#emr-presto-ldap-prestoconfig)\. Ensure that any firewalls and security groups allow inbound and outbound traffic on port 636 \(or your custom port\) and also port 8446 \(or your custom port\), which is used for internal cluster communications\.

### The LDAP server certificate<a name="w3aac47c21c13b7b7"></a>

You must upload the certificate file to a secure location in Amazon S3\. For more information, see [How do I Upload Files and Folders to an S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/upload-objects.html) in the *Amazon Simple Storage Service Console User Guide*\. You create a bootstrap action that copies this certificate from Amazon S3 to each node in the cluster when the cluster launches\. In [Step 4: Create the script to copy the LDAP server certificate and upload it to Amazon S3](#emr-presto-ldap-servercert)\. The example certificate is *s3://MyBucket/ldap\_server\.crt*\.

### The LDAP server's settings for anonymous binding<a name="w3aac47c21c13b7b9"></a>

If anonymous binding is disabled, you need the user ID \(UID\) and password of an account with permissions to bind to the LDAP server so that the Presto server can establish a connection\. You specify the UID and password using the `internal-communication.authentication.ldap.user` and `internal-communication.authentication.ldap.password` properties in the `presto-config` configuration classification\. Amazon EMR 5\.10\.0 does not support these settings, so anonymous binding must be supported on the LDAP server when you use this release version\.

**To get the status of anonymous binding on the LDAP server**
+ Use the [ldapwhoami](https://linux.die.net/man/1/ldapwhoami) command from a Linux client, as shown in the following example:

  ```
  ldapwhoami -x -H ldaps://LDAPServerHostNameOrIPAddress
  ```

  If anonymous binding is not allowed, the command returns the following:

  ```
  ldap_bind: Inappropriate authentication (48)
  additional info: anonymous bind disallowed
  ```

**To verify that an account has permissions to an LDAP server that uses simple authentication**
+ Use the[ldapwhoami](https://linux.die.net/man/1/ldapwhoami) command from a Linux client, as shown in the following example\. The example uses a fictitious user, *presto*, stored in an Open LDAP server running on an EC2 instance with the fictitious host name *ip\-xxx\-xxx\-xxx\-xxx\.ec2\.internal*\. The user is associated with the organizational unit \(OU\) *admins* and with the password *123456*:

  ```
  ldapwhoami -x -w "123456" -D uid=presto,ou=admins,dc=ec2,dc=internal -H ldaps://ip-xxx-xxx-xxx-xxx.ec2.internal 
  ```

  If the account is valid and has appropriate permissions, the command returns:

  ```
  dn:uid=presto,ou=admins,dc=ec2,dc=internal
  ```

The example configurations in [Step 3: Create a configuration JSON with Presto properties for LDAP](#emr-presto-ldap-prestoconfig) include this account for clarity, with the exception of the 5\.10\.0 example, where it is not supported\. If the LDAP server uses anonymous binding, remove the `internal-communication.authentication.ldap.user` and `internal-communication.authentication.ldap.password` name/value pairs\.

### The LDAP distinguished name \(DN\) for Presto users<a name="w3aac47c21c13b7c11"></a>

When you specify the LDAP configuration for Presto, you specify a bind pattern that consists of `${USER}` along with an organizational unit \(OU\) and additional domain components \(DCs\)\. Presto replaces `${USER}` with the actual User ID \(UID\) of each user during password authentication to match the distinguished name \(DN\) that this bind pattern specifies\. You need the OUs that eligible users belong to and their DCs\. For example, to allow users from the `admins` OU in the `corp.example.com` domain to authenticate to Presto, you specify `${USER},ou=admins,dc=corp,dc=example,dc=com` as the user bind pattern\.

When using Amazon EMR 5\.10\.0, you can specify only one such pattern\. Using Amazon EMR 5\.11\.0 or later, you can specify multiple patterns separated by a colon \(:\)\. Users attempting to authenticate to Presto are compared to the first pattern, then the second, and so on\. For an example, see [Step 3: Create a configuration JSON with Presto properties for LDAP](#emr-presto-ldap-prestoconfig)\.

## Step 2: Set up a security configuration<a name="emr-presto-ldap-seccfg"></a>

Create a security configuration with in\-transit encryption enabled\. For more information, see [Create a Security Configuration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-create-security-configuration.html) in the *Amazon EMR Management Guide*\. The encryption artifacts that you provide when you set up in\-transit encryption are used to encrypt internal communication between Presto nodes\. For more information, see [Providing Certificates for In\-Transit Data Encryption](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-encryption-enable.html#emr-encryption-certificates)\. The LDAP server certificate is used to authenticate client connections to the Presto server\.

## Step 3: Create a configuration JSON with Presto properties for LDAP<a name="emr-presto-ldap-prestoconfig"></a>

You use the `presto-config` configuration classification to set Presto properties for LDAP\. The format and contents of `presto-config` are slightly different depending on the Amazon EMR release version you use\. Examples of configuration differences are provided later in this section\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

The following steps assume that you save the JSON to a file, *MyPrestoConfig\.json*\. If you use the console, upload the file to a secure location in Amazon S3 so that you can reference it when you create the cluster\. If you use the AWS CLI, you can reference the file locally\.

**Example Amazon EMR 5\.16\.0 and later**  
The following example uses the LDAP user ID and password, and the LDAP host name from [Step 1: Gather information about your LDAP server and copy the server certificate to Amazon S3](#emr-presto-ldap-server-prereq) to authenticate to the LDAP server for binding\. Two user bind patterns are specified, which indicates that users within the `admins` OU and the `datascientists` OU on the LDAP server are eligible for authentication to the Presto server as users\. The bind patterns are separated by a colon \(`:`\)\.  

```
[{
        "Classification": "presto-config",
                "Properties": {
                        "http-server.authentication.type": "PASSWORD"
                }
        },
        {
                "Classification": "presto-password-authenticator",
                "Properties": {
                        "password-authenticator.name": "ldap",
                        "ldap.url": "ldaps://ip-xxx-xxx-xxx-xxx.ec2.internal:636",
                        "authentication.ldap.user-bind-pattern": "uid=${USER},ou=admins,dc=ec2,dc=internal:uid=${USER},ou=datascientists,dc=ec2,dc=internal",
                        "internal-communication.authentication.ldap.user": "presto",
                        "internal-communication.authentication.ldap.password": "123456"
                }
        }]
```

**Example Amazon EMR 5\.11\.0 through 5\.15\.0**  
The format of the `presto-config `configuration classification is slightly different for these release versions\. The following example specifies the same parameters as the previous example\.  

```
[{
        "Classification": "presto-config",
                "Properties": {
                        "http-server.authentication.type": "LDAP",
                        "authentication.ldap.url": "ldaps://ip-xxx-xxx-xxx-xxx.ec2.internal:636",
                        "authentication.ldap.user-bind-pattern": "uid=${USER},ou=admins,dc=ec2,dc=internal:uid=${USER},ou=datascientists,dc=ec2,dc=internal",
                        "internal-communication.authentication.ldap.user": "presto",
                        "internal-communication.authentication.ldap.password": "123456"
                }
        }]
```

**Example Amazon EMR 5\.10\.0**  
Amazon EMR 5\.10\.0 supports anonymous binding only, so those entries are omitted\. In addition, only a single bind pattern can be specified\.  

```
[{
        "Classification": "presto-config",
                "Properties": {
                        "http-server.authentication.type": "LDAP",
                        "authentication.ldap.url": "ldaps://ip-xxx-xxx-xxx-xxx.ec2.internal:636",
                        "ldap.user-bind-pattern": "uid=${USER},ou=prestousers,dc=ec2,dc=internal"
                }
        }]
```

## Step 4: Create the script to copy the LDAP server certificate and upload it to Amazon S3<a name="emr-presto-ldap-servercert"></a>

Create a script that copies the certificate file to each node in the cluster and adds it to the keystore\. Create the script using a text editor, save it, and then upload it to Amazon S3\. In [Step 5: Create the cluster](#emr-presto-ldap-createcluster), the script file is referenced as *s3://MyBucket/LoadLDAPCert\.sh*\.

The following example script uses the default keystore password, *changeit*\. We recommend that you connect to the master node after you create the cluster and change the keystore password using the keytool command\.

```
#!/bin/bash
aws s3 cp s3://MyBucket/ldap_server.crt .
sudo keytool -import -keystore /usr/lib/jvm/jre-1.8.0-openjdk.x86_64/lib/security/cacerts -trustcacerts -alias ldap_server -file ./ldap_server.crt -storepass changeit -noprompt
```

## Step 5: Create the cluster<a name="emr-presto-ldap-createcluster"></a>

When you create the cluster, you specify Presto and other applications that you want Amazon EMR to install\. The following examples also reference the configuration classification properties within a JSON, but you can also specify the configuration classification inline\.

**To create a Presto cluster with LDAP authentication using the EMR management console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Choose **Presto** along with other applications for Amazon EMR to install, and under **Software Configuration**, select the **Release** of Amazon EMR to use\. LDAP authentication is supported only with Amazon EMR 5\.10\.0 and later\.

1. Under **Edit software settings**, choose **Load JSON from S3** , enter the location in Amazon S3 of the JSON configuration file you created in [Step 3: Create a configuration JSON with Presto properties for LDAP](#emr-presto-ldap-prestoconfig), and then choose **Next**\.

1. Configure cluster hardware and networking, and then choose **Next**\.

1. Choose **Bootstrap Actions**\. For **Add bootstrap action**, select **Custom action**, and then choose **Configure and add**\.

1. Enter a **Name** for the bootstrap action, enter the **Script location** that you created in [Step 4: Create the script to copy the LDAP server certificate and upload it to Amazon S3](#emr-presto-ldap-servercert), for example **s3://MyBucket/LoadLDAPCert\.sh**, and then choose **Add**\.

1. Under **General Options**, **Tags**, and **Additional Options** choose the settings that are appropriate for your application, and then choose **Next**\.

1. Choose **Authentication and encryption**, and then select the **Security configuration** that you created in [Step 2: Set up a security configuration](#emr-presto-ldap-seccfg)\.

1. Choose other security options as appropriate for your application, and then choose **Create cluster**\.

**To create a Presto cluster with LDAP authentication using the AWS CLI**
+ Use the `aws emr create-cluster` command\. At a minimum, specify the Presto application, and also the Presto configuration classification, the bootstrap script, and the security configuration that you created in the previous steps\. The following example references the configuration file as a JSON file saved in the same directory where you run the command\. The bootstrap script, on the other hand, must be saved in Amazon S3\. The following example uses `s3://MyBucket/LoadLDAPCert.sh`\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster  --applications Name=presto --release-label emr-5.16.0 \
  --use-default-roles --ec2-attributes KeyName=MyKeyPair,SubnetId=subnet-1234ab5 \ --instance-count 3 --instance-type m4.large --region us-west-2 --name "MyPrestoWithLDAPAuth” \
  --bootstrap-actions Name="Distribute LDAP server cert",Path="s3://MyBucket/LoadLDAPCert.sh" \
  --security-configuration MyPrestoLDAPSecCfg --configurations file://MyPrestoConfig.json
  ```