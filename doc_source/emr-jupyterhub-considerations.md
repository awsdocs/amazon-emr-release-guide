# Considerations When Using JupyterHub on Amazon EMR<a name="emr-jupyterhub-considerations"></a>

Consider the following when using JupyterHub on Amazon EMR\.
+ 
**Warning**  
User notebooks and files are saved to the file system on the master node\. This is ephemeral storage that does not persist through cluster termination\. When a cluster terminates, this data is lost if not backed up\. We recommend that you schedule regular backups using `cron` jobs or another means suitable for your application\.  
In addition, configuration changes made within the container may not persist if the container restarts\. We recommend that you script or otherwise automate container configuration so that you can reproduce customizations more readily\.
+ Kerberos authentication that has been set up using an Amazon EMR security configuration is not supported\.
+ [OAuthenticator](https://github.com/jupyterhub/oauthenticator) is not supported\.