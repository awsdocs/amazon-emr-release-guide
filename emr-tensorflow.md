# TensorFlow<a name="emr-tensorflow"></a>

TensorFlow is an open\-source symbolic math library for machine intelligence and deep learning applications\. For more information, see the [TensorFlow website](https://www.tensorflow.org/)\. TensorFlow is available with Amazon EMR release version 5\.17\.0 and later\.

The following table lists the version of TensorFlow included in the latest release of Amazon EMR, along with the components that Amazon EMR installs with TensorFlow\.

For the version of components installed with TensorFlow in this release, see [Release 5\.23\.0 Component Versions](emr-release-5x.md#emr-5230-release)\.


**TensorFlow Version Information for emr\-5\.23\.0**  

| Amazon EMR Release Label | TensorFlow Version | Components Installed With TensorFlow | 
| --- | --- | --- | 
| emr\-5\.23\.0 | TensorFlow 1\.12\.0 | emrfs, emr\-goodies, hadoop\-client, hadoop\-hdfs\-datanode, hadoop\-hdfs\-library, hadoop\-hdfs\-namenode, hadoop\-httpfs\-server, hadoop\-kms\-server, hadoop\-yarn\-nodemanager, hadoop\-yarn\-resourcemanager, hadoop\-yarn\-timeline\-server, tensorflow | 

## TensorFlow Builds by Amazon EC2 Instance Type<a name="w3aac53c11"></a>

Amazon EMR uses different builds of the TensorFlow library depending on the instance types that you choose for your cluster\. The following table lists builds by instance type\.


| EC2 Instance Types | TensorFlow Build | 
| --- | --- | 
|  M5 and C5  |  Tensorflow 1\.9\.0 with Intel MKL optimization  | 
|  P2  |  Tensorflow 1\.9\.0 with CUDA 9\.2, cuDNN 7\.1  | 
|  P3  |  Tensorflow 1\.9\.0 with CUDA 9\.2, cuDNN 7\.1, NCCL 2\.2\.13 [Nvidia NCCL](https://developer.nvidia.com/nccl) is available only on P3 instances\. **End User License Agreement \(EULA\)**: By using Nvidia components on Amazon EMR, you agree to the terms and conditions outlined in the [product EULA](https://d7umqicpi7263.cloudfront.net/eula/product/d0199cf7-a04a-4204-be4d-dc3e2af678af/5b36dd71-7d6e-4d97-a8f7-013d3eccec70.txt)\.  | 
|  All others  |  Tensorflow 1\.9\.0  | 

## Security<a name="w3aac53c13"></a>

In addition to following the guidance in [Using TensorFlow Securely](https://github.com/tensorflow/tensorflow/blob/master/SECURITY.md) we recommend that you launch your cluster in a private subnet to help you limit access to trusted sources\. For more information, see [Amazon VPC Options](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-clusters-in-a-vpc.html#emr-vpc-private-subnet) in the *Amazon EMR Management Guide*\.

## Using TensorBoard<a name="emr-tensorflow-tensorboard"></a>

TensorBoard is a suite of visualization tools for TensorFlow programs\. For more information, see [TensorBoard: Visualized Learning](https://www.tensorflow.org/get_started/summaries_and_tensorboard) on the Tensorflow website\.

To use TensorBoard with Amazon EMR, you must start TensorBoard on the cluster master node\.

## To use Tensorboard with Tensorflow on Amazon EMR

1. Connect to the master node of the cluster using SSH\. For more information, see [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

1. Type the following command to start Tensorboard on the master node\. Replace `/my/log/directory` with a directory on the master node where you have generated and stored summary data using a summary writer\.

   ```
   python3 -m tensorboard.main --logdir=/my/log/dir
   ```

   By default, the master node hosts TensorBoard using port 6006 and the master public DNS name\. After you start TensorBoard, the command line output presents the URL that can be used to connect to TensorBoard, as shown in the following example:

   ```
   TensorBoard 1.9.0 at http://master-public-dns-name:6006 (Press CTRL+C to quit)
   ```

1. Set up access to web interfaces on the master node from trusted clients\. For more information, see [View Web Interfaces Hosted on Amazon EMR Clusters](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-web-interfaces.html) in the *Amazon EMR Management Guide*\.

1. Open TensorBoard at `http://master-public-dns-name:6006`\.