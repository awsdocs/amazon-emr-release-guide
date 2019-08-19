# JupyterHub Configuration and Administration<a name="emr-jupyterhub-administer"></a>

JupyterHub and related components run inside a Docker container named `jupyterhub` that runs the Ubuntu operating system\. There are several ways for you to administer components running inside the container\.

**Warning**  
Customizations that you perform within the container may not persist if the container restarts\. We recommend that you script or otherwise automate container configuration so that you can reproduce customizations more readily\.

## Administration Using the Command Line<a name="emr-jupyterhub-administer-cli"></a>

When connected to the master node using SSH, you can issue commands by using the Docker command\-line interface \(CLI\) and specifying the container by name \(`jupyterhub`\) or ID\. For example, `sudo docker exec jupyterhub command` runs commands recognized by the operating system or an application running inside the container\. You can use this method to add users to the operating system and to install additional applications and libraries within the Docker container\. For example, the default container image includes Conda for package installation, so you might run the following command on the master node command line to install an application, Keras, within the container:

```
sudo docker exec jupyterhub conda install keras
```

## Administration by Submitting Steps<a name="emr-jupyterhub-administer-steps"></a>

Steps are a way to submit work to a cluster\. You can submit steps when you launch a cluster, or you can submit steps to a running cluster\. Commands that you run on the command line can be submitted as steps using `command-runner.jar`\. For more information, see [Work with Steps Using the CLI and Console](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-work-with-steps.html) in the *Amazon EMR Management Guide* and [Command Runner](emr-commandrunner.md)\.

For example, you could use the following AWS CLI command on a local computer to install Keras in the same way that you did from the command line of the master node in the earlier example:

```
aws emr add-steps --cluster-id MyClusterID --steps Name="Command Runner",Jar="command-runner.jar",Args="/usr/bin/sudo","/usr/bin/docker","exec","jupyterhub","conda","install","keras"
```

Also, you can script a sequence of steps, upload the script to Amazon S3, and then use `script-runner.jar` to run the script when you create the cluster or add the script as a step\. For more information, see [Run a Script in a Cluster](emr-hadoop-script.md)\. For an example, see [Example: Bash Script to Add Multiple Users](emr-jupyterhub-pam-users.md#emr-jupyterhub-script-multuser)\.

## Administration Using REST APIs<a name="emr-jupyterhub-administer-rest"></a>

Jupyter, JupyterHub, and the HTTP proxy for JupyterHub provide REST APIs that you can use to send requests\. To send requests to JupyterHub, you must pass an API token with the request\. You can use the `curl` command from the master node command line to execute REST commands\. For more information, see the following resources:
+ [Using JupyterHub's REST API](http://jupyterhub.readthedocs.io/en/latest/reference/rest.html) in the documentation for JupyterHub, which includes instructions for generating API tokens
+ [Jupyter Notebook Server API](https://github.com/jupyter/jupyter/wiki/Jupyter-Notebook-Server-API) on GitHub
+ [configurable\-http\-proxy](https://github.com/jupyterhub/configurable-http-proxy) on GitHub

The following example demonstrates using the REST API for JupyterHub to get a list of users\. The command passes a previously generated admin token and uses the default port, 9443, for JupyterHub, piping the output to [jq](https://stedolan.github.io/jq/) for easier viewing:

```
curl -XGET -s -k https://$HOST:9443/hub/api/users \
-H "Authorization: token $admin_token" | jq .
```