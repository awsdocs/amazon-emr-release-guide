# Installing Additional Kernels and Libraries<a name="emr-jupyterhub-install-kernels-libs"></a>

When you create a cluster with JupyterHub on Amazon EMR, the default Python 3 kernel for Jupyter, and the PySpark and Spark kernels for Sparkmagic are installed on the Docker container\. You can install additional kernels\. You can also install additional libraries and packages and then import them for the appropriate shell\.

## Installing a Kernel<a name="emr-jupyterhub-install-kernels"></a>

Kernels are installed within the Docker container\. The easiest way to accomplish this is to create a bash script with installation commands, save it to the master node, and then use the `sudo docker exec jupyterhub script_name` command to run the script within the `jupyterhub` container\. The following example script installs the kernel, and then installs a few libraries for that kernel on the master node so that later you can import the libraries using the kernel in Jupyter\.

```
#!/bin/bash
# Install Python 2 kernel
conda create -n py27 python=2.7 anaconda
source  /opt/conda/envs/py27/bin/activate
apt-get update
apt-get install -y gcc
/opt/conda/envs/py27/bin/python -m pip install --upgrade ipykernel
/opt/conda/envs/py27/bin/python -m ipykernel install

# Install libraries for Python2
/opt/conda/envs/py27/bin/pip install paramiko nltk scipy numpy scikit-learn pandas
```

To install the kernel and libraries within the container, open a terminal connection to the master node, save the script to `/etc/jupyter/install_kernels.sh`, and run the following command on the master node command line:

```
sudo docker exec jupyterhub bash /etc/jupyter/install_kernels.sh
```

## Using Libraries and Installing Additional Libraries<a name="emr-jupyterhub-install-libs"></a>

A core set of machine learning and data science libraries for Python 3 are pre\-installed with JupyterHub on Amazon EMR\. You can use `sudo docker exec jupyterhub bash -c "conda list" ` and `sudo docker exec jupyterhub bash -c "pip freeze" `\.

If a Spark job needs libraries on worker nodes, we recommend that you use a bootstrap action to run a script to install the libraries when you create the cluster\. Bootstrap actions run on all cluster nodes during the cluster creation process, which simplifies installation\. If you install libraries on core/worker nodes after a cluster is running, the operation is more complex\. We provide an example Python program in this section that shows how to install these libraries\.

The bootstrap action and Python program examples shown in this section use a bash script saved to Amazon S3 to install the libraries on all nodes\.

The script referenced in the following examples uses `pip` to install paramiko, nltk, scipy, scikit\-learn, and pandas for the Python 3 kernel:

```
#!/bin/bash

sudo python3 -m pip install boto3 paramiko nltk scipy scikit-learn pandas
```

After you create the script, upload it to a location in Amazon S3, for example, `s3://mybucket/install-my-jupyter-libraries.sh`\. For more information, see [How do I Upload Files and Folders to an S3 Bucket](https://docs.aws.amazon.com/AmazonS3/latest/user-guide/upload-objects.html) in the *Amazon Simple Storage Service Console User Guide* so that you can use it in your bootstrap action or in your Python program\.

**To specify a bootstrap action that installs libraries on all nodes when you create a cluster using the AWS CLI**

1. Create a script similar to the earlier example and save it to a location in Amazon S3\. We use the example `s3://mybucket/install-my-jupyter-libraries.sh`\.

1. Create the cluster with JupyterHub and use the `Path` argument of the `--bootstrap-actions` option to specify the script location as shown in the following example:
**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

   ```
   aws emr create-cluster --name="MyJupyterHubCluster" --release-label emr-5.31.0 \
   --applications Name=JupyterHub --log-uri s3://MyBucket/MyJupyterClusterLogs \
   --use-default-roles --instance-type m5.xlarge --instance-count 2 --ec2-attributes KeyName=MyKeyPair \
   --bootstrap-actions Path=s3://mybucket/install-my-jupyter-libraries.sh,Name=InstallJupyterLibs
   ```

**To specify a bootstrap action that installs libraries on all nodes when you create a cluster using the console**

1. Open the Amazon EMR console at [https://console\.aws\.amazon\.com/elasticmapreduce/](https://console.aws.amazon.com/elasticmapreduce/)\.

1. Choose **Create cluster**, **Go to advanced options**\.

1. Specify settings for **Software and Steps** and **Hardware** as appropriate for your application\.

1. On the **General Cluster Settings** screen, expand **Bootstrap Actions**\.

1. For **Add bootstrap action**, select **Custom action**, **Configure and add**\.

1. For **Name**, enter a friendly name\. For **Script location**, enter the location in Amazon S3 of your script \(the example we use is *s3://mybucket/install\-my\-jupyter\-libraries\.sh*\)\. Leave **Optional arguments** blank, and choose **Add**\.

1. Specify other settings for your cluster, and choose **Next**\.

1. Specify security settings, and choose **Create cluster**\.

**Example Installing Libraries on Core Nodes of a Running Cluster**  
After you install libraries on the master node from within Jupyter, you can install libraries on running core nodes in various ways\. The following example shows a Python program written to run on a local machine\. When you run the Python program locally, it uses the `AWS-RunShellScript` of AWS Systems Manager to run the example script, shown earlier in this section, which installs libraries on the cluster's core nodes\.  

```
import argparse
import time
import boto3


def install_libraries_on_core_nodes(
        cluster_id, script_path, emr_client, ssm_client):
    """
    Copies and runs a shell script on the core nodes in the cluster.

    :param cluster_id: The ID of the cluster.
    :param script_path: The path to the script, typically an Amazon S3 object URL.
    :param emr_client: The Boto3 Amazon EMR client.
    :param ssm_client: The Boto3 AWS Systems Manager client.
    """
    core_nodes = emr_client.list_instances(
        ClusterId=cluster_id, InstanceGroupTypes=['CORE'])['Instances']
    core_instance_ids = [node['Ec2InstanceId'] for node in core_nodes]
    print(f"Found core instances: {core_instance_ids}.")

    commands = [
        # Copy the shell script from Amazon S3 to each node instance.
        f"aws s3 cp {script_path} /home/hadoop",
        # Run the shell script to install libraries on each node instance.
        "bash /home/hadoop/install_libraries.sh"]
    for command in commands:
        print(f"Sending '{command}' to core instances...")
        command_id = ssm_client.send_command(
            InstanceIds=core_instance_ids,
            DocumentName='AWS-RunShellScript',
            Parameters={"commands": [command]},
            TimeoutSeconds=3600)['Command']['CommandId']
        while True:
            # Verify the previous step succeeded before running the next step.
            cmd_result = ssm_client.list_commands(
                CommandId=command_id)['Commands'][0]
            if cmd_result['StatusDetails'] == 'Success':
                print(f"Command succeeded.")
                break
            elif cmd_result['StatusDetails'] in ['Pending', 'InProgress']:
                print(f"Command status is {cmd_result['StatusDetails']}, waiting...")
                time.sleep(10)
            else:
                print(f"Command status is {cmd_result['StatusDetails']}, quitting.")
                raise RuntimeError(
                    f"Command {command} failed to run. "
                    f"Details: {cmd_result['StatusDetails']}")


def main():
    parser = argparse.ArgumentParser()
    parser.add_argument('cluster_id', help="The ID of the cluster.")
    parser.add_argument('script_path', help="The path to the script in Amazon S3.")
    args = parser.parse_args()

    emr_client = boto3.client('emr')
    ssm_client = boto3.client('ssm')

    install_libraries_on_core_nodes(
        args.cluster_id, args.script_path, emr_client, ssm_client)


if __name__ == '__main__':
    main()
```
