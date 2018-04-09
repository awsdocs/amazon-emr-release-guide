# Sandbox Applications<a name="emr-sandbox-apps-4x"></a>

When using Amazon EMR 4\.x release versions, some applications are considered *sandbox* applications\. Sandbox applications are early versions of the application that we made available at the time of the initial Amazon EMR release because of demand\. You can use the console, AWS CLI, or API to have Amazon EMR install sandbox applications in the same way as native applications, but sandbox applications have limited support and documentation\. Sandbox applications became native, fully supported applications in Amazon EMR release version 5\.0\.0 and later\. The following are sandbox applications in Amazon EMR 4\.x release versions:
+ Oozie
+ Presto
+ Sqoop
+ Zeppelin
+ Zookeeper

When you install sandbox applications, the application names are denoted with the suffix `-sandbox`\. For example, to install the sandbox version of *Presto*, use `Presto-sandbox`\. Installation may take longer than it does for a fully supported application\. The version numbers listed for each application in this section correspond to the community version of the application\.

## Oozie \(Sandbox Versions\)<a name="emr-Oozie-sandbox-4x"></a>

Oozie is available as a sandbox application beginning with Amazon EMR release version 4\.1\.0\.

Oozie examples are not installed by default using the sandbox versions\. To install the examples, SSH to the master node and run `install-oozie-examples`\.


**Oozie\-Sandbox Version Information for emr\-4\.9\.3**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.3 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.9\.2**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.2 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.9\.1**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.1 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.8\.4**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.4 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.8\.3**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.3 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.8\.2**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.2 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.8\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.7\.2**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.2 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.7\.1**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.1 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.7\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.6\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.6\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.5\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.5\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.4\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.4\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.3\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.3\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.2\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.2\.0 | Oozie\-Sandbox 4\.2\.0 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 


**Oozie\-Sandbox Version Information for emr\-4\.1\.0**  

| Amazon EMR Release Label | Oozie\-Sandbox Version | Components Installed With Oozie\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.1\.0 | Oozie\-Sandbox 4\.0\.1 | emrfs, emr\-ddb, emr\-goodies, emr\-kinesis, emr\-s3\-dist\-cp, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, oozie\-client, oozie\-server | 

## Presto \(Sandbox Versions\)<a name="emr-Presto-sandbox-4x"></a>

Presto is available as a sandbox application beginning with Amazon EMR release version 4\.1\.0\.


**Presto\-Sandbox Version Information for emr\-4\.9\.3**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.3 | Presto\-Sandbox 0\.157\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.9\.2**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.2 | Presto\-Sandbox 0\.157\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.9\.1**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.1 | Presto\-Sandbox 0\.157\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.8\.4**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.4 | Presto\-Sandbox 0\.157\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.8\.3**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.3 | Presto\-Sandbox 0\.157\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.8\.2**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.2 | Presto\-Sandbox 0\.152\.3 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.8\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.0 | Presto\-Sandbox 0\.151 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.7\.2**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.2 | Presto\-Sandbox 0\.148 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.7\.1**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.1 | Presto\-Sandbox 0\.147 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.7\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.0 | Presto\-Sandbox 0\.147 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hcatalog\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.6\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.6\.0 | Presto\-Sandbox 0\.143 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.5\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.5\.0 | Presto\-Sandbox 0\.140 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.4\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.4\.0 | Presto\-Sandbox 0\.136 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.3\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.3\.0 | Presto\-Sandbox 0\.130 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.2\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.2\.0 | Presto\-Sandbox 0\.125 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 


**Presto\-Sandbox Version Information for emr\-4\.1\.0**  

| Amazon EMR Release Label | Presto\-Sandbox Version | Components Installed With Presto\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.1\.0 | Presto\-Sandbox 0\.119 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hive\-client, hive\-metastore\-server, mysql\-server, presto\-coordinator, presto\-worker | 

## Sqoop \(Sandbox Versions\)<a name="emr-Sqoop-sandbox-4x"></a>

Sqoop is available as a sandbox application beginning with Amazon EMR release version 4\.4\.0\.


**Sqoop\-Sandbox Version Information for emr\-4\.9\.3**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.3 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.9\.2**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.2 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.9\.1**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.1 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.8\.4**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.4 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.8\.3**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.3 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.8\.2**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.2 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.8\.0**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.0 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.7\.2**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.2 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.7\.1**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.1 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.7\.0**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.0 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.6\.0**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.6\.0 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, mysql\-server, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.5\.0**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.5\.0 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, sqoop\-client | 


**Sqoop\-Sandbox Version Information for emr\-4\.4\.0**  

| Amazon EMR Release Label | Sqoop\-Sandbox Version | Components Installed With Sqoop\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.4\.0 | Sqoop\-Sandbox 1\.4\.6 | emrfs, emr\-ddb, emr\-goodies, hadoop\-client, hadoop\-mapred, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, sqoop\-client | 

## Zeppelin \(Sandbox Versions\)<a name="emr-Zeppelin-sandbox-4x"></a>

Zeppelin is available as a sandbox application beginning with Amazon EMR release version 4\.1\.0\.


**Zeppelin\-Sandbox Version Information for emr\-4\.9\.3**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.3 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.9\.2**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.2 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.9\.1**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.1 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.8\.4**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.4 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.8\.3**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.3 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.8\.2**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.2 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.8\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.0 | Zeppelin\-Sandbox 0\.6\.1 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.7\.2**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.2 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.7\.1**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.1 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.7\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.0 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.6\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.6\.0 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.5\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.5\.0 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.4\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.4\.0 | Zeppelin\-Sandbox 0\.5\.6 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.3\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.3\.0 | Zeppelin\-Sandbox 0\.5\.5 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.2\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.2\.0 | Zeppelin\-Sandbox 0\.5\.5 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 


**Zeppelin\-Sandbox Version Information for emr\-4\.1\.0**  

| Amazon EMR Release Label | Zeppelin\-Sandbox Version | Components Installed With Zeppelin\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.1\.0 | Zeppelin\-Sandbox 0\.6\.0\-SNAPSHOT | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, spark\-client, spark\-history\-server, spark\-on\-yarn, spark\-yarn\-slave, zeppelin\-server | 

## Zookeeper \(Sandbox Versions\)<a name="emr-Zookeeper-sandbox-4x"></a>

Zookeeper is available as a sandbox application beginning with Amazon EMR release version 4\.6\.0\.


**ZooKeeper\-Sandbox Version Information for emr\-4\.9\.3**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.3 | ZooKeeper\-Sandbox 3\.4\.9 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.9\.2**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.2 | ZooKeeper\-Sandbox 3\.4\.9 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.9\.1**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.9\.1 | ZooKeeper\-Sandbox 3\.4\.9 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.8\.4**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.4 | ZooKeeper\-Sandbox 3\.4\.9 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.8\.3**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.3 | ZooKeeper\-Sandbox 3\.4\.9 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.8\.2**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.2 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.8\.0**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.8\.0 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.7\.2**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.2 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.7\.1**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.1 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.7\.0**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.7\.0 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 


**ZooKeeper\-Sandbox Version Information for emr\-4\.6\.0**  

| Amazon EMR Release Label | ZooKeeper\-Sandbox Version | Components Installed With ZooKeeper\-Sandbox | 
| --- | --- | --- | 
| emr\-4\.6\.0 | ZooKeeper\-Sandbox 3\.4\.8 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, zookeeper\-client, zookeeper\-server | 