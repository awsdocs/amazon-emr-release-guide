# Using the Hudi CLI<a name="emr-hudi-cli"></a>

You can use the Hudi CLI to administer Hudi datasets to view information about commits, the filesystem, statistics, and more\. You can also use the CLI to manually perform compactions, schedule compactions, or cancel scheduled compactions\. For more information, see [Administering Hudi Pipelines](https://hudi.apache.org/admin_guide.html) in the Apache Hudi documentation\.

**To start the Hudi CLI and connect to a dataset**

1. Connect to the master node using SSH\. For more information, see [Connect to the Master Node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. At the command line, type `usr/lib/hudi/cli/bin/hudi-cli.sh`\.

   The command prompt changes to `hudi->`\.

1. Type the following code to connect to a dataset\. Replace *s3://mybucket/myhudidataset* with the path to the dataset that you want to work with\. The value we use is the same as the value established in earlier examples\.

   ```
   connect --path s3://mybucket/myhudidataset
   ```

   The command prompt changes to include the dataset that you're connected to, as shown in the following example\.

   ```
   hudi:myhudidataset->
   ```