# Using LDAP Authentication<a name="emr-jupyterhub-ldap-users"></a>

Lightweight Directory Access Protocol \(LDAP\) is an application protocol for querying and modifying objects that correspond to resources such as users and computers stored in an LDAP\-compatible directory service provider such as Active Directory or an OpenLDAP server\. You can use the [LDAP Authenticator Plugin for JupyterHub](https://github.com/jupyterhub/ldapauthenticator/) with JupyterHub on Amazon EMR to use LDAP for user authentication\. The plugin handles login sessions for LDAP users and provides user information to Jupyter\. This lets users connect to JupyterHub and notebooks by using the credentials for their identities stored in an LDAP\-compatible server\.

The steps in this section walk you through the following steps to set up and enable LDAP using the LDAP Authenticator Plugin for JupyterHub\. You perform the steps while connected to the master node command line\. For more information, see [Connecting to the Master Node and Notebook Servers](emr-jupyterhub-connect.md)\.

1. Create an LDAP configuration file with information about the LDAP server, such as the host IP address, port, binding names, and so on\.

1. Modify `/etc/jupyter/conf/jupyterhub_config.py` to enable the LDAP Authenticator Plugin for JupyterHub\.

1. Create and run a script that configures LDAP within the `jupyterhub` container\.

1. Query LDAP for users, and then create home directories within the container for each user\. JupyterHub requires home directories to host notebooks\.

1. Run a script that restarts JupyterHub

**Important**  
Before you set up LDAP, test your network infrastructure to ensure that the LDAP server and the cluster master node can communicate as required\. TLS typically uses port 389 over a plain TCP connection\. If your LDAP connection uses SSL, the well\-known TCP port for SSL is 636\.

## Create the LDAP Configuration File<a name="emr-jupyterhub-ldap-config"></a>

The example below uses the following place\-holder configuration values\. Replace these with parameters that match your implementation\.
+ The LDAP server is running version 3 and available on port 389\. This is the standard non\-SSL port for LDAP\.
+ The base distinguished name \(DN\) is `dc=example, dc=org`\.

Use a text editor to create the file [ldap\.conf](http://manpages.ubuntu.com/manpages/bionic/man5/ldap.conf.5.html), with contents similar to the following\. Use values appropriate for your LDAP implementation\. Replace *host* with the IP address or resolvable host name of your LDAP server\.

```
base dc=example,dc=org
uri ldap://host
ldap_version 3
binddn cn=admin,dc=example,dc=org
bindpw admin
```

## Enable LDAP Authenticator Plugin for JupyterHub<a name="emr-jupyterhub-ldap-plugin"></a>

Use a text editor to modify the `/etc/jupyter/conf/jupyterhub_config.py` file and add [ldapauthenticator](https://github.com/jupyterhub/ldapauthenticator) properties similar to the following\. Replace *host* with the IP address or resolvable host name of the LDAP server\. The example assumes that the user objects are within an organizational unit \(ou\) named *people*, and uses the distinguished name components that you established earlier using `ldap.conf`\.

```
c.JupyterHub.authenticator_class = 'ldapauthenticator.LDAPAuthenticator'
c.LDAPAuthenticator.use_ssl = False
c.LDAPAuthenticator.server_address = 'host' 
c.LDAPAuthenticator.bind_dn_template = 'cn={username},ou=people,dc=example,dc=org'
```

## Configure LDAP Within The Container<a name="emr-jupyterhub-ldap-container"></a>

Use a text editor to create a bash script with the following contents:

```
#!/bin/bash


# Uncomment the following lines to install LDAP client libraries only if
# using Amazon EMR release version 5.14.0. Later versions install libraries by default.
# sudo docker exec jupyterhub bash -c "sudo apt-get update"
# sudo docker exec jupyterhub bash -c "sudo apt-get -y install libnss-ldap libpam-ldap ldap-utils nscd"
 
# Copy ldap.conf
sudo docker cp ldap.conf jupyterhub:/etc/
sudo docker exec jupyterhub bash -c "cat /etc/ldap.conf"
 
# configure nss switch
sudo docker exec jupyterhub bash -c "sed -i 's/\(^passwd.*\)/\1 ldap/g' /etc/nsswitch.conf"
sudo docker exec jupyterhub bash -c "sed -i 's/\(^group.*\)/\1 ldap/g' /etc/nsswitch.conf"
sudo docker exec jupyterhub bash -c "sed -i 's/\(^shadow.*\)/\1 ldap/g' /etc/nsswitch.conf"
sudo docker exec jupyterhub bash -c "cat /etc/nsswitch.conf"
 
# configure PAM to create home directories
sudo docker exec jupyterhub bash -c "echo 'session required        pam_mkhomedir.so skel=/etc/skel umask=077' >> /etc/pam.d/common-session"
sudo docker exec jupyterhub bash -c "cat /etc/pam.d/common-session"
 
# restart nscd service
sudo docker exec jupyterhub bash -c "sudo service nscd restart"
 
# Test
sudo docker exec jupyterhub bash -c "getent passwd"

# Install ldap plugin
sudo docker exec jupyterhub bash -c "pip install jupyterhub-ldapauthenticator"
```

Save the script to the master node, and then run it from the master node command line\. For example, with the script saved as `configure_ldap_client.sh`, make the file executable:

```
chmod +x configure_ldap_client.sh
```

And run the script:

```
./configure_ldap_client.sh
```

## Add Attributes to Active Directory<a name="emr-jupyterhub-ldap-adproperties"></a>

To find each user and create the appropriate entry in the database, the JupyterHub docker container requires the following UNIX properties for the corresponding user object in Active Directory\. For more information, see the section *How do I continue to edit the GID/UID RFC 2307 attributes now that the Unix Attributes Plug\-in is no longer available for the Active Directory Users and Computers MMC snap\-in?* in the article [Clarification regarding the status of Identity Management for Unix \(IDMU\) and NIS Server Role in Windows Server 2016 Technical Preview and beyond](https://blogs.technet.microsoft.com/activedirectoryua/2016/02/09/identity-management-for-unix-idmu-is-deprecated-in-windows-server/)\.
+ `homeDirectory`

  This is the location to the user's home directory, which is usually `/home/username`\.
+ `gidNumber`

  This is a value greater than 60000 that is not already used by a another user\. Check the `etc/passwd` file for gids in use\.
+ `uidNumber`

  This is a value greater than 60000 that is not already used by a another group\. Check the `etc/group` file for uids in use\.
+ `uid`

  This is the same as the *username*\.

## Create User Home Directories<a name="emr-jupyterhub-ldap-directories"></a>

JupyterHub needs home directories within the container to authenticate LDAP users and store instance data\. The following example demonstrates two users, *shirley* and *diego*, in the LDAP directory\.

The first step is to query the LDAP server for each user's user id and group id information using [ldapsearch](http://manpages.ubuntu.com/manpages/xenial/man1/ldapsearch.1.html) as shown in the following example, replacing *host* with the IP address or resolvable host name of your LDAP server:

```
ldapsearch -x -H ldap://host \
 -D "cn=admin,dc=example,dc=org" \
 -w admin \
 -b "ou=people,dc=example,dc=org" \
 -s sub \
 "(objectclass=*)" uidNumber gidNumber
```

The `ldapsearch` command returns an LDIF\-formatted response that looks similar to the following for users *shirley* and *diego*\.

```
# extended LDIF
#
# LDAPv3
# base <ou=people,dc=example,dc=org> with scope subtree
# filter: (objectclass=*)
# requesting: uidNumber gidNumber sn 
#

# people, example.org
dn: ou=people,dc=example,dc=org

# diego, people, example.org
dn: cn=diego,ou=people,dc=example,dc=org
sn: B
uidNumber: 1001
gidNumber: 100

# shirley, people, example.org
dn: cn=shirley,ou=people,dc=example,dc=org
sn: A
uidNumber: 1002
gidNumber: 100

# search result
search: 2
result: 0 Success

# numResponses: 4
# numEntries: 3
```

Using information from the response, run commands within the container to create a home directory for each user common name \(`cn`\)\. Use the `uidNumber` and `gidNumber` to fix ownership for the home directory for that user\. The following example commands do this for the user *shirley*\.

```
sudo docker container exec jupyterhub bash -c "mkdir /home/shirley"
sudo docker container exec jupyterhub bash -c "chown -R $uidNumber /home/shirley"
sudo docker container exec jupyterhub bash -c "sudo chgrp -R $gidNumber /home/shirley"
```

## Restart the Jupyterhub Container<a name="emr-jupyterhub-ldap-restart"></a>

Run the following commands to restart the `jupyterhub` container:

```
sudo docker stop jupyterhub
sudo docker start jupyterhub
```