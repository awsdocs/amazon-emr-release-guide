# Using the Scala Shell<a name="flink-scala"></a>

Currently, the Flink Scala shell for EMR clusters is only configured to start new YARN sessions\. You can use the Scala shell by following the procedure below\.

**Using the Flink Scala shell on the master node**

1. Log in to the master node using SSH as described in [Connect to the Master Node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html)\.

1. Type the following to start a shell:

   In Amazon EMR version 5\.5\.0 and later, you can use:

   ```
   % flink-scala-shell yarn -n 1
   ```

   In earlier versions of Amazon EMR, use:

   ```
   % /usr/lib/flink/bin/start-scala-shell.sh yarn -n 1
   ```

   This starts the Flink Scala shell so you can interactively use Flink\. Just as with other interfaces and options, you can scale the `-n` option value used in the example based on the number of tasks you want to run from the shell\.