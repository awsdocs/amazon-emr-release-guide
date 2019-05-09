# Use the Hive JDBC Driver<a name="HiveJDBCDriver"></a>

You can use popular business intelligence tools like Microsoft Excel, MicroStrategy, QlikView, and Tableau with Amazon EMR to explore and visualize your data\. Many of these tools require Java Database Connectivity \(JDBC\) driver or an Open Database Connectivity \(ODBC\) driver\. Amazon EMR supports both JDBC and ODBC connectivity\.

The example below demonstrates using SQL Workbench/J as a SQL client to connect to a Hive cluster in Amazon EMR\. For additional drivers, see [Use Business Intelligence Tools with Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-bi-tools.html)\.

Before you install and work with SQL Workbench/J, download the driver package and install the driver\. The drivers included in the package support the Hive versions available in Amazon EMR release versions 4\.0 and later\. For detailed release notes and documentation, see the PDF documentation included in the package\.
+ **JDBC Driver Package Download**

  [http://awssupportdatasvcs.com/bootstrap-actions/Simba/AmazonHiveJDBC-1.0.9.1060.zip](http://awssupportdatasvcs.com/bootstrap-actions/Simba/AmazonHiveJDBC-1.0.9.1060.zip)

**To install and configure SQL Workbench**

1. Download the SQL Workbench/J client for your operating system from [http://www.sql-workbench.net/downloads.html](http://www.sql-workbench.net/downloads.html)\.

1. Install SQL Workbench/J\. For more information, see [Installing and starting SQL Workbench/J](http://www.sql-workbench.net/manual/install.html) in the SQL Workbench/J Manual User's Manual\.

1. **Linux, Unix, Mac OS X users**: In a terminal session, create an SSH tunnel to the master node of your cluster using the following command\. Replace *master\-public\-dns\-name* with the public DNS name of the master node and *path\-to\-key\-file* with the location and file name of your Amazon EC2 private key \(`.pem`\) file\.

   ```
   ssh -o ServerAliveInterval=10 -i path-to-key-file -N -L 10000:localhost:10000 hadoop@master-public-dns-name
   ```

   **Windows users**: In a PuTTY session, create an SSH tunnel to the master node of your cluster \(using local port forwarding\) with `10000` for **Source port** and `master-public-dns-name:10000` for **Destination**\. Replace `master-public-dns-name` with the public DNS name of the master node\.

1. Add the JDBC driver to SQL Workbench\.

   1. In the **Select Connection Profile** dialog box, click **Manage Drivers**\. 

   1. Click the **Create a new entry** \(blank page\) icon\.

   1. In the **Name** field, type **Hive JDBC**\.

   1. For **Library**, click the **Select the JAR file\(s\)** icon\.

   1. Browse to the location containing the extracted drivers, select the following JAR files and click **Open**\.

      ```
      hive_metastore.jar
      hive_service.jar
      HiveJDBC41.jar
      libfb303-0.9.0.jar
      libthrift-0.9.0.jar
      log4j-1.2.14.jar
      ql.jar
      slf4j-api-1.5.11.jar
      slf4j-log4j12-1.5.11.jar
      TCLIServiceClient.jar
      zookeeper-3.4.6.jar
      ```

   1. In the **Please select one driver** dialog box, select `com.amazon.hive.jdbc41.HS2Driver`, **OK**\.

1. When you return to the **Manage Drivers** dialog box, verify that the **Classname** field is populated and select **OK**\. 

1. When you return to the **Select Connection Profile** dialog box, verify that the **Driver** field is set to **Hive JDBC** and provide the following JDBC connection string in the **URL** field: `jdbc:hive2://localhost:10000/default`\.

1. Select **OK** to connect\. After the connection is complete, connection details appear at the top of the SQL Workbench/J window\.

For more information about using Hive and the JDBC interface, see [HiveClient](https://cwiki.apache.org/confluence/display/Hive/HiveClient) and [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface) in Apache Hive documentation\.