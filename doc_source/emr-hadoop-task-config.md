# Task configuration<a name="emr-hadoop-task-config"></a>

You can set configuration variables to tune the performance of your MapReduce jobs\. This section provides the default values for important settings\. Default values vary based on the EC2 instance type of the node used in the cluster\. HBase is available when using Amazon EMR release version 4\.6\.0 and later\. Different defaults are used when HBase is installed\. Those values are provided along with the initial defaults\.

Hadoop 2 uses two parameters, `mapreduce.map.java.opts` and `mapreduce.reduce.java.opts`, to configure memory for map and reduce JVMs respectively\. These replace the single `mapreduce.map.java.opts` configuration option from earlier Hadoop versions\.

Similarly, `mapred.job.jvm.num.tasks` replaces `mapred.job.reuse.jvm.num.tasks` in Hadoop 2\.7\.2 and later\. Amazon EMR sets this value to 20 regardless of EC2 instance type\. You can override this setting using the `mapred-site` configuration classification\. Setting a value of `-1` indicates that a JVM can be re\-used for an infinite number of tasks within a single job, and a value of `1` indicates that a new JVM is spawned for each task\.

For example, to set the value of `mapred.job.jvm.num.tasks` to \-1 you can create a file with the following contents:

```
[
    {
      "Classification": "mapred-site",
      "Properties": {
        "mapred.job.jvm.num.tasks": "-1"
      }
    }
  ]
```

When you use the `create-cluster` command or `modify-instance-groups` command from the AWS CLI, you can then reference the JSON configuration file\. In the following example, the configuration file is saved as `myConfig.json` and stored in Amazon S3\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --release-label emr-5.33.0 --instance-type m5.xlarge \
--instance-count 3 --applications Name=Hadoop --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json \
--use-default-roles
```

You can change default values listed below using the `mapred-site` configuration classification in the same way, and set multiple values and multiple configuration classifications using a single JSON file\. For more information, see [Configure applications](emr-configure-apps.md)\.

With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

## Default values for task configuration settings<a name="emr-hadoop-task-jvm"></a>

**Topics**
+ [c1 instances](#emr-hadoop-task-config-c1)
+ [c3 instances](#emr-hadoop-task-config-c3)
+ [c4 instances](#emr-hadoop-task-config-c4)
+ [c5 instances](#emr-hadoop-task-config-c5)
+ [c5a instances](#emr-hadoop-task-config-c5a)
+ [c5ad instances](#emr-hadoop-task-config-c5ad)
+ [c5d instances](#emr-hadoop-task-config-c5d)
+ [c5n instances](#emr-hadoop-task-config-c5n)
+ [c6g instances](#emr-hadoop-task-config-c6g)
+ [c6gd instances](#emr-hadoop-task-config-c6gd)
+ [c6gn instances](#emr-hadoop-task-config-c6gn)
+ [cc2 instances](#emr-hadoop-task-config-cc2)
+ [cg1 instances](#emr-hadoop-task-config-cg1)
+ [cr1 instances](#emr-hadoop-task-config-cr1)
+ [d2 instances](#emr-hadoop-task-config-d2)
+ [d3 instances](#emr-hadoop-task-config-d3)
+ [d3en instances](#emr-hadoop-task-config-d3)
+ [g2 instances](#emr-hadoop-task-config-g2)
+ [g3 instances](#emr-hadoop-task-config-g3)
+ [g3s instances](#emr-hadoop-task-config-g3s)
+ [g4dn instances](#emr-hadoop-task-config-g4dn)
+ [hi1 instances](#emr-hadoop-task-config-hi1)
+ [hs1 instances](#emr-hadoop-task-config-hs1)
+ [i2 instances](#emr-hadoop-task-config-i2)
+ [i3 instances](#emr-hadoop-task-config-i3)
+ [i3en instances](#emr-hadoop-task-config-i3en)
+ [m1 instances](#emr-hadoop-task-config-m1)
+ [m2 instances](#emr-hadoop-task-config-m2)
+ [m3 instances](#emr-hadoop-task-config-m3)
+ [m4 instances](#emr-hadoop-task-config-m4)
+ [m5 instances](#emr-hadoop-task-config-m5)
+ [m5a instances](#emr-hadoop-task-config-m5a)
+ [m5d instances](#emr-hadoop-task-config-m5d)
+ [m5zn instances](#emr-hadoop-task-config-m5zn)
+ [m6g instances](#emr-hadoop-task-config-m6g)
+ [m6gd instances](#emr-hadoop-task-config-m6gd)
+ [p2 instances](#emr-hadoop-task-config-p2)
+ [p3 instances](#emr-hadoop-task-config-p3)
+ [r3 instances](#emr-hadoop-task-config-r3)
+ [r4 instances](#emr-hadoop-task-config-r4)
+ [r5 instances](#emr-hadoop-task-config-r5)
+ [r5a instances](#emr-hadoop-task-config-r5a)
+ [r5b instances](#emr-hadoop-task-config-r5b)
+ [r5d instances](#emr-hadoop-task-config-r5d)
+ [r5dn instances](#emr-hadoop-task-config-r5dn)
+ [r6g instances](#emr-hadoop-task-config-r6g)
+ [r6gd instances](#emr-hadoop-task-config-r6gd)
+ [z1d instances](#emr-hadoop-task-config-z1d)

### c1 instances<a name="emr-hadoop-task-config-c1"></a>


**c1\.medium**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx288m | 
| mapreduce\.reduce\.java\.opts | \-Xmx288m | 
| mapreduce\.map\.memory\.mb | 512 | 
| mapreduce\.reduce\.memory\.mb | 512 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 512 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 512 | 
| yarn\.nodemanager\.resource\.memory\-mb | 1024 | 


**c1\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx864m | \-Xmx864m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 1024 | 1024 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 2048 | 2560 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5120 | 2560 | 

### c3 instances<a name="emr-hadoop-task-config-c3"></a>


**c3\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 2816 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 2816 | 


**c3\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11520 | 5760 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11520 | 5760 | 


**c3\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23040 | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23040 | 11520 | 


**c3\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1331m | \-Xmx1331m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2662m | \-Xmx2662m | 
| mapreduce\.map\.memory\.mb | 1664 | 1664 | 
| mapreduce\.reduce\.memory\.mb | 3328 | 3328 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3328 | 3328 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53248 | 26624 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53248 | 26624 | 

### c4 instances<a name="emr-hadoop-task-config-c4"></a>


**c4\.large**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx717m | \-Xmx717m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1434m | \-Xmx1434m | 
| mapreduce\.map\.memory\.mb | 896 | 896 | 
| mapreduce\.reduce\.memory\.mb | 1792 | 1792 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 1792 | 1792 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 1792 | 896 | 
| yarn\.nodemanager\.resource\.memory\-mb | 1792 | 896 | 


**c4\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2253m | \-Xmx2253m | 
| mapreduce\.map\.memory\.mb | 1408 | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 2816 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 2816 | 


**c4\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11520 | 5760 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11520 | 5760 | 


**c4\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23040 | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23040 | 11520 | 


**c4\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1183m | \-Xmx1183m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2366m | \-Xmx2366m | 
| mapreduce\.map\.memory\.mb | 1479 | 1479 | 
| mapreduce\.reduce\.memory\.mb | 2958 | 2958 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2958 | 2958 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53248 | 26624 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53248 | 26624 | 

### c5 instances<a name="emr-hadoop-task-config-c5"></a>


**c5\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 6144 | 


**c5\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**c5\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**c5\.9xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1456m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2912m | 
| mapreduce\.map\.memory\.mb | 1820 | 
| mapreduce\.reduce\.memory\.mb | 3640 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3640 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 65536 | 
| yarn\.nodemanager\.resource\.memory\-mb | 65536 | 


**c5\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1502m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3004m | 
| mapreduce\.map\.memory\.mb | 1877 | 
| mapreduce\.reduce\.memory\.mb | 3754 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3754 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 90112 | 
| yarn\.nodemanager\.resource\.memory\-mb | 90112 | 


**c5\.18xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1547m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3094m | 
| mapreduce\.map\.memory\.mb | 1934 | 
| mapreduce\.reduce\.memory\.mb | 3868 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3868 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 139264 | 
| yarn\.nodemanager\.resource\.memory\-mb | 139264 | 


**c5\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1570m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3140m | 
| mapreduce\.map\.memory\.mb | 1963 | 
| mapreduce\.reduce\.memory\.mb | 3926 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3926 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 

### c5a instances<a name="emr-hadoop-task-config-c5a"></a>


**c5a\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 


**c5a\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**c5a\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**c5a\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1357m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2714m | 
| mapreduce\.map\.memory\.mb | 1696 | 
| mapreduce\.reduce\.memory\.mb | 3392 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3392 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**c5a\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1502m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3004m | 
| mapreduce\.map\.memory\.mb | 1877 | 
| mapreduce\.reduce\.memory\.mb | 3754 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3754 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 90112 | 
| yarn\.nodemanager\.resource\.memory\-mb | 90112 | 


**c5a\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1459m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3004m | 
| mapreduce\.map\.memory\.mb | 1824 | 
| mapreduce\.reduce\.memory\.mb | 3648 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3648 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**c5a\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1494m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2988m | 
| mapreduce\.map\.memory\.mb | 1867 | 
| mapreduce\.reduce\.memory\.mb | 3734 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3734 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 179200 | 
| yarn\.nodemanager\.resource\.memory\-mb | 179200 | 

### c5ad instances<a name="emr-hadoop-task-config-c5ad"></a>


**c5ad\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 


**c5ad\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**c5ad\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**c5ad\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1357m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2714m | 
| mapreduce\.map\.memory\.mb | 1696 | 
| mapreduce\.reduce\.memory\.mb | 3392 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3392 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**c5ad\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1425m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1425m | 
| mapreduce\.map\.memory\.mb | 1781 | 
| mapreduce\.reduce\.memory\.mb | 3562 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3562 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**c5ad\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1459m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2918m | 
| mapreduce\.map\.memory\.mb | 1824 | 
| mapreduce\.reduce\.memory\.mb | 3648 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3648 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**c5ad\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1494m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2988m | 
| mapreduce\.map\.memory\.mb | 1867 | 
| mapreduce\.reduce\.memory\.mb | 3734 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3734 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 179200 | 
| yarn\.nodemanager\.resource\.memory\-mb | 179200 | 

### c5d instances<a name="emr-hadoop-task-config-c5d"></a>


**c5d\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 6144 | 


**c5d\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**c5d\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**c5d\.9xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1456m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2912m | 
| mapreduce\.map\.memory\.mb | 1820 | 
| mapreduce\.reduce\.memory\.mb | 3640 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3640 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 65536 | 
| yarn\.nodemanager\.resource\.memory\-mb | 65536 | 


**c5d\.18xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1547m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3094m | 
| mapreduce\.map\.memory\.mb | 1934 | 
| mapreduce\.reduce\.memory\.mb | 3868 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3868 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 139264 | 
| yarn\.nodemanager\.resource\.memory\-mb | 139264 | 

### c5n instances<a name="emr-hadoop-task-config-c5n"></a>


**c5n\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1613m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3226m | 
| mapreduce\.map\.memory\.mb | 2016 | 
| mapreduce\.reduce\.memory\.mb | 4032 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 4032 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8064 | 
| yarn\.nodemanager\.resource\.memory\-mb | 8064 | 


**c5n\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1613m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3226m | 
| mapreduce\.map\.memory\.mb | 2016 | 
| mapreduce\.reduce\.memory\.mb | 4032 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 4032 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 16128 | 
| yarn\.nodemanager\.resource\.memory\-mb | 16128 | 


**c5n\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1741m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3482m | 
| mapreduce\.map\.memory\.mb | 2176 | 
| mapreduce\.reduce\.memory\.mb | 4352 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 4352 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 34816 | 
| yarn\.nodemanager\.resource\.memory\-mb | 34816 | 


**c5n\.9xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2002m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4004m | 
| mapreduce\.map\.memory\.mb | 2503 | 
| mapreduce\.reduce\.memory\.mb | 5006 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5006 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 90112 | 
| yarn\.nodemanager\.resource\.memory\-mb | 90112 | 


**c5n\.18xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2094m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4188m | 
| mapreduce\.map\.memory\.mb | 2617 | 
| mapreduce\.reduce\.memory\.mb | 5234 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5234 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 

### c6g instances<a name="emr-hadoop-task-config-c6g"></a>


**c6g\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126 | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 


**c6g\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**c6g\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**c6g\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1375m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2714m | 
| mapreduce\.map\.memory\.mb | 1696 | 
| mapreduce\.reduce\.memory\.mb | 3392 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3392 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**c6g\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1425m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2850m | 
| mapreduce\.map\.memory\.mb | 1781 | 
| mapreduce\.reduce\.memory\.mb | 3562 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3562 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**c6g\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1459m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2918m | 
| mapreduce\.map\.memory\.mb | 1824 | 
| mapreduce\.reduce\.memory\.mb | 3648 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3648 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 

### c6gd instances<a name="emr-hadoop-task-config-c6gd"></a>


**c6gd\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 


**c6gd\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**c6gd\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**c6gd\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1357m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2714m | 
| mapreduce\.map\.memory\.mb | 1696 | 
| mapreduce\.reduce\.memory\.mb | 3392 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3392 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**c6gd\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1425m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2850m | 
| mapreduce\.map\.memory\.mb | 1781 | 
| mapreduce\.reduce\.memory\.mb | 3562 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3562 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**c6gd\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1459m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2918m | 
| mapreduce\.map\.memory\.mb | 1824 | 
| mapreduce\.reduce\.memory\.mb | 3648 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3648 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 

### c6gn instances<a name="emr-hadoop-task-config-c6gn"></a>


**c6gn\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1126m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2252m | 
| mapreduce\.map\.memory\.mb | 1408 | 
| mapreduce\.reduce\.memory\.mb | 2816 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2816 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5632 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5632 | 


**c6gn\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**c6gn\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1171m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2342m | 
| mapreduce\.map\.memory\.mb | 1464 | 
| mapreduce\.reduce\.memory\.mb | 2928 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2928 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**c6gn\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1357m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2714m | 
| mapreduce\.map\.memory\.mb | 1696 | 
| mapreduce\.reduce\.memory\.mb | 3392 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3392 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**c6gn\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1425m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2850m | 
| mapreduce\.map\.memory\.mb | 1781 | 
| mapreduce\.reduce\.memory\.mb | 3562 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3562 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**c6gn\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1459m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2918m | 
| mapreduce\.map\.memory\.mb | 1824 | 
| mapreduce\.reduce\.memory\.mb | 3648 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3648 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 

### cc2 instances<a name="emr-hadoop-task-config-cc2"></a>


**cc2\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 56320 | 28160 | 
| yarn\.nodemanager\.resource\.memory\-mb | 56320 | 28160 | 

### cg1 instances<a name="emr-hadoop-task-config-cg1"></a>


**cg1\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5120 | 10240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 20480 | 10240 | 

### cr1 instances<a name="emr-hadoop-task-config-cr1"></a>


**cr1\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 

### d2 instances<a name="emr-hadoop-task-config-d2"></a>


**d2\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4685m | \-Xmx4685m | 
| mapreduce\.map\.memory\.mb | 2928 | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 11712 | 


**d2\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 27136 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 27136 | 


**d2\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5836m | \-Xmx5836m | 
| mapreduce\.map\.memory\.mb | 3648 | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 87552 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 87552 | 


**d2\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2417m | \-Xmx2417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4384m | \-Xmx4834m | 
| mapreduce\.map\.memory\.mb | 3021 | 3021 | 
| mapreduce\.reduce\.memory\.mb | 6042 | 6042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6042 | 6042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211470 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211470 | 

### d3 instances<a name="emr-hadoop-task-config-d3"></a>


**d3\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**d3\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m | 
| mapreduce\.map\.memory\.mb | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**d3\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**d3\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 

### d3en instances<a name="emr-hadoop-task-config-d3"></a>


**d3en\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**d3en\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**d3en\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**d3en\.6xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2850m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5700m | 
| mapreduce\.map\.memory\.mb | 3563 | 
| mapreduce\.reduce\.memory\.mb | 7126 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7126 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**d3en\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5700m | 
| mapreduce\.map\.memory\.mb | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**d3en\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5700m | 
| mapreduce\.map\.memory\.mb | 3733 | 
| mapreduce\.reduce\.memory\.mb | 7466 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7466 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 179200 | 
| yarn\.nodemanager\.resource\.memory\-mb | 179200 | 

### g2 instances<a name="emr-hadoop-task-config-g2"></a>


**g2\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 768 | 768 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 6144 | 

### g3 instances<a name="emr-hadoop-task-config-g3"></a>


**g3\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**g3\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 


**g3\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 

### g3s instances<a name="emr-hadoop-task-config-g3s"></a>


**g3s\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 

### g4dn instances<a name="emr-hadoop-task-config-g4dn"></a>


**g4dn\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**g4dn\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**g4dn\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2867m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5734m | 
| mapreduce\.map\.memory\.mb | 3584 | 
| mapreduce\.reduce\.memory\.mb | 7168 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7168 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**g4dn\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3072m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6144m | 
| mapreduce\.map\.memory\.mb | 3840 | 
| mapreduce\.reduce\.memory\.mb | 7680 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7680 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**g4dn\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3140m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6280m | 
| mapreduce\.map\.memory\.mb | 3925 | 
| mapreduce\.reduce\.memory\.mb | 7850 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7850 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**g4dn\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3174m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6348m | 
| mapreduce\.map\.memory\.mb | 3968 | 
| mapreduce\.reduce\.memory\.mb | 7936 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7936 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 

### hi1 instances<a name="emr-hadoop-task-config-hi1"></a>


**hi1\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2688m | \-Xmx2688m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5376m | \-Xmx5376m | 
| mapreduce\.map\.memory\.mb | 3360 | 3360 | 
| mapreduce\.reduce\.memory\.mb | 6720 | 6720 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6720 | 6720 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53760 | 26880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53760 | 26880 | 

### hs1 instances<a name="emr-hadoop-task-config-hs1"></a>


**hs1\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 28160 | 
| yarn\.nodemanager\.resource\.memory\-mb | 56320 | 28160 | 

### i2 instances<a name="emr-hadoop-task-config-i2"></a>


**i2\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 11712 | 


**i2\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 27136 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 27136 | 


**i2\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5836m | \-Xmx5836m | 
| mapreduce\.map\.memory\.mb | 3648 | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 87552 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 87552 | 


**i2\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 

### i3 instances<a name="emr-hadoop-task-config-i3"></a>


**i3\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m  | 
| mapreduce\.map\.memory\.mb | 5856  | 
| mapreduce\.reduce\.memory\.mb | 11712  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424  | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424  | 


**i3\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m  | 
| mapreduce\.map\.memory\.mb | 6784  | 
| mapreduce\.reduce\.memory\.mb | 13568  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272  | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272  | 


**i3\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m  | 
| mapreduce\.map\.memory\.mb | 7296  | 
| mapreduce\.reduce\.memory\.mb | 14592  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736  | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736  | 


**i3\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12083m  | 
| mapreduce\.map\.memory\.mb | 7552  | 
| mapreduce\.reduce\.memory\.mb | 15104  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664  | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664  | 


**i3\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m  | 
| mapreduce\.map\.memory\.mb | 7680  | 
| mapreduce\.reduce\.memory\.mb | 15360  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520  | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520  | 

### i3en instances<a name="emr-hadoop-task-config-i3en"></a>


**i3en\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4915m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9830m | 
| mapreduce\.map\.memory\.mb | 6144 | 
| mapreduce\.reduce\.memory\.mb | 12288 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 12288 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**i3en\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5734m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11468m | 
| mapreduce\.map\.memory\.mb | 7168 | 
| mapreduce\.reduce\.memory\.mb | 14336 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14336 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**i3en\.3xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6007m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12014m | 
| mapreduce\.map\.memory\.mb | 7509 | 
| mapreduce\.reduce\.memory\.mb | 15018 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15018 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 90112 | 
| yarn\.nodemanager\.resource\.memory\-mb | 90112 | 


**i3en\.6xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6281m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12562m | 
| mapreduce\.map\.memory\.mb | 7851 | 
| mapreduce\.reduce\.memory\.mb | 15702 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15702 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**i3en\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12834m | 
| mapreduce\.map\.memory\.mb | 8021 | 
| mapreduce\.reduce\.memory\.mb | 16042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 


**i3en\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6486m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12972m | 
| mapreduce\.map\.memory\.mb | 8107 | 
| mapreduce\.reduce\.memory\.mb | 16214 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16214 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 778240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 778240 | 

### m1 instances<a name="emr-hadoop-task-config-m1"></a>


**m1\.medium**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx768m | 
| mapreduce\.map\.memory\.mb | 768 | 
| mapreduce\.reduce\.memory\.mb | 1024 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 1024 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 2048 | 
| yarn\.nodemanager\.resource\.memory\-mb | 2048 | 


**m1\.large**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1024m | \-Xmx1024m | 
| mapreduce\.map\.memory\.mb | 768 | 768 | 
| mapreduce\.reduce\.memory\.mb | 1536 | 1536 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 1536 | 1536 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5120 | 2560 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5120 | 2560 | 


**m1\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 768 | 768 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 6144 | 

### m2 instances<a name="emr-hadoop-task-config-m2"></a>


**m2\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx864m | \-Xmx864m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 1024 | 1024 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 7168 | 7168 | 
| yarn\.nodemanager\.resource\.memory\-mb | 14336 | 7168 | 


**m2\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 15360 | 
| yarn\.nodemanager\.resource\.memory\-mb | 61440 | 15360 | 


**m2\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 30720 | 
| yarn\.nodemanager\.resource\.memory\-mb | 61440 | 30720 | 

### m3 instances<a name="emr-hadoop-task-config-m3"></a>


**m3\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23040 | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23040 | 11520 | 

### m4 instances<a name="emr-hadoop-task-config-m4"></a>


**m4\.large**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 1536 | 3072 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 6144 | 3072 | 
| yarn\.nodemanager\.resource\.memory\-mb | 6144 | 3072 | 


**m4\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 6144 | 


**m4\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1229m | \-Xmx1229m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2458m | \-Xmx2458m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 3072 | 3072 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3072 | 3072 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 12288 | 


**m4\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1434m | \-Xmx1434m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2868m | \-Xmx2868m | 
| mapreduce\.map\.memory\.mb | 1792 | 1792 | 
| mapreduce\.reduce\.memory\.mb | 3584 | 3584 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3584 | 3584 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 28672 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 28672 | 


**m4\.10xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1557m | \-Xmx1557m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3114m | \-Xmx3114m | 
| mapreduce\.map\.memory\.mb | 1946 | 1946 | 
| mapreduce\.reduce\.memory\.mb | 3892 | 3892 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3892 | 3892 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 155648 | 124544 | 
| yarn\.nodemanager\.resource\.memory\-mb | 155648 | 124544 | 


**m4\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1587m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3174m | 
| mapreduce\.map\.memory\.mb | 1984 | 
| mapreduce\.reduce\.memory\.mb | 3968 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3968 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 

### m5 instances<a name="emr-hadoop-task-config-m5"></a>


**m5\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**m5\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**m5\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2867m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5734m | 
| mapreduce\.map\.memory\.mb | 3584 | 
| mapreduce\.reduce\.memory\.mb | 7168 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7168 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**m5\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3072m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6144m | 
| mapreduce\.map\.memory\.mb | 3840 | 
| mapreduce\.reduce\.memory\.mb | 7680 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7680 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**m5\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3140m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6280m | 
| mapreduce\.map\.memory\.mb | 3925 | 
| mapreduce\.reduce\.memory\.mb | 7850 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7850 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**m5\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3174m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6348m | 
| mapreduce\.map\.memory\.mb | 3968 | 
| mapreduce\.reduce\.memory\.mb | 7936 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7936 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**m5\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3209m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6418m | 
| mapreduce\.map\.memory\.mb | 4011 | 
| mapreduce\.reduce\.memory\.mb | 8022 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 8022 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 

### m5a instances<a name="emr-hadoop-task-config-m5a"></a>


**m5a\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**m5a\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**m5a\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2867m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5734m | 
| mapreduce\.map\.memory\.mb | 3584 | 
| mapreduce\.reduce\.memory\.mb | 7168 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7168 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**m5a\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**m5a\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3140m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6280m | 
| mapreduce\.map\.memory\.mb | 3925 | 
| mapreduce\.reduce\.memory\.mb | 7850 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7850 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**m5a\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6349m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12698m | 
| mapreduce\.map\.memory\.mb | 7936 | 
| mapreduce\.reduce\.memory\.mb | 15872 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15872 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**m5a\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3209m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6418m | 
| mapreduce\.map\.memory\.mb | 4011 | 
| mapreduce\.reduce\.memory\.mb | 8022 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 8022 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 

### m5d instances<a name="emr-hadoop-task-config-m5d"></a>


**m5d\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 12288 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 


**m5d\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2458m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4916m | 
| mapreduce\.map\.memory\.mb | 3072 | 
| mapreduce\.reduce\.memory\.mb | 6144 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6144 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**m5d\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2867m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5734m | 
| mapreduce\.map\.memory\.mb | 3584 | 
| mapreduce\.reduce\.memory\.mb | 7168 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7168 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**m5d\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**m5d\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3140m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6280m | 
| mapreduce\.map\.memory\.mb | 3925 | 
| mapreduce\.reduce\.memory\.mb | 7850 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7850 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**m5d\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6349m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12698m | 
| mapreduce\.map\.memory\.mb | 7936 | 
| mapreduce\.reduce\.memory\.mb | 15872 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15872 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**m5d\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3209m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6418m | 
| mapreduce\.map\.memory\.mb | 4011 | 
| mapreduce\.reduce\.memory\.mb | 8022 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 8022 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 

### m5zn instances<a name="emr-hadoop-task-config-m5zn"></a>


**m5zn\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2304m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4608m | 
| mapreduce\.map\.memory\.mb | 2880 | 
| mapreduce\.reduce\.memory\.mb | 5760 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5760 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11520 | 


**m5zn\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2304m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4608m | 
| mapreduce\.map\.memory\.mb | 2880 | 
| mapreduce\.reduce\.memory\.mb | 5760 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5760 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11520 | 


**m5zn\.3xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2304m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5154m | 
| mapreduce\.map\.memory\.mb | 3221 | 
| mapreduce\.reduce\.memory\.mb | 6442 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6442 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 38656 | 
| yarn\.nodemanager\.resource\.memory\-mb | 38656 | 


**m5zn\.6xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2850m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5700m | 
| mapreduce\.map\.memory\.mb | 3563 | 
| mapreduce\.reduce\.memory\.mb | 7126 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7126 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 85504 | 
| yarn\.nodemanager\.resource\.memory\-mb | 85504 | 


**m5zn\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2986m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5972m | 
| mapreduce\.map\.memory\.mb | 3733 | 
| mapreduce\.reduce\.memory\.mb | 7466 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7466 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 179200 | 
| yarn\.nodemanager\.resource\.memory\-mb | 179200 | 

### m6g instances<a name="emr-hadoop-task-config-m6g"></a>


**m6g\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**m6g\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**m6g\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**m6g\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5836m | 
| mapreduce\.map\.memory\.mb | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**m6g\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 181248 | 
| yarn\.nodemanager\.resource\.memory\-mb | 181248 | 


**m6g\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 

### m6gd instances<a name="emr-hadoop-task-config-m6gd"></a>


**m6gd\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 11712 | 


**m6gd\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**m6gd\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**m6gd\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5836m | 
| mapreduce\.map\.memory\.mb | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**m6gd\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 181248 | 
| yarn\.nodemanager\.resource\.memory\-mb | 181248 | 


**m6gd\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 

### p2 instances<a name="emr-hadoop-task-config-p2"></a>


**p2\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx10854m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx21708m  | 
| mapreduce\.map\.memory\.mb | 13568  | 
| mapreduce\.reduce\.memory\.mb | 27136  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 27136  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272  | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272  | 


**p2\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx12288m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx24576  | 
| mapreduce\.map\.memory\.mb | 15360  | 
| mapreduce\.reduce\.memory\.mb | 30720  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 30720  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520  | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520  | 


**p2\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx9267m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx18534m  | 
| mapreduce\.map\.memory\.mb | 11584  | 
| mapreduce\.reduce\.memory\.mb | 23168  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 23168  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 741376  | 
| yarn\.nodemanager\.resource\.memory\-mb | 741376  | 

### p3 instances<a name="emr-hadoop-task-config-p3"></a>


**p3\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m  | 
| mapreduce\.map\.memory\.mb | 6784  | 
| mapreduce\.reduce\.memory\.mb | 13568  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272  | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272  | 


**p3\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m  | 
| mapreduce\.map\.memory\.mb | 7552  | 
| mapreduce\.reduce\.memory\.mb | 15104  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664  | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664  | 


**p3\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m  | 
| mapreduce\.map\.memory\.mb | 7680  | 
| mapreduce\.reduce\.memory\.mb | 15360  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520  | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520  | 

### r3 instances<a name="emr-hadoop-task-config-r3"></a>


**r3\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 2928 | 2928 | 
| mapreduce\.reduce\.memory\.mb | 5856 | 5856 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 5856 | 5856 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 11712 | 


**r3\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2714m | \-Xmx2714m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5428m | \-Xmx5428m | 
| mapreduce\.map\.memory\.mb | 3392 | 3392 | 
| mapreduce\.reduce\.memory\.mb | 6784 | 6784 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6784 | 6784 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 27136 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 27136 | 


**r3\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2918m | \-Xmx2918m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5836m | \-Xmx5836m | 
| mapreduce\.map\.memory\.mb | 3648 | 3648 | 
| mapreduce\.reduce\.memory\.mb | 7296 | 7296 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7296 | 7296 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 87552 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 87552 | 


**r3\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 

### r4 instances<a name="emr-hadoop-task-config-r4"></a>

**Note**  
R4 instances are available only in Amazon EMR release version 5\.4\.0 and later\.


**r4\.xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 5856 | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 11712 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 11712 | 


**r4\.2xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m | \-Xmx10854m | 
| mapreduce\.map\.memory\.mb | 6784 | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 27136 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 27136 | 


**r4\.4xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 87552 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 87552 | 


**r4\.8xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 


**r4\.16xlarge**  

| Configuration option | Default value | With HBase installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | \-Xmx1228m | 
| mapreduce\.map\.memory\.mb | 7680 | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 460800 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 460800 | 

### r5 instances<a name="emr-hadoop-task-config-r5"></a>


**r5\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4915m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9830m | 
| mapreduce\.map\.memory\.mb | 6144 | 
| mapreduce\.reduce\.memory\.mb | 12288 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 12288 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**r5\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5734m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11468m | 
| mapreduce\.map\.memory\.mb | 7168 | 
| mapreduce\.reduce\.memory\.mb | 14336 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14336 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**r5\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**r5\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6349m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12698m | 
| mapreduce\.map\.memory\.mb | 7936 | 
| mapreduce\.reduce\.memory\.mb | 15872 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15872 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**r5\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12834m | 
| mapreduce\.map\.memory\.mb | 8021 | 
| mapreduce\.reduce\.memory\.mb | 16042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 


**r5\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6451m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12902m | 
| mapreduce\.map\.memory\.mb | 8064 | 
| mapreduce\.reduce\.memory\.mb | 16128 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16128 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 516096 | 
| yarn\.nodemanager\.resource\.memory\-mb | 516096 | 


**r5\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6486m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12972m | 
| mapreduce\.map\.memory\.mb | 8107 | 
| mapreduce\.reduce\.memory\.mb | 16214 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16214 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 778240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 778240 | 

### r5a instances<a name="emr-hadoop-task-config-r5a"></a>


**r5a\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4915m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9830m | 
| mapreduce\.map\.memory\.mb | 6144 | 
| mapreduce\.reduce\.memory\.mb | 12288 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 12288 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**r5a\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5734m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11468m | 
| mapreduce\.map\.memory\.mb | 7168 | 
| mapreduce\.reduce\.memory\.mb | 14336 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14336 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**r5a\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**r5a\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6349m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12698m | 
| mapreduce\.map\.memory\.mb | 7936 | 
| mapreduce\.reduce\.memory\.mb | 15872 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15872 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**r5a\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12834m | 
| mapreduce\.map\.memory\.mb | 8021 | 
| mapreduce\.reduce\.memory\.mb | 16042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 


**r5a\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6451m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12902m | 
| mapreduce\.map\.memory\.mb | 8064 | 
| mapreduce\.reduce\.memory\.mb | 16128 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16128 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 516096 | 
| yarn\.nodemanager\.resource\.memory\-mb | 516096 | 


**r5a\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6486m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12972m | 
| mapreduce\.map\.memory\.mb | 8107 | 
| mapreduce\.reduce\.memory\.mb | 16214 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16214 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 778240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 778240 | 

### r5b instances<a name="emr-hadoop-task-config-r5b"></a>


**r5b\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**r5b\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m | 
| mapreduce\.map\.memory\.mb | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**r5b\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**r5b\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 


**r5b\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6110m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12220m | 
| mapreduce\.map\.memory\.mb | 7637 | 
| mapreduce\.reduce\.memory\.mb | 15274 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15274 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 366592 | 
| yarn\.nodemanager\.resource\.memory\-mb | 366592 | 


**r5b\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 


**r5b\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6178m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12356m | 
| mapreduce\.map\.memory\.mb | 7723 | 
| mapreduce\.reduce\.memory\.mb | 15446 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15446 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 741376 | 
| yarn\.nodemanager\.resource\.memory\-mb | 741376 | 

### r5d instances<a name="emr-hadoop-task-config-r5d"></a>


**r5d\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4915m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9830m | 
| mapreduce\.map\.memory\.mb | 6144 | 
| mapreduce\.reduce\.memory\.mb | 12288 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 12288 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**r5d\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5734m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11468m | 
| mapreduce\.map\.memory\.mb | 7168 | 
| mapreduce\.reduce\.memory\.mb | 14336 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14336 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**r5d\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 122880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 122880 | 


**r5d\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6349m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12698m | 
| mapreduce\.map\.memory\.mb | 7936 | 
| mapreduce\.reduce\.memory\.mb | 15872 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15872 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**r5d\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12834m | 
| mapreduce\.map\.memory\.mb | 8021 | 
| mapreduce\.reduce\.memory\.mb | 16042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 


**r5d\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6451m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12902m | 
| mapreduce\.map\.memory\.mb | 8064 | 
| mapreduce\.reduce\.memory\.mb | 16128 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16128 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 516096 | 
| yarn\.nodemanager\.resource\.memory\-mb | 516096 | 


**r5d\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6486m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12972m | 
| mapreduce\.map\.memory\.mb | 8107 | 
| mapreduce\.reduce\.memory\.mb | 16214 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16214 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 778240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 778240 | 

### r5dn instances<a name="emr-hadoop-task-config-r5dn"></a>


**r5dn\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**r5dn\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m | 
| mapreduce\.map\.memory\.mb | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**r5dn\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 14592 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**r5dn\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 


**r5dn\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12220m | 
| mapreduce\.map\.memory\.mb | 7637 | 
| mapreduce\.reduce\.memory\.mb | 15274 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15274 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 366592 | 
| yarn\.nodemanager\.resource\.memory\-mb | 366592 | 


**r5dn\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 


**r5dn\.24xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6178m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12356m | 
| mapreduce\.map\.memory\.mb | 7723 | 
| mapreduce\.reduce\.memory\.mb | 15446 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15446 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 741376 | 
| yarn\.nodemanager\.resource\.memory\-mb | 741376 | 

### r6g instances<a name="emr-hadoop-task-config-r6g"></a>


**r6g\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2342m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4684m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**r6g\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10584m | 
| mapreduce\.map\.memory\.mb | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**r6g\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**r6g\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 


**r6g\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6110m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12220m | 
| mapreduce\.map\.memory\.mb | 7637 | 
| mapreduce\.reduce\.memory\.mb | 15274 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15274 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 366592 | 
| yarn\.nodemanager\.resource\.memory\-mb | 366592 | 


**r6g\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 

### r6gd instances<a name="emr-hadoop-task-config-r6gd"></a>


**r6gd\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4685m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9370m | 
| mapreduce\.map\.memory\.mb | 5856 | 
| mapreduce\.reduce\.memory\.mb | 11712 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 11712 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23424 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23424 | 


**r6gd\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5427m | 
| mapreduce\.reduce\.java\.opts | \-Xmx10854m | 
| mapreduce\.map\.memory\.mb | 6784 | 
| mapreduce\.reduce\.memory\.mb | 13568 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 13568 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 54272 | 
| yarn\.nodemanager\.resource\.memory\-mb | 54272 | 


**r6gd\.4xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5837m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11674m | 
| mapreduce\.map\.memory\.mb | 7296 | 
| mapreduce\.reduce\.memory\.mb | 14592 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14592 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 116736 | 
| yarn\.nodemanager\.resource\.memory\-mb | 116736 | 


**r6gd\.8xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 


**r6gd\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6110m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12220m | 
| mapreduce\.map\.memory\.mb | 7637 | 
| mapreduce\.reduce\.memory\.mb | 15274 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15274 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 366592 | 
| yarn\.nodemanager\.resource\.memory\-mb | 366592 | 


**r6gd\.16xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | 
| mapreduce\.map\.memory\.mb | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 

### z1d instances<a name="emr-hadoop-task-config-z1d"></a>


**z1d\.xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx4915m | 
| mapreduce\.reduce\.java\.opts | \-Xmx9830m | 
| mapreduce\.map\.memory\.mb | 6144 | 
| mapreduce\.reduce\.memory\.mb | 12288 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 12288 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 24576 | 
| yarn\.nodemanager\.resource\.memory\-mb | 24576 | 


**z1d\.2xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx5734m | 
| mapreduce\.reduce\.java\.opts | \-Xmx11468m | 
| mapreduce\.map\.memory\.mb | 7168 | 
| mapreduce\.reduce\.memory\.mb | 14336 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 14336 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 57344 | 
| yarn\.nodemanager\.resource\.memory\-mb | 57344 | 


**z1d\.3xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6007m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12014m | 
| mapreduce\.map\.memory\.mb | 7509 | 
| mapreduce\.reduce\.memory\.mb | 15018 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15018 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 90112 | 
| yarn\.nodemanager\.resource\.memory\-mb | 90112 | 


**z1d\.6xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6281m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12562m | 
| mapreduce\.map\.memory\.mb | 7851 | 
| mapreduce\.reduce\.memory\.mb | 15702 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15702 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 188416 | 
| yarn\.nodemanager\.resource\.memory\-mb | 188416 | 


**z1d\.12xlarge**  

| Configuration option | Default value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12834m | 
| mapreduce\.map\.memory\.mb | 8021 | 
| mapreduce\.reduce\.memory\.mb | 16042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 16042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 385024 | 
| yarn\.nodemanager\.resource\.memory\-mb | 385024 | 