# HBase Application Specifics for Earlier AMI Versions of Amazon EMR<a name="emr-3x-hbase"></a>

## Supported HBase Versions<a name="emr-3x-hbase-versions"></a>


| HBase Version | AMI Version | AWS CLI Configuration Parameters | HBase Version Details | 
| --- | --- | --- | --- | 
| [0\.94\.18](https://svn.apache.org/repos/asf/hbase/branches/0.94/CHANGES.txt) | 3\.1\.0 and later |  `--ami-version 3.1` `--ami-version 3.2` `--ami-version 3.3` `--applications Name=HBase`  |  [\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-3x-hbase.html)  | 
| [0\.94\.7](https://svn.apache.org/repos/asf/hbase/branches/0.94/CHANGES.txt) | 3\.0\-3\.0\.4 |  `--ami-version 3.0` `--applications Name=HBase`  | 
| [0\.92](https://svn.apache.org/repos/asf/hbase/branches/0.92/CHANGES.txt) | 2\.2 and later |  `--ami-version 2.2 or later` `--applications Name=HBase`  | 

## HBase Cluster Prerequisites<a name="emr-3x-hbase-prerequisites"></a>

A cluster created using Amazon EMR AMI versions 2\.x and 3\.x should meet the following requirements for HBase\.
+ The AWS CLI \(optional\)—To interact with HBase using the command line, download and install the latest version of the AWS CLI\. For more information, see [Installing the AWS Command Line Interface](https://docs.aws.amazon.com/cli/latest/userguide//installing.html) in the *AWS Command Line Interface User Guide*\.
+ At least two instances \(optional\)—The cluster's master node runs the HBase master server and Zookeeper, and task nodes run the HBase region servers\. For best performance, HBase clusters should run on at least two EC2 instances, but you can run HBase on a single node for evaluation purposes\. 
+ Long\-running cluster—HBase only runs on long\-running clusters\. By default, the CLI and Amazon EMR console create long\-running clusters\. 
+ An Amazon EC2 key pair set \(recommended\)—To use the Secure Shell \(SSH\) network protocol to connect with the master node and run HBase shell commands, you must use an Amazon EC2 key pair when you create the cluster\. 
+ The correct AMI and Hadoop versions—HBase clusters are currently supported only on Hadoop 20\.205 or later\. 
+ Ganglia \(optional\)—To monitor HBase performance metrics, install Ganglia when you create the cluster\. 
+ An Amazon S3 bucket for logs \(optional\)—The logs for HBase are available on the master node\. If you'd like these logs copied to Amazon S3, specify an S3 bucket to receive log files when you create the cluster\. 

## Creating a Cluster with HBase<a name="emr-3x-hbase-launch"></a>

The following table lists options that are available when using the console to create a cluster with HBase using an Amazon EMR AMI release version\.


| Field | Action | 
| --- | --- | 
| Restore from backup | Specify whether to pre\-load the HBase cluster with data stored in Amazon S3\. | 
| Backup location | Specify the URI where the backup from which to restore resides in Amazon S3\.  | 
| Backup version | Optionally, specify the version name of the backup at Backup Location to use\. If you leave this field blank, Amazon EMR uses the latest backup at Backup Location to populate the new HBase cluster\.  | 
| Schedule Regular Backups | Specify whether to schedule automatic incremental backups\. The first backup is a full backup to create a baseline for future incremental backups\. | 
| Consistent backup | Specify whether the backups should be consistent\. A consistent backup is one that pauses write operations during the initial backup stage, synchronization across nodes\. Any write operations thus paused are placed in a queue and resume when synchronization completes\. | 
| Backup frequency | The number of days/hours/minutes between scheduled backups\. | 
| Backup location | The Amazon S3 URI where backups are stored\. The backup location for each HBase cluster should be different to ensure that differential backups stay correct\.  | 
| Backup start time | Specify when the first backup should occur\. You can set this to now, which causes the first backup to start as soon as the cluster is running, or enter a date and time in [ISO format](http://www.w3.org/TR/NOTE-datetime)\. For example, 2012\-06\-15T20:00Z would set the start time to June 15, 2012 at 8PM UTC\.  | 

The following example AWS CLI command launches a cluster with HBase and other applications:

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.3 \
               --applications Name=Hue Name=Hive Name=Pig Name=HBase \
               --use-default-roles --ec2-attributes KeyName=myKey \
               --instance-type c1.xlarge --instance-count 3 --termination-protected
```

After the connection between the Hive and HBase clusters has been made \(as shown in the previous procedure\), you can access the data stored on the HBase cluster by creating an external table in Hive\. 

The following example, when run from the Hive prompt, creates an external table that references data stored in an HBase table called `inputTable`\. You can then reference `inputTable` in Hive statements to query and modify data stored in the HBase cluster\. 

**Note**  
The following example uses **protobuf\-java\-2\.4\.0a\.jar** in AMI 2\.3\.3, but you should modify the example to match your version\. To check which version of the Protocol Buffers JAR you have, run the command at the Hive command prompt: `! ls /home/hadoop/lib;`\. 

```
add jar lib/emr-metrics-1.0.jar ;
               add jar lib/protobuf-java-2.4.0a.jar ;
               
               set hbase.zookeeper.quorum=ec2-107-21-163-157.compute-1.amazonaws.com ;
               
               create external table inputTable (key string, value string)
                    stored by 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
                     with serdeproperties ("hbase.columns.mapping" = ":key,f1:col1")
                     tblproperties ("hbase.table.name" = "t1");
               
               select count(*) from inputTable ;
```

## Customizing HBase Configuration<a name="emr-3x-hbase-customize"></a>

Although the default settings should work for most applications, you have the flexibility to modify your HBase configuration settings\. To do this, run one of two bootstrap action scripts: 
+ **configure\-hbase\-daemons**—Configures properties of the master, regionserver, and zookeeper daemons\. These properties include heap size and options to pass to the Java Virtual Machine \(JVM\) when the HBase daemon starts\. You set these properties as arguments in the bootstrap action\. This bootstrap action modifies the /home/hadoop/conf/hbase\-user\-env\.sh configuration file on the HBase cluster\. 
+ **configure\-hbase**—Configures HBase site\-specific settings such as the port the HBase master should bind to and the maximum number of times the client CLI client should retry an action\. You can set these one\-by\-one, as arguments in the bootstrap action, or you can specify the location of an XML configuration file in Amazon S3\. This bootstrap action modifies the /home/hadoop/conf/hbase\-site\.xml configuration file on the HBase cluster\. 

**Note**  
These scripts, like other bootstrap actions, can only be run when the cluster is created; you cannot use them to change the configuration of an HBase cluster that is currently running\. 

When you run the **configure\-hbase** or **configure\-hbase\-daemons** bootstrap actions, the values you specify override the default values\. Any values that you don't explicitly set receive the default values\. 

Configuring HBase with these bootstrap actions is analogous to using bootstrap actions in Amazon EMR to configure Hadoop settings and Hadoop daemon properties\. The difference is that HBase does not have per\-process memory options\. Instead, memory options are set using the `--daemon-opts` argument, where *daemon* is replaced by the name of the daemon to configure\. 

### Configure HBase Daemons<a name="emr-3x-hbase-configure-daemons"></a>

 Amazon EMR provides a bootstrap action, `s3://region.elasticmapreduce/bootstrap-actions/configure-hbase-daemons`, that you can use to change the configuration of HBase daemons, where *region* is the region into which you're launching your HBase cluster\. 

To configure HBase daemons using the AWS CLI, add the `configure-hbase-daemons` bootstrap action when you launch the cluster to configure one or more HBase daemons\. You can set the following properties\. 


| Property | Description | 
| --- | --- | 
| hbase\-master\-opts | Options that control how the JVM runs the master daemon\. If set, these override the default HBASE\_MASTER\_OPTS variables\.  | 
| regionserver\-opts | Options that control how the JVM runs the region server daemon\. If set, these override the default HBASE\_REGIONSERVER\_OPTS variables\. | 
| zookeeper\-opts | Options that control how the JVM runs the zookeeper daemon\. If set, these override the default HBASE\_ZOOKEEPER\_OPTS variables\.  | 

For more information about these options, see [hbase\-env\.sh](https://hbase.apache.org/book.html#hbase.env.sh) in the HBase documentation\. 

A bootstrap action to configure values for `zookeeper-opts` and `hbase-master-opts` is shown in the following example\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.3 \
--applications Name=Hue Name=Hive Name=Pig Name=HBase \
--use-default-roles --ec2-attributes KeyName=myKey \
--instance-type c1.xlarge --instance-count 3 --termination-protected \
--bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hbase-daemons,\
Args=["--hbase-zookeeper-opts=-Xmx1024m -XX:GCTimeRatio=19","--hbase-master-opts=-Xmx2048m","--hbase-regionserver-opts=-Xmx4096m"]
```

### Configure HBase Site Settings<a name="emr-3x-hbase-configure-site"></a>

Amazon EMR provides a bootstrap action, `s3://elasticmapreduce/bootstrap-actions/configure-hbase`, that you can use to change the configuration of HBase\. You can set configuration values one\-by\-one, as arguments in the bootstrap action, or you can specify the location of an XML configuration file in Amazon S3\. Setting configuration values one\-by\-one is useful if you only need to set a few configuration settings\. Setting them using an XML file is useful if you have many changes to make, or if you want to save your configuration settings for reuse\. 

**Note**  
You can prefix the Amazon S3 bucket name with a region prefix, such as `s3://region.elasticmapreduce/bootstrap-actions/configure-hbase`, where *region* is the region into which you're launching your HBase cluster\. 

This bootstrap action modifies the `/home/hadoop/conf/hbase-site.xml` configuration file on the HBase cluster\. The bootstrap action can only be run when the HBase cluster is launched\.

For more information about the HBase site settings that you can configure, see [Default Configuration](http://hbase.apache.org/book.html#config.files) in the HBase documentation\. 

Set the `configure-hbase` bootstrap action when you launch the HBase cluster and specify the values in `hbase-site.xml` to change\.

**To specify individual HBase site settings using the AWS CLI**
+ To change the `hbase.hregion.max.filesize` setting, type the following command and replace *myKey* with the name of your Amazon EC2 key pair\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

  ```
  aws emr create-cluster --name "Test cluster" --ami-version 3.3 \
  --applications Name=Hue Name=Hive Name=Pig Name=HBase \
  --use-default-roles --ec2-attributes KeyName=myKey \
  --instance-type c1.xlarge --instance-count 3 --termination-protected \
  --bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hbase,Args=["-s","hbase.hregion.max.filesize=52428800"]
  ```

**To specify HBase site settings with an XML file using the AWS CLI**

1. Create a custom version of `hbase-site.xml`\. Your custom file must be valid XML\. To reduce the chance of introducing errors, start with the default copy of `hbase-site.xml`, located on the Amazon EMR HBase master node at `/home/hadoop/conf/hbase-site.xml`, and edit a copy of that file instead of creating a file from scratch\. You can give your new file a new name, or leave it as `hbase-site.xml`\. 

1. Upload your custom `hbase-site.xml` file to an Amazon S3 bucket\. It should have permissions set so the AWS account that launches the cluster can access the file\. If the AWS account launching the cluster also owns the Amazon S3 bucket, it has access\. 

1. Set the **configure\-hbase** bootstrap action when you launch the HBase cluster, and include the location of your custom `hbase-site.xml` file\. The following example sets the HBase site configuration values to those specified in the file `s3://mybucket/my-hbase-site.xml`\. Type the following command, replace *myKey* with the name of your EC2 key pair, and replace *mybucket* with the name of your Amazon S3 bucket\.
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

   ```
   aws emr create-cluster --name "Test cluster" --ami-version 3.3 \
           --applications Name=Hue Name=Hive Name=Pig Name=HBase \
           --use-default-roles --ec2-attributes KeyName=myKey \
           --instance-type c1.xlarge --instance-count 3 --termination-protected \
           --bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hbase,Args=["--site-config-file","s3://mybucket/config.xml"]
   ```

   If you specify more than one option to customize HBase operation, you must prepend each key\-value pair with a `-s` option switch, as shown in the following example:

   ```
          --bootstrap-actions s3://elasticmapreduce/bootstrap-actions/configure-hbase,Args=["-s","zookeeper.session.timeout=60000"]
   ```

With the proxy set and the SSH connection open, you can view the HBase UI by opening a browser window with http://*master\-public\-dns\-name*:60010/master\-status, where *master\-public\-dns\-name* is the public DNS address of the master node in the HBase cluster\. 

You can view the current HBase logs by using SSH to connect to the master node, and navigating to the `mnt/var/log/hbase` directory\. These logs are not available after the cluster is terminated unless you enable logging to Amazon S3 when the cluster is launched\.

## Back Up and Restore HBase<a name="emr-3x-hbase-backup-restore"></a>

Amazon EMR provides the ability to back up your HBase data to Amazon S3, either manually or on an automated schedule\. You can perform both full and incremental backups\. After you have a backed\-up version of HBase data, you can restore that version to an HBase cluster\. You can restore to an HBase cluster that is currently running, or launch a new cluster pre\-populated with backed\-up data\. 

During the backup process, HBase continues to execute write commands\. Although this ensures that your cluster remains available throughout the backup, there is the risk of inconsistency between the data being backed up and any write operations being executed in parallel\. To understand the inconsistencies that might arise, you have to consider that HBase distributes write operations across the nodes in its cluster\. If a write operation happens after a particular node is polled, that data is not included in the backup archive\. You may even find that earlier writes to the HBase cluster \(sent to a node that has already been polled\) might not be in the backup archive, whereas later writes \(sent to a node before it was polled\) are included\. 

If a consistent backup is required, you must pause writes to HBase during the initial portion of the backup process, synchronization across nodes\. You can do this by specifying the `--consistent` parameter when requesting a backup\. With this parameter, writes during this period are queued and executed as soon as the synchronization completes\. You can also schedule recurring backups, which resolves any inconsistencies over time, as data that is missed on one backup pass is backed up on the following pass\. 

When you back up HBase data, you should specify a different backup directory for each cluster\. An easy way to do this is to use the cluster identifier as part of the path specified for the backup directory\. For example, `s3://mybucket/backups/j-3AEXXXXXX16F2`\. This ensures that any future incremental backups reference the correct HBase cluster\. 

When you are ready to delete old backup files that are no longer needed, we recommend that you first do a full backup of your HBase data\. This ensures that all data is preserved and provides a baseline for future incremental backups\. After the full backup is done, you can navigate to the backup location and manually delete the old backup files\. 

The HBase backup process uses S3DistCp for the copy operation, which has certain limitations regarding temporary file storage space\. 

### Back Up and Restore HBase Using the Console<a name="emr-3x-hbase-backup-restore-console"></a>

The console provides the ability to launch a new cluster and populate it with data from a previous HBase backup\. It also gives you the ability to schedule periodic incremental backups of HBase data\. Additional backup and restore functionality, such as the ability to restore data to an already running cluster, do manual backups, and schedule automated full backups, is available using the CLI\.

**To populate a new cluster with archived HBase data using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**\.

1. In the **Software Configuration** section, for **Additional Applications**, choose **HBase** and **Configure and add**\.

1. On the **Add Application** dialog box, check **Restore From Backup**\. 

1. For **Backup Location**, specify the location of the backup yto load into the new HBase cluster\. This should be an Amazon S3 URL of the form `s3://myawsbucket/backups/`\. 

1. For **Backup Version**, you have the option to specify the name of a backup version to load by setting a value\. If you do not set a value for **Backup Version**, Amazon EMR loads the latest backup in the specified location\. 

1. Choose **Add** and proceed to create the cluster with other options as desired\.

**To schedule automated backups of HBase data using the console**

1. In the **Software Configuration** section, for **Additional Applications**, choose **HBase** and **Configure and add**\.

1. Choose **Schedule Regular Backups**\.

1. Specify whether the backups should be consistent\. A consistent backup is one that pauses write operations during the initial backup stage, synchronization across nodes\. Any write operations thus paused are placed in a queue and resume when the synchronization completes\. 

1. Set how often backups should occur by entering a number for **Backup Frequency** and choosing **Days**, **Hours**, or **Minutes**\. The first automated backup that runs is a full backup; after that, Amazon EMR saves incremental backups based on the schedule that you specify\. 

1. Specify the location in Amazon S3 where the backups should be stored\. Each HBase cluster should be backed up to a separate location in Amazon S3 to ensure that incremental backups are calculated correctly\. 

1. Specify when the first backup should occur by setting a value for **Backup Start Time**\. You can set this to `now`, which causes the first backup to start as soon as the cluster is running, or enter a date and time in [ISO format](http://www.w3.org/TR/NOTE-datetime)\. For example, 2013\-09\-26T20:00Z, sets the start time to September 26, 2013 at 8PM UTC\. 

1. Choose **Add**\.

1. Proceed with creating the cluster with other options as desired\.

## Monitor HBase with CloudWatch<a name="emr-3x-hbase-cloudwatch"></a>

Amazon EMR reports three metrics to CloudWatch that you can use to monitor your HBase backups\. These metrics are pushed to CloudWatch at five\-minute intervals, and are provided without charge\.


| Metric | Description | 
| --- | --- | 
| HBaseBackupFailed |  Whether the last backup failed\. This is set to 0 by default and updated to 1 if the previous backup attempt failed\. This metric is only reported for HBase clusters\. Use case: Monitor HBase backups Units: *Count*  | 
| HBaseMostRecentBackupDuration |  The amount of time it took the previous backup to complete\. This metric is set regardless of whether the last completed backup succeeded or failed\. While the backup is ongoing, this metric returns the number of minutes after the backup started\. This metric is only reported for HBase clusters\. Use case: Monitor HBase Backups Units: *Minutes*  | 
| HBaseTimeSinceLastSuccessfulBackup |  The number of elapsed minutes after the last successful HBase backup started on your cluster\. This metric is only reported for HBase clusters\. Use case: Monitor HBase backups Units: *Minutes*  | 

## Configure Ganglia for HBase<a name="emr-3x-ganglia-for-hbase"></a>

You configure Ganglia for HBase using the **configure\-hbase\-for\-ganglia** bootstrap action\. This bootstrap action configures HBase to publish metrics to Ganglia\. 

You must configure HBase and Ganglia when you launch the cluster; Ganglia reporting cannot be added to a running cluster\. 

Ganglia also stores log files on the server at `/mnt/var/log/ganglia/rrds`\. If you configured your cluster to persist log files to an Amazon S3 bucket, the Ganglia log files are persisted there as well\. 

To launch a cluster with Ganglia for HBase, use the **configure\-hbase\-for\-ganglia** bootstrap action as shown in the following example\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.3 \
--applications Name=Hue Name=Hive Name=Pig Name=HBase Name=Ganglia \
--use-default-roles --ec2-attributes KeyName=myKey \
--instance-type c1.xlarge --instance-count 3 --termination-protected \
--bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hbase-for-ganglia
```

After the cluster is launched with Ganglia configured, you can access the Ganglia graphs and reports using the graphical interface running on the master node\. 