# Configuring Persistence for Notebooks in Amazon S3<a name="emr-jupyterhub-s3"></a>

You can configure a JupyterHub cluster in Amazon EMR so that notebooks saved by a user persist in Amazon S3, outside of ephemeral storage on cluster EC2 instances\.

You specify S3 persistence using the `jupyter-s3-conf` configuration classification when you create a cluster\. For more information, see [Configuring Applications](emr-configure-apps.md)\.

In addition to enabling S3 persistence using the `s3.persistence.enabled` property, you specify a bucket in Amazon S3 where notebooks are saved using the `s3.persistence.bucket` property\. Notebooks for each user are saved to a `jupyter/jupyterhub-user-name` folder in the specified bucket\. The bucket must already exist in Amazon S3, and the role for the EC2 instance profile that you specify when you create the cluster must have permissions to the bucket \(by default, the role is `EMR_EC2_DefaultRole`\)\. For more information, see [Configure IAM Roles for Amazon EMR Permissions to AWS Services](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-iam-roles.html)\.

When you launch a new cluster using the same configuration classification properties, users can open notebooks with the content from the saved location\.

The following example enables S3 persistence\. Notebooks saved by users are saved in the `s3://MyJupyterBackups/jupyter/jupyterhub-user-name` folder for each user, where `jupyterhub-user-name` is a user name, such as `diego`\.

```
[
    {
        "Classification": "jupyter-s3-conf",
        "Properties": {
            "s3.persistence.enabled": "true",
            "s3.persistence.bucket": "MyJupyterBackups"
        }
    }
]
```