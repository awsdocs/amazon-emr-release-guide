# Finding the Flink Web Interface<a name="flink-web-interface"></a>

The Application Master that belongs to the Flink application hosts the Flink web interface, which is an alternative way to submit a JAR as a job or to view the current status of other jobs\. The Flink web interface is active as long as you have a Flink session running\. If you have a long\-running YARN job already active, you can follow the instructions in the [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) topic in the *Amazon EMR Management Guide* to connect to the YARN ResourceManager\. For example, if you’ve set up an SSH tunnel and have activated a proxy in your browser, you choose the ResourceManager connection under **Connections ** in your EMR cluster details page\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/resourcemanager.png)

After you find the ResourceManager, select the YARN application that’s hosting a Flink session\. Choose the link under the **Tracking UI** column\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/resourcemanager2.png)

In the Flink web interface, you can view configuration, submit your own custom JAR as a job, or monitor jobs in progress\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/images/flink.png)