# View Ganglia Metrics<a name="view_Ganglia"></a>

 Ganglia provides a web\-based user interface that you can use to view the metrics Ganglia collects\. When you run Ganglia on Amazon EMR, the web interface runs on the master node and can be viewed using port forwarding, also known as creating an SSH tunnel\. For more information about viewing web interfaces on Amazon EMR, see [View Web Interfaces Hosted on EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html) in the *Amazon EMR Management Guide*\.

**To view the Ganglia web interface**

1.  Use SSH to tunnel into the master node and create a secure connection\. For information about how to create an SSH tunnel to the master node, see [Option 2, Part 1: Set Up an SSH Tunnel to the Master Node Using Dynamic Port Forwarding](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ssh-tunnel.html) in the *Amazon EMR Management Guide*\.

1.  Install a web browser with a proxy tool, such as the FoxyProxy plug\-in for Firefox, to create a SOCKS proxy for domains of the type \*ec2\*\.amazonaws\.com\*\. For more information, see [Option 2, Part 2: Configure Proxy Settings to View Websites Hosted on the Master Node](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-proxy.html) in the *Amazon EMR Management Guide*\. 

1.  With the proxy set and the SSH connection open, you can view the Ganglia UI by opening a browser window with http://*master\-public\-dns\-name*/ganglia/, where *master\-public\-dns\-name* is the public DNS address of the master server in the EMR cluster\. 

![\[Ganglia cluster report\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/ganglianew.png)