# Adding Jupyter Notebook Users and Administrators<a name="emr-jupyterhub-user-access"></a>

JupyterHub on Amazon EMR has a default user with administrator permissions\. The user name is `jovyan` and the password is `jupyter`\. We strongly recommend that you replace the user with another user who has administrative permissions\. Either use a step when you create the cluster, or connect to the master node after you create the cluster\.

You can use one of two methods for users to authenticate to JupyterHub so that they can create notebooks and, optionally, administer JupyterHub\. The easiest method is to use JupyterHub's pluggable authentication module \(PAM\)\. In addition, JupyterHub on Amazon EMR supports the [LDAP Authenticator Plugin for JupyterHub](https://github.com/jupyterhub/ldapauthenticator/) for obtaining user identities from an LDAP server, such as a Microsoft Active Directory server\. Instructions and examples for adding users with each authentication method are provided in this section\.

**Topics**
+ [Using PAM Authentication](emr-jupyterhub-pam-users.md)
+ [Using LDAP Authentication](emr-jupyterhub-ldap-users.md)