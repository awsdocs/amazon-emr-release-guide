# Monitor HBase with Ganglia<a name="emr-hbase-ganglia"></a>

The Ganglia open\-source project is a scalable, distributed system designed to monitor clusters and grids while minimizing the impact on their performance\. When you enable Ganglia on your cluster, you can generate reports and view the performance of the cluster as a whole, as well as inspect the performance of individual node instances\. For more information about the Ganglia open\-source project, see [http://ganglia\.info/](http://ganglia.info/)\. For more information about using Ganglia with Amazon EMR clusters, see [Ganglia](emr-ganglia.md)\.

After the cluster is launched with Ganglia configured, you can access the Ganglia graphs and reports using the graphical interface running on the master node\. 

Ganglia stores log files on the master node in the `/mnt/var/lib/ganglia/rrds/` directory\. Earlier release versions of Amazon EMR may store log files in the `/var/log/ganglia/rrds/` directory\.

**To configure a cluster for Ganglia and HBase using the AWS CLI**
+ Use a `create-cluster` command similar to the following:

  ```
  aws emr create-cluster --name "Test cluster" --release-label emr-5.33.0 \
  --applications Name=HBase Name=Ganglia --use-default-roles \
  --ec2-attributes KeyName=myKey --instance-type m5.xlarge \
  --instance-count 3
  ```
**Note**  
If the default Amazon EMR service role and Amazon EC2 instance profile don't exist, an error occurs\. Use the `aws emr create-default-roles` command to create them and then try again\.

  For more information, see [Amazon EMR commands in the AWS CLI](https://docs.aws.amazon.com/cli/latest/reference/emr)\.

**To view HBase metrics in the Ganglia web interface**

1. Use SSH to tunnel into the master node and create a secure connection\. For more information, see [Option 2, part 1: Set up an SSH tunnel to the master node using dynamic port forwarding ](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ssh-tunnel.html) in the *Amazon EMR Management Guide*\. 

1. Install a web browser with a proxy tool, such as the FoxyProxy plug\-in for Firefox, to create a SOCKS proxy for AWS domains\. For more information, see [ Option 2, part 2: Configure proxy settings to view websites hosted on the master node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-proxy.html) in the *Amazon EMR Management Guide*\. 

1. With the proxy set and the SSH connection open, you can view the Ganglia metrics by opening a browser window with http://*master\-public\-dns\-name*/ganglia/, where *master\-public\-dns\-name* is the public DNS address of the master server in the HBase cluster\. 

**To view Ganglia log files on the master node**
+ If the cluster is still running, you can access the log files by using SSH to connect to the master node and navigating to the `/mnt/var/lib/ganglia/rrds/` directory\. For EMR 3\.x, navigate to the `/var/log/ganglia/rrds` directory\. For more information, see [Connect to the master node using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\. 

**To view Ganglia log files on Amazon S3**
+ The Ganglia log files are not automatically written to Amazon S3 even if you enable logging for your cluster\. To view Ganglia log files on Amazon S3, you must manually push the logs from `/mnt/var/lib/ganglia/rrds/` to the S3 bucket\. 