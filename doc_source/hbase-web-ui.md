# View the HBase User Interface<a name="hbase-web-ui"></a>

HBase provides a web\-based user interface that you can use to monitor your HBase cluster\. When you run HBase on Amazon EMR, the web interface runs on the master node and can be viewed using port forwarding, also known as creating an SSH tunnel\. 

**To view the HBase User Interface**

1. Use SSH to tunnel into the master node and create a secure connection\. For more information, see [Option 2, Part 1: Set Up an SSH Tunnel to the Master Node Using Dynamic Port Forwarding](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ssh-tunnel.html) in the *Amazon EMR Management Guide*\. 

1. Install a web browser with a proxy tool, such as the FoxyProxy plug\-in for Firefox, to create a SOCKS proxy for AWS domains\. For more information, see [Option 2, Part 2: Configure Proxy Settings to View Websites Hosted on the Master Node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-proxy.html) in the *Amazon EMR Management Guide*\. 

1. With the proxy set and the SSH connection open, you can view the HBase UI by opening a browser window with **http://*master\-public\-dns\-name*:16010/master\-status**, where *master\-public\-dns\-name* is the public DNS address of the cluster's master node\. 

![\[HMaster\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/hmaster.png)

You can also view HBase in Hue\. For example, the following shows the table, `t1`, created in [Using the HBase Shell](emr-hbase-connect.md):

![\[HMaster\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/huehbase.png)

 For more information about Hue, see [Hue](emr-hue.md)\.