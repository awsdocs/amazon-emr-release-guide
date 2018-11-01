# Using the HBase Shell<a name="emr-hbase-connect"></a>

After you create an HBase cluster, the next step is to connect to HBase so you can begin reading and writing data \(data writes are not supported on a read\-replica cluster\)\. You can use the [HBase shell](https://hbase.apache.org/book.html#shell) to test commands\.

**To open the HBase shell**

1. Use SSH to connect to the master server in the HBase cluster\. For information about how to connect to the master node using SSH, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\. 

1. Run `hbase shell`\. The HBase shell opens with a prompt similar to the following example: 

   ```
   hbase(main):001:0>
   ```

You can issue HBase shell commands from the prompt\. For more information about the shell commands and how to call them, type help at the HBase prompt and press Enter\. 

## Create a Table<a name="emr-hbase-create-table"></a>

The following command creates a table named 't1' that has a single column family named 'f1': 

```
hbase(main):001:0>create 't1', 'f1'
```

## Put a Value<a name="emr-hbase-put-value"></a>

The following command puts value 'v1' for row 'r1' in table 't1' and column 'f1':

```
hbase(main):001:0>put 't1', 'r1', 'f1:col1', 'v1'
```

## Get a Value<a name="emr-hbase-get-value"></a>

The following command gets the values for row 'r1' in table 't1': 

```
hbase(main):001:0>get 't1', 'r1'			
```