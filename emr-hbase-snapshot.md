# Using HBase Snapshots<a name="emr-hbase-snapshot"></a>

HBase uses a built\-in [snapshot](https://hbase.apache.org/book.html#ops.snapshots) functionality to create lightweight backups of tables\. In EMR clusters, these backups can be exported to Amazon S3 using EMRFS\. You can create a snapshot on the master node using the HBase shell\. This topic shows you how to run these commands interactively with the shell or through a step using `command-runner.jar` with either the AWS CLI or AWS SDK for Java\. For more information about other types of HBase backups, see [HBase Backup](https://hbase.apache.org/book.html#ops.backup) in the HBase documentation\.

## Create a snapshot using a table<a name="w3aac25c31b4"></a>

```
hbase snapshot create -n snapshotName -t tableName
```

Using command\-runner\.jar from the AWS CLI:

```
aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
--steps Name="HBase Shell Step",Jar="command-runner.jar",\
Args=[ "hbase", "snapshot", "create","-n","snapshotName","-t","tableName"]
```

AWS SDK for Java

```
HadoopJarStepConfig hbaseSnapshotConf = new HadoopJarStepConfig()
  .withJar("command-runner.jar")
  .withArgs("hbase","snapshot","create","-n","snapshotName","-t","tableName");
```

**Note**  
If your snapshot name is not unique, the create operation fails with a return code of `-1` or `255` but you may not see an error message that states what went wrong\. To use the same snapshot name, delete it and then re\-create it\.

## Delete a snapshot<a name="w3aac25c31b6"></a>

```
hbase shell
>> delete_snapshot 'snapshotName'
```

## View snapshot info<a name="w3aac25c31b8"></a>

```
hbase snapshot info -snapshot snapshotName
```

## Export a snapshot to Amazon S3<a name="w3aac25c31c10"></a>

**Important**  
If you do not specify a `-mappers` value when exporting a snapshot, HBase uses an arbitrary calculation to determine the number of mappers\. This value can be very large depending on your table size, which negatively affects running jobs during the export\. For this reason, we recommend that you specify the `-mappers` parameter, the `-bandwidth` parameter \(which specifies the bandwidth consumption in megabytes per second\), or both to limit the cluster resources used by the export operation\. Alternatively, you can run the export snapshot operation during a period of low usage\.

```
hbase snapshot export -snapshot snapshotName \
-copy-to s3://bucketName/folder -mappers 2
```

Using `command-runner.jar` from the AWS CLI:

```
aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
--steps Name="HBase Shell Step",Jar="command-runner.jar",\
Args=[ "hbase", "snapshot", "export","-snapshot","snapshotName","-copy-to","s3://bucketName/folder","-mappers","2","-bandwidth","50"]
```

AWS SDK for Java:

```
HadoopJarStepConfig hbaseImportSnapshotConf = new HadoopJarStepConfig()
  .withJar("command-runner.jar")
  .withArgs("hbase","snapshot","export",
      "-snapshot","snapshotName","-copy-to",
      "s3://bucketName/folder",
      "-mappers","2","-bandwidth","50");
```

## Import snapshot from Amazon S3<a name="w3aac25c31c12"></a>

Although this is an import, the HBase option used here is still `export`\.

```
sudo -u hbase hbase snapshot export \
-D hbase.rootdir=s3://bucketName/folder \
-snapshot snapshotName \
-copy-to hdfs://masterPublicDNSName:8020/user/hbase \
-mappers 2
```

Using `command-runner.jar` from the AWS CLI:

```
aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
--steps Name="HBase Shell Step",Jar="command-runner.jar", \
Args=["sudo","-u","hbase","hbase snapshot export","-snapshot","snapshotName", \
"-D","hbase.rootdir=s3://bucketName/folder", \
"-copy-to","hdfs://masterPublicDNSName:8020/user/hbase","-mappers","2","-chmod","700"]
```

AWS SDK for Java:

```
HadoopJarStepConfig hbaseImportSnapshotConf = new HadoopJarStepConfig()
  .withJar("command-runner.jar")
  .withArgs("sudo","-u","hbase","hbase","snapshot","export", "-D","hbase.rootdir=s3://path/to/snapshot",
      "-snapshot","snapshotName","-copy-to",
      "hdfs://masterPublicDNSName:8020/user/hbase",
      "-mappers","2","-chuser","hbase");
```

## Restore a table from snapshots within the HBase shell<a name="w3aac25c31c14"></a>

```
hbase shell
>> disable tableName
>> restore_snapshot snapshotName
>> enable tableName
```

HBase currently does not support all snapshot commands found in the HBase shell\. For example, there is no HBase command\-line option to restore a snapshot, so you must restore it within a shell\. This means that `command-runner.jar` must run a Bash command\. 

**Note**  
Because the command used here is `echo`, it is possible that your shell command will still fail even if the command run by Amazon EMR returns a `0` exit code\. Check the step logs if you choose to run a shell command as a step\.

```
echo 'disable tableName; \
restore_snapshot snapshotName; \
enable tableName' | hbase shell
```

Here is the step using the AWS CLI\. First, create the following `snapshot.json` file:

```
[
  {
    "Name": "restore",
    "Args": ["bash", "-c", "echo $'disable \"tableName\"; restore_snapshot \"snapshotName\"; enable \"tableName\"' | hbase shell"],
    "Jar": "command-runner.jar",
    "ActionOnFailure": "CONTINUE",
    "Type": "CUSTOM_JAR"
  }
]
```

```
aws emr add-steps --cluster-id j-2AXXXXXXGAPLF \
--steps file://./snapshot.json
```

AWS SDK for Java:

```
HadoopJarStepConfig hbaseRestoreSnapshotConf = new HadoopJarStepConfig()
  .withJar("command-runner.jar")
  .withArgs("bash","-c","echo $'disable \"tableName\"; restore_snapshot \"snapshotName\"; enable \"snapshotName\"' | hbase shell");
```