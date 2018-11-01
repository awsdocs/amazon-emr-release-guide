# Task Configuration<a name="emr-hadoop-task-config"></a>

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

When you use the `create-cluster` command from the AWS CLI, you can then reference the JSON configuration file\. In the following example, the configuration file is saved as `myConfig.json` and stored in Amazon S3\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --release-label emr-5.18.0 --instance-type m4.large \
--instance-count 3 --applications Name=Hadoop --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json \
--use-default-roles
```

You can change default values listed below using the `mapred-site` configuration classification in the same way, and set multiple values and multiple configuration classifications using a single JSON file\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

## Default Values for Task Configuration Settings<a name="emr-hadoop-task-jvm"></a>


**c1\.medium**  

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx864m | \-Xmx864m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 1024 | 1024 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 2048 | 2560 | 
| yarn\.nodemanager\.resource\.memory\-mb | 5120 | 2560 | 


**c3\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1331m | \-Xmx1331m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2662m | \-Xmx2662m | 
| mapreduce\.map\.memory\.mb | 1664 | 1664 | 
| mapreduce\.reduce\.memory\.mb | 3328 | 3328 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3328 | 3328 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53248 | 26624 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53248 | 26624 | 


**c4\.large**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1183m | \-Xmx1183m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2366m | \-Xmx2366m | 
| mapreduce\.map\.memory\.mb | 1479 | 1479 | 
| mapreduce\.reduce\.memory\.mb | 2958 | 2958 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2958 | 2958 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53248 | 26624 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53248 | 26624 | 


**cc2\.8xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 56320 | 28160 | 
| yarn\.nodemanager\.resource\.memory\-mb | 56320 | 28160 | 


**cg1\.4xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 5120 | 10240 | 
| yarn\.nodemanager\.resource\.memory\-mb | 20480 | 10240 | 


**cr1\.8xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12084m | \-Xmx12084m | 
| mapreduce\.map\.memory\.mb | 7552 | 7552 | 
| mapreduce\.reduce\.memory\.mb | 15104 | 15104 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15104 | 15104 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 


**d2\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2417m | \-Xmx2417m | 
| mapreduce\.reduce\.java\.opts | \-Xmx4384m | \-Xmx4834m | 
| mapreduce\.map\.memory\.mb | 3021 | 3021 | 
| mapreduce\.reduce\.memory\.mb | 6042 | 6042 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6042 | 6042 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211470 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211470 | 


**g2\.2xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 768 | 768 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 6144 | 


**hi1\.4xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx2688m | \-Xmx2688m | 
| mapreduce\.reduce\.java\.opts | \-Xmx5376m | \-Xmx5376m | 
| mapreduce\.map\.memory\.mb | 3360 | 3360 | 
| mapreduce\.reduce\.memory\.mb | 6720 | 6720 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 6720 | 6720 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 53760 | 26880 | 
| yarn\.nodemanager\.resource\.memory\-mb | 53760 | 26880 | 


**hs1\.8xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 28160 | 
| yarn\.nodemanager\.resource\.memory\-mb | 56320 | 28160 | 


**i2\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 


**i3\.xlarge**  

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m  | 
| mapreduce\.map\.memory\.mb | 7680  | 
| mapreduce\.reduce\.memory\.mb | 15360  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520  | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520  | 


**m1\.medium**  

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx512m | \-Xmx512m | 
| mapreduce\.reduce\.java\.opts | \-Xmx1536m | \-Xmx1536m | 
| mapreduce\.map\.memory\.mb | 768 | 768 | 
| mapreduce\.reduce\.memory\.mb | 2048 | 2048 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2048 | 2048 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 6144 | 
| yarn\.nodemanager\.resource\.memory\-mb | 12288 | 6144 | 


**m2\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1280m | \-Xmx1280m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1536 | 1536 | 
| mapreduce\.reduce\.memory\.mb | 2560 | 2560 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2560 | 2560 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 256 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 8192 | 30720 | 
| yarn\.nodemanager\.resource\.memory\-mb | 61440 | 30720 | 


**m3\.2xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1152m | \-Xmx1152m | 
| mapreduce\.reduce\.java\.opts | \-Xmx2304m | \-Xmx2304m | 
| mapreduce\.map\.memory\.mb | 1440 | 1440 | 
| mapreduce\.reduce\.memory\.mb | 2880 | 2880 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 2880 | 2880 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 23040 | 11520 | 
| yarn\.nodemanager\.resource\.memory\-mb | 23040 | 11520 | 


**m4\.large**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx1587m | 
| mapreduce\.reduce\.java\.opts | \-Xmx3174m | 
| mapreduce\.map\.memory\.mb | 1984 | 
| mapreduce\.reduce\.memory\.mb | 3968 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 3968 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 253952 | 
| yarn\.nodemanager\.resource\.memory\-mb | 253952 | 


**p2\.xlarge**  

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx9267m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx18534m  | 
| mapreduce\.map\.memory\.mb | 11584  | 
| mapreduce\.reduce\.memory\.mb | 23168  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 23168  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 741376  | 
| yarn\.nodemanager\.resource\.memory\-mb | 741376  | 


**p3\.2xlarge**  

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
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

| Configuration Option | Default Value | 
| --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m  | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m  | 
| mapreduce\.map\.memory\.mb | 7680  | 
| mapreduce\.reduce\.memory\.mb | 15360  | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360  | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520  | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520  | 


**r3\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx3021m | \-Xmx3021m | 
| mapreduce\.reduce\.java\.opts | \-Xmx6042m | \-Xmx6042m | 
| mapreduce\.map\.memory\.mb | 3776 | 3776 | 
| mapreduce\.reduce\.memory\.mb | 7552 | 7552 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 7552 | 7552 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 241664 | 211456 | 
| yarn\.nodemanager\.resource\.memory\-mb | 241664 | 211456 | 

**Note**  
R4 instances are available only in Amazon EMR release version 5\.4\.0 and later\.


**r4\.xlarge**  

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
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

| Configuration Option | Default Value | With HBase Installed | 
| --- | --- | --- | 
| mapreduce\.map\.java\.opts | \-Xmx6144m | \-Xmx6144m | 
| mapreduce\.reduce\.java\.opts | \-Xmx12288m | \-Xmx1228m | 
| mapreduce\.map\.memory\.mb | 7680 | 7680 | 
| mapreduce\.reduce\.memory\.mb | 15360 | 15360 | 
| yarn\.app\.mapreduce\.am\.resource\.mb | 15360 | 15360 | 
| yarn\.scheduler\.minimum\-allocation\-mb | 32 | 32 | 
| yarn\.scheduler\.maximum\-allocation\-mb | 491520 | 460800 | 
| yarn\.nodemanager\.resource\.memory\-mb | 491520 | 460800 | 