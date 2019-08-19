# Configuring JupyterHub<a name="emr-jupyterhub-configure"></a>

You can customize the configuration of JupyterHub on Amazon EMR and individual user notebooks by connecting to the cluster master node and editing configuration files\. After you change values, restart the `jupyterhub` container\.

Modify properties in the following files to configure JupyterHub and individual Jupyter notebooks:
+ `jupyterhub_config.py`—By default, this file is saved in the `/etc/jupyter/conf/` directory on the master node\. For more information, see [Configuration Basics](http://jupyterhub.readthedocs.io/en/latest/getting-started/config-basics.html) in the JupyterHub documentation\.
+ `jupyter_notebook_config.py`—This file is saved in the `/etc/jupyter/` directory by default and copied to the `jupyterhub` container as the default\. For more information, see [Config file and command line options](http://jupyter-notebook.readthedocs.io/en/stable/config.html) in the Jupyter Notebook documentation\.

You can also use the `jupyter-sparkmagic-conf` configuration classification to customize Sparkmagic, which updates values in the `config.json` file for Sparkmagic\. For more information about available settings, see the [example\_config\.json on GitHub](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json)\. For more information about using configuration classifications with applications in Amazon EMR, see [Configuring Applications](emr-configure-apps.md)\.

The following example launches a cluster using the AWS CLI, referencing the file `MyJupyterConfig.json` for Sparkmagic configuration classification settings\.

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

```
aws emr create-cluster --use-default-roles --release-label emr-5.14.0 \
--applications Name=Jupyter --instance-type m4.xlarge --instance-count 3 \
--ec2-attributes KeyName=MyKey,SubnetId=subnet-1234a5b6 --configurations file://MyJupyterConfig.json
```

Sample contents of `MyJupyterConfig.json` are as follows:

```
[
    {
    "Classification":"jupyter-sparkmagic-conf",
    "Properties": {
      "kernel_python_credentials" : "{\"username\":\"diego\",\"base64_password\":\"mypass\",\"url\":\"http:\/\/localhost:8998\",\"auth\":\"None\"}"
      }
    }
]
```

**Note**  
With Amazon EMR version 5\.21\.0 and later, you can override cluster configurations and specify additional configuration classifications for each instance group in a running cluster\. You do this by using the Amazon EMR console, the AWS Command Line Interface \(AWS CLI\), or the AWS SDK\. For more information, see [Supplying a Configuration for an Instance Group in a Running Cluster](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps-running-cluster.html)\.