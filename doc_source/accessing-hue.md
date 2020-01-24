# Launching the Hue Web Interface<a name="accessing-hue"></a>

Launching Hue is the same as connecting to any HTTP interface hosted on the master node of a cluster\. The following procedure describes how to access the Hue interface\. For more information, see [View Web Interfaces Hosted on EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html) in the *Amazon EMR Management Guide*\.

**To launch the Hue web interface**

1. Follow these instructions to [Set Up an SSH TUnnel to the Master Node Using Dynamic Port Forwarding](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-ssh-tunnel.html) in the *Amazon EMR Management Guide*\.

1. Type the following address in your browser to open the **Hue** web interface: `http://master public DNS:8888` where *master public dns* is the public DNS name of your cluster master node, for example `ec2-11-22-333-44.compute-1.amazonaws.com`\.

1. At the Hue login screen, if you are the administrator logging in for the first time, enter a user name and password to create your Hue superuser account and then select **Create account**\. Otherwise, type your username and password and select **Create account** or enter the credentials provided by your administrator\.