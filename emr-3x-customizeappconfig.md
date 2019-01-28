# Customizing Cluster and Application Configuration With Earlier AMI Versions of Amazon EMR<a name="emr-3x-customizeappconfig"></a>

Amazon EMR release version 4\.0\.0 introduced a simplified method of configuring applications using configuration classifications\. For more information, see [Configuring Applications](emr-configure-apps.md)\. When using an AMI version, you configure applications using bootstrap actions along with arguments that you pass\. For example, the `configure-hadoop` and `configure-daemons` bootstrap actions set Hadoop and YARN–specific environment properties like `--namenode-heap-size`\. In more recent versions, these are configured using the `hadoop-env` and `yarn-env` configuration classifications\. For bootstrap actions that perform common configurations, see the [emr\-bootstrap\-actions repository on Github](https://github.com/awslabs/emr-bootstrap-actions)\.

The following tables map bootstrap actions to configuration classifications in more recent Amazon EMR release versions\.


**Hadoop**  

| Affected application file name | AMI version bootstrap action | Configuration classification | 
| --- | --- | --- | 
| core\-site\.xml  | configure\-hadoop \-c  | core\-site | 
| log4j\.properties  | configure\-hadoop \-l  | hadoop\-log4j | 
| hdfs\-site\.xml  | configure\-hadoop \-s  | hdfs\-site  | 
| n/a | n/a | hdfs\-encryption\-zones | 
| mapred\-site\.xml  | configure\-hadoop \-m  | mapred\-site | 
| yarn\-site\.xml  | configure\-hadoop \-y  | yarn\-site | 
| httpfs\-site\.xml  | configure\-hadoop \-t  | httpfs\-site | 
| capacity\-scheduler\.xml  | configure\-hadoop \-z  | capacity\-scheduler | 
| yarn\-env\.sh  | configure\-daemons \-\-resourcemanager\-opts | yarn\-env | 


**Hive**  

| Affected application file name | AMI version bootstrap action | Configuration classification | 
| --- | --- | --- | 
| hive\-env\.sh | n/a | hive\-env | 
| hive\-site\.xml | hive\-script \-\-install\-hive\-site $\{MY\_HIVE\_SITE\_FILE\} | hive\-site | 
| hive\-exec\-log4j\.properties | n/a | hive\-exec\-log4j | 
| hive\-log4j\.properties | n/a | hive\-log4j | 


**EMRFS**  

| Affected application file name | AMI version bootstrap action | Configuration classification | 
| --- | --- | --- | 
| emrfs\-site\.xml | configure\-hadoop \-e | emrfs\-site | 
| n/a | s3get \-s s3://custom\-provider\.jar \-d /usr/share/aws/emr/auxlib/ | emrfs\-site \(with new setting fs\.s3\.cse\.encryptionMaterialsProvider\.uri\) | 

For a list of all classifications, see [Configuring Applications](emr-configure-apps.md)\.

## Application Environment Variables<a name="emr-3x-appenv"></a>

When using an AMI version, a `hadoop-user-env.sh` script is used along with the `configure-daemons` bootstrap action to configure the Hadoop environment\. The script includes the following actions:

```
#!/bin/bash 
export HADOOP_USER_CLASSPATH_FIRST=true; 
echo "HADOOP_CLASSPATH=/path/to/my.jar" >> /home/hadoop/conf/hadoop-user-env.sh
```

In Amazon EMR release 4\.x, you do the same using the `hadoop-env` configuration classification, as shown in the following example:

```
[ 
      { 
         "Classification":"hadoop-env",
         "Properties":{ 

         },
         "Configurations":[ 
            { 
               "Classification":"export",
               "Properties":{ 
                  "HADOOP_USER_CLASSPATH_FIRST":"true",
                  "HADOOP_CLASSPATH":"/path/to/my.jar"
               }
            }
         ]
      }
   ]
```

As another example, using `configure-daemons` and passing `--namenode-heap-size=2048` and `--namenode-opts=-XX:GCTimeRatio=19` is equivalent to the following configuration classifications\.

```
[ 
      { 
         "Classification":"hadoop-env",
         "Properties":{ 

         },
         "Configurations":[ 
            { 
               "Classification":"export",
               "Properties":{ 
                  "HADOOP_DATANODE_HEAPSIZE":  "2048",
           	"HADOOP_NAMENODE_OPTS":  "-XX:GCTimeRatio=19"
               }
            }
         ]
      }
   ]
```

Other application environment variables are no longer defined in `/home/hadoop/.bashrc`\. Instead, they are primarily set in `/etc/default` files per component or application, such as `/etc/default/hadoop`\. Wrapper scripts in `/usr/bin/` installed by application RPMs may also set additional environment variables before involving the actual bin script\.

## Service Ports<a name="emr-3x-serviceports"></a>

When using an AMI version, some services use custom ports\.


**Changes in Port Settings**  

| Setting | AMI Version 3\.x | Open\-source default | 
| --- | --- | --- | 
| fs\.default\.name | hdfs://emrDeterminedIP:9000 | default \(hdfs://emrDeterminedIP:8020\)  | 
| dfs\.datanode\.address | 0\.0\.0\.0:9200 | default \(0\.0\.0\.0:50010\)  | 
| dfs\.datanode\.http\.address | 0\.0\.0\.0:9102 | default \(0\.0\.0\.0:50075\)  | 
| dfs\.datanode\.https\.address | 0\.0\.0\.0:9402 | default \(0\.0\.0\.0:50475\) | 
| dfs\.datanode\.ipc\.address | 0\.0\.0\.0:9201 | default \(0\.0\.0\.0:50020\) | 
| dfs\.http\.address | 0\.0\.0\.0:9101 | default \(0\.0\.0\.0:50070\)  | 
| dfs\.https\.address | 0\.0\.0\.0:9202 | default \(0\.0\.0\.0:50470\)  | 
| dfs\.secondary\.http\.address | 0\.0\.0\.0:9104 | default \(0\.0\.0\.0:50090\) | 
| yarn\.nodemanager\.address | 0\.0\.0\.0:9103 | default \($\{yarn\.nodemanager\.hostname\}:0\)  | 
| yarn\.nodemanager\.localizer\.address  | 0\.0\.0\.0:9033 | default \($\{yarn\.nodemanager\.hostname\}:8040\) | 
| yarn\.nodemanager\.webapp\.address | 0\.0\.0\.0:9035 | default \($\{yarn\.nodemanager\.hostname\}:8042\) | 
| yarn\.resourcemanager\.address | emrDeterminedIP:9022 | default \($\{yarn\.resourcemanager\.hostname\}:8032\) | 
| yarn\.resourcemanager\.admin\.address | emrDeterminedIP:9025 | default \($\{yarn\.resourcemanager\.hostname\}:8033\) | 
| yarn\.resourcemanager\.resource\-tracker\.address | emrDeterminedIP:9023 | default \($\{yarn\.resourcemanager\.hostname\}:8031\) | 
| yarn\.resourcemanager\.scheduler\.address | emrDeterminedIP:9024 | default \($\{yarn\.resourcemanager\.hostname\}:8030\) | 
| yarn\.resourcemanager\.webapp\.address | 0\.0\.0\.0:9026  | default \($\{yarn\.resourcemanager\.hostname\}:8088\) | 
| yarn\.web\-proxy\.address | emrDeterminedIP:9046  | default \(no\-value\)  | 
| yarn\.resourcemanager\.hostname | 0\.0\.0\.0 \(default\)  | emrDeterminedIP | 

**Note**  
The *emrDeterminedIP* is an IP address that is generated by Amazon EMR\.

## Users<a name="emr-3x-users"></a>

When using an AMI version, the user `hadoop` runs all processes and owns all files\. In Amazon EMR release version 4\.0\.0 and later, users exist at the application and component level\.

## Installation Sequence, Installed Artifacts, and Log File Locations<a name="emr-3x-directories"></a>

When using an AMI version, application artifacts and their configuration directories are installed in the `/home/hadoop/application` directory\. For example, if you installed Hive, the directory would be `/home/hadoop/hive`\. In Amazon EMR release 4\.0\.0 and later, application artifacts are installed in the `/usr/lib/application` directory\. When using an AMI version, log files are found in various places\. The table below lists locations\.


**Changes in Log Locations on Amazon S3**  

| Daemon or Application | Directory location | 
| --- | --- | 
| instance\-state | node/instance\-id/instance\-state/ | 
| hadoop\-hdfs\-namenode | daemons/instance\-id/hadoop\-hadoop\-namenode\.log | 
| hadoop\-hdfs\-datanode | daemons/instance\-id/hadoop\-hadoop\-datanode\.log | 
| hadoop\-yarn \(ResourceManager\) | daemons/instance\-id/yarn\-hadoop\-resourcemanager | 
| hadoop\-yarn \(Proxy Server\) | daemons/instance\-id/yarn\-hadoop\-proxyserver | 
| mapred\-historyserver | daemons/instance\-id/ | 
| httpfs | daemons/instance\-id/httpfs\.log | 
| hive\-server | node/instance\-id/hive\-server/hive\-server\.log | 
| hive\-metastore | node/instance\-id/apps/hive\.log | 
| Hive CLI | node/instance\-id/apps/hive\.log | 
| YARN applications user logs and container logs | task\-attempts/ | 
| Mahout | N/A | 
| Pig | N/A | 
| spark\-historyserver | N/A | 
| mapreduce job history files | jobs/ | 

## Command Runner<a name="emr-differences-commandrunner"></a>

When using an AMI version, many scripts or programs, like `/home/hadoop/contrib/streaming/hadoop-streaming.jar`, are not placed on the shell login path environment, so you need to specify the full path when you use a jar file such as command\-runner\.jar or script\-runner\.jar to execute the scripts\. The `command-runner.jar` is located on the AMI so there is no need to know a full URI as was the case with `script-runner.jar`\. 

## Replication Factor<a name="emr-3x-replication"></a>

The replication factor lets you configure when to start a Hadoop JVM\. You can start a new Hadoop JVM for every task, which provides better task isolation, or you can share JVMs between tasks, providing lower framework overhead\. If you are processing many small files, it makes sense to reuse the JVM many times to amortize the cost of start\-up\. However, if each task takes a long time or processes a large amount of data, then you might choose to not reuse the JVM to ensure that all memory is freed for subsequent tasks\. When using an AMI version, you can customize the replication factor using the `configure-hadoop` bootstrap action to set the `mapred.job.reuse.jvm.num.tasks` property\. 

The following example demonstrates setting the JVM reuse factor for infinite JVM reuse\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --name "Test cluster" --ami-version 3.11.0 \
--applications Name=Hue Name=Hive Name=Pig \
--use-default-roles --ec2-attributes KeyName=myKey \
--instance-groups InstanceGroupType=MASTER,InstanceCount=1,InstanceType=m3.xlarge \
InstanceGroupType=CORE,InstanceCount=2,InstanceType=m3.xlarge \
--bootstrap-actions Path=s3://elasticmapreduce/bootstrap-actions/configure-hadoop,\
Name="Configuring infinite JVM reuse",Args=["-m","mapred.job.reuse.jvm.num.tasks=-1"]
```