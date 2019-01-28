# User Impersonation<a name="emr-jupyterhub-user-impersonation"></a>

A Spark job running inside a Jupyter notebook traverses multiple applications during its execution on Amazon EMR\. For example, PySpark3 code that a user runs inside Jupyter is received by Sparkmagic, which uses an HTTP POST request to submit it to Livy, which then creates a Spark job to execute on the cluster using YARN\.

By default, YARN jobs submitted this way run as user `livy`, regardless of the user who initiated the job\. By setting up *user impersonation* you can have the user ID of the notebook user also be the user associated with the YARN job\. Rather than having jobs initiated by both `shirley` and `diego` associated with the user `livy`, jobs that each user initiates are associated with `shirley` and `diego` respectively\. This helps you to audit Jupyter usage and manage applications within your organization\.

This configuration is only supported when calls from Sparkmagic to Livy are unauthenticated\. Applications that provide an authentication or proxying layer between Hadoop applications and Livy \(such as Apache Knox Gateway\) are not supported\. The steps to configure user impersonation in this section assume that JupyterHub and Livy are running on the same master node\. If your application has separate clusters, [Step 3: Create HDFS home directories for users](#Step3-UserImpersonation) needs to be modified so that HDFS directories are created on the Livy master node\.

**Topics**
+ [Step 1: Configure Livy](#Step1-UserImpersonation)
+ [Step 2: Add users](#Step2-UserImpersonation)
+ [Step 3: Create HDFS home directories for users](#Step3-UserImpersonation)

## Step 1: Configure Livy<a name="Step1-UserImpersonation"></a>

You use the `livy-conf` and `core-site` configuration classifications when you create a cluster to enable Livy user impersonation as shown in the following example\. Save the configuration classification as a JSON and then reference it when you create the cluster, or specify the configuration classification inline\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

```
[
  {
    "Classification": "livy-conf",
    "Properties": {
      "livy.impersonation.enabled": "true"
    }
  },
  {
    "Classification": "core-site",
    "Properties": {
      "hadoop.proxyuser.livy.groups": "*",
      "hadoop.proxyuser.livy.hosts": "*"
    }
  }
]
```

## Step 2: Add users<a name="Step2-UserImpersonation"></a>

Add JupyterHub users using PAM or LDAP\. For more information, see [Using PAM Authentication](emr-jupyterhub-pam-users.md) and [Using LDAP Authentication](emr-jupyterhub-ldap-users.md)\.

## Step 3: Create HDFS home directories for users<a name="Step3-UserImpersonation"></a>

You connected to the master node to create users\. While still connected to the master node, copy the contents below and save it to a script file\. The script creates HDFS home directories for each JupyterHub user on the master node\. The script assumes you are using the default administrator user ID, *jovyan*\.

```
#!/bin/bash

CURL="curl --silent -k"
HOST=$(curl -s http://169.254.169.254/latest/meta-data/local-hostname)

admin_token() {
    local user=jovyan
    local pwd=jupyter
    local token=$($CURL https://$HOST:9443/hub/api/authorizations/token \
        -d "{\"username\":\"$user\", \"password\":\"$pwd\"}" | jq ".token")
    if [[ $token != null ]]; then
        token=$(echo $token | sed 's/"//g')
    else
        echo "Unable to get Jupyter API Token."
        exit 1
    fi
    echo $token
}

# Get Jupyter Admin token
token=$(admin_token)

# Get list of Jupyter users
users=$(curl -XGET -s -k https://$HOST:9443/hub/api/users \
 -H "Authorization: token $token" | jq '.[].name' | sed 's/"//g')

# Create HDFS home dir 
for user in ${users[@]}; 
do
 echo "Create hdfs home dir for $user"
 hadoop fs -mkdir /user/$user
 hadoop fs -chmod 777 /user/$user
done
```