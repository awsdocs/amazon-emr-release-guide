# Configure Hue for LDAP Users<a name="hue-ldap"></a>

Integration with LDAP allows users to log into Hue using existing credentials stored in an LDAP directory\. When you integrate Hue with LDAP, you do not need to independently manage user information in Hue\. The information below demonstrates Hue integration with Microsoft Active Directory, but the configuration options are analogous to any LDAP directory\.

LDAP authentication first binds to the server and establishes the connection\. Then, the established connection is used for any subsequent queries to search for LDAP user information\. Unless your Active Directory server allows anonymous connections, a connection needs to be established using a bind distinguished name and password\. The bind distinguished name \(or DN\) is defined by the `bind_dn` configuration setting\. The bind password is defined by the `bind_password` configuration setting\. Hue has two ways to bind LDAP requests: search bind and direct bind\. The preferred method for using Hue with Amazon EMR is search bind\.

When search bind is used with Active Directory, Hue uses the user name attribute \(defined by `user_name_attr config`\) to find the attribute that needs to be retrieved from the base distinguished name \(or DN\)\. Search bind is useful when the full DN is not known for the Hue user\. 

For example, you may have `user_name_attr config` set to use the common name \(or CN\)\. In that case, the Active Directory server uses the Hue username provided during login to search the directory tree for a common name that matches, starting at the base distinguished name\. If the common name for the Hue user is found, the user's distinguished name is returned by the server\. Hue then constructs a distinguished name used to authenticate the user by performing a bind operation\.

**Note**  
Search bind searches usernames in all directory subtrees beginning at the base distinguished name\. The base distinguished name specified in the Hue LDAP configuration should be the closest parent of the username, or your LDAP authentication performance may suffer\. 

When direct bind is used with Active Directory, the exact `nt_domain` or `ldap_username_pattern` must be used to authenticate\. When direct bind is used, if the nt domain \(defined by the `nt_domain` configuration setting\) attribute is defined, a user distinguished name template is created using the form: `<login username>@nt_domain`\. This template is used to search all directory subtrees beginning at the base distinguished name\. If the nt domain is not configured, Hue searches for an exact distinguished name pattern for the user \(defined by the `ldap_username_pattern` configuration setting\)\. In this instance, the server searches for a matching `ldap_username_pattern` value in all directory subtrees beginning at the base distinguished name\.

**To Launch a cluster with LDAP properties for Hue using the AWS CLI**
+ To specify LDAP properties for `hue-ini`, create a cluster with Hue installed and reference a json file with configuration properties for LDAP\. An example command is shown below, which references a configuration file `myConfig.json` stored in Amazon S3\.

  ```
  aws emr create-cluster --release-label emr-5.23.0 --applications Name=Hue Name=Spark Name=Hive \
  --instance-type m4.large --instance-count 3 --configurations https://s3.amazonaws.com/mybucket/myfolder/myConfig.json.
  ```

  Example contents of `myConfig.json` are shown below\.

  ```
  [
    {
      "Classification": "hue-ini",
      "Properties": {},
      "Configurations": [
        {
          "Classification": "desktop",
          "Properties": {},
          "Configurations": [
            {
              "Classification": "ldap",
              "Properties": {},
              "Configurations": [
                {
                  "Classification": "ldap_servers",
                  "Properties": {},
                  "Configurations": [
                    {
                      "Classification": "yourcompany",
                      "Properties": {
                        "base_dn": "DC=yourcompany,DC=hue,DC=com",
                        "ldap_url": "ldap://ldapurl",
                        "search_bind_authentication": "true",
                        "bind_dn": "CN=hue,CN=users,DC=yourcompany,DC=hue,DC=com",
                        "bind_password": "password"
                      },
                      "Configurations": []
                    }
                  ]
                }
              ]
            }
          ]
        }
      ]
    }
  ]
  ```

**Note**  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.

**To View LDAP Settings in Hue**

1. Verify you have an active VPN connection or SSH tunnel to the Amazon EMR cluster's master node\. Then, in your browser, type *master\-public\-dns*:8888 to open the Hue web interface\. 

1. Log in using your Hue administrator credentials\. If the **Did you know?** window opens, click **Got it, prof\!** to close it\. 

1. Click the **Hue** icon in the toolbar\.

1. On the **About Hue** page, click **Configuration**\.

1. In the **Configuration Sections and Variables** section, click **Desktop**\.

1. Scroll to the **ldap** section to view your settings\.