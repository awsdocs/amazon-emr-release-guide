# Build Binaries Using Amazon EMR<a name="emr-build-binaries"></a>

You can use Amazon EMR as a build environment to compile programs for use in your cluster\. Programs that you use with Amazon EMR must be compiled on a system running the same version of Linux used by Amazon EMR\. For a 32\-bit version, you should have compiled on a 32\-bit machine or with 32\-bit cross compilation options turned on\. For a 64\-bit version, you need to have compiled on a 64\-bit machine or with 64\-bit cross compilation options turned\. For more information about EC2 instance versions, see [Plan and Configure EC2 Instances](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-ec2-instances.html) in the *Amazon EMR Management Guide*\. Supported programming languages include C\+\+, Cython, and C\#\. 

The following table outlines the steps involved to build and test your application using Amazon EMR\.


**Process for Building a Module**  

|  |  | 
| --- |--- |
|  1 |  Connect to the master node of your cluster\. | 
|  2  |  Copy source files to the master node\. | 
|  3  |  Build binaries with any necessary optimizations\. | 
|  4 |  Copy binaries from the master node to Amazon S3\. | 

The details for each of these steps are covered in the sections that follow\. 

**To connect to the master node of the cluster**
+ Follow the instructions at [Connect to the Master Node Using SSH](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-connect-master-node-ssh.html) in the *Amazon EMR Management Guide*\.

**To copy source files to the master node**

1. Put your source files in an Amazon S3 bucket\. To learn how to create buckets and how to move data into Amazon S3, see the [Amazon Simple Storage Service Getting Started Guide](https://docs.aws.amazon.com/AmazonS3/latest/gsg/)\.

1. Create a folder on your Hadoop cluster for your source files by entering a command similar to the following:

   ```
   mkdir SourceFiles
   ```

1. Copy your source files from Amazon S3 to the master node by typing a command similar to the following:

   ```
   hadoop fs -get s3://mybucket/SourceFiles SourceFiles
   ```

**Build binaries with any necessary optimizations**  
How you build your binaries depends on many factors\. Follow the instructions for your specific build tools to setup and configure your environment\. You can use Hadoop system specification commands to obtain cluster information to determine how to install your build environment\.

**To identify system specifications**
+ Use the following commands to verify the architecture you are using to build your binaries\.

  1. To view the version of Debian, enter the following command:

     ```
     master$ cat /etc/issue
     ```

     The output looks similar to the following\.

     ```
     Debian GNU/Linux 5.0
     ```

  1. To view the public DNS name and processor size, enter the following command:

     ```
     master$ uname -a
     ```

     The output looks similar to the following\.

     ```
     Linux domU-12-31-39-17-29-39.compute-1.internal 2.6.21.7-2.fc8xen #1 SMP Fri Feb 15 12:34:28 EST 2008 x86_64 GNU/Linux
     ```

  1. To view the processor speed, enter the following command:

     ```
     master$ cat /proc/cpuinfo
     ```

     The output looks similar to the following\.

     ```
     processor : 0
     vendor_id : GenuineIntel
     model name : Intel(R) Xeon(R) CPU E5430 @ 2.66GHz
     flags : fpu tsc msr pae mce cx8 apic mca cmov pat pse36 clflush dts acpi mmx fxsr sse sse2 ss ht tm syscall nx lm constant_tsc pni monitor ds_cpl vmx est tm2 ssse3 cx16 xtpr cda lahf_lm
     ...
     ```

Once your binaries are built, you can copy the files to Amazon S3\.

**To copy binaries from the master node to Amazon S3**
+ Type the following command to copy the binaries to your Amazon S3 bucket:

  ```
  hadoop fs -put BinaryFiles s3://mybucket/BinaryDestination
  ```