# Run Spark applications with Docker using Amazon EMR 6\.x<a name="emr-spark-docker"></a>

With Amazon EMR 6\.0\.0, Spark applications can use Docker containers to define their library dependencies, instead of installing dependencies on the individual Amazon EC2 instances in the cluster\. To run Spark with Docker, you must first configure the Docker registry and define additional parameters when submitting a Spark application\. For more information, see [Configure Docker integration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html)\.

When the application is submitted, YARN invokes Docker to pull the specified Docker image and run the Spark application inside a Docker container\. This allows you to easily define and isolate dependencies\. It reduces the time for bootstrapping or preparing instances in the Amazon EMR cluster with the libraries needed for job execution\. 

## Considerations when running Spark with Docker<a name="emr-spark-docker-considerations"></a>

When running Spark with Docker, make sure the following prerequisites are met:
+ The `docker` package and CLI are only installed on core and task nodes\.
+ On Amazon EMR 6\.1\.0 and later, you can alternatively install Docker on a master node by using following commands\.
  + 

    ```
    sudo yum install -y docker
    sudo systemctl start docker
    ```
+ The `spark-submit` command should always be run from a master instance on the Amazon EMR cluster\.
+ The Docker registries used to resolve Docker images must be defined using the Classification API with the `container-executor` classification key to define additional parameters when launching the cluster:
  + `docker.trusted.registries`
  + `docker.privileged-containers.registries`
+ To execute a Spark application in a Docker container, the following configuration options are necessary:
  + `YARN_CONTAINER_RUNTIME_TYPE=docker`
  + `YARN_CONTAINER_RUNTIME_DOCKER_IMAGE={DOCKER_IMAGE_NAME}`
+ When using Amazon ECR to retrieve Docker images, you must configure the cluster to authenticate itself\. To do so, you must use the following configuration option:
  + YARN\_CONTAINER\_RUNTIME\_DOCKER\_CLIENT\_CONFIG=\{DOCKER\_CLIENT\_CONFIG\_PATH\_ON\_HDFS\}
+ In EMR 6\.1\.0 and later, you are not required to use the listed command `YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG={DOCKER_CLIENT_CONFIG_PATH_ON_HDFS}` when the ECR auto authentication feature is enabled\.
+ Any Docker image used with Spark must have Java installed in the Docker image\.

For more information about the prerequisites, see [Configure Docker integration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html)\.

## Creating a Docker image<a name="emr-spark-docker-image"></a>

Docker images are created using a Dockerfile, which defines the packages and configuration to include in the image\. The following two example Dockerfiles use PySpark and SparkR\.

**PySpark Dockerfile**

Docker images created from this Dockerfile include Python 3 and the NumPy Python package\. This Dockerfile uses Amazon Linux 2 and the Amazon Corretto JDK 8\.

```
FROM amazoncorretto:8

RUN yum -y update
RUN yum -y install yum-utils
RUN yum -y groupinstall development

RUN yum list python3*
RUN yum -y install python3 python3-dev python3-pip python3-virtualenv

RUN python -V
RUN python3 -V

ENV PYSPARK_DRIVER_PYTHON python3
ENV PYSPARK_PYTHON python3

RUN pip3 install --upgrade pip
RUN pip3 install numpy pandas

RUN python3 -c "import numpy as np"
```

**SparkR Dockerfile**

Docker images created from this Dockerfile include R and the randomForest CRAN package\. This Dockerfile includes Amazon Linux 2 and the Amazon Corretto JDK 8\.

```
FROM amazoncorretto:8

RUN java -version

RUN yum -y update
RUN amazon-linux-extras enable R3.4

RUN yum -y install R R-devel openssl-devel
RUN yum -y install curl

#setup R configs
RUN echo "r <- getOption('repos'); r['CRAN'] <- 'http://cran.us.r-project.org'; options(repos = r);" ) ~/.Rprofile

RUN Rscript -e "install.packages('randomForest')"
```

For more information on Dockerfile syntax, see the [Dockerfile reference documentation](https://docs.docker.com/engine/reference/builder/)\.

## Using Docker images from Amazon ECR<a name="emr-spark-docker-ECR"></a>

Amazon Elastic Container Registry \(Amazon ECR\) is a fully\-managed Docker container registry, which makes it easy to store, manage, and deploy Docker container images\. When using Amazon ECR, the cluster must be configured to trust your instance of ECR, and you must configure authentication in order for the cluster to use Docker images from Amazon ECR\. For more information, see [Configuring YARN to access Amazon ECR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html#emr-docker-ECR)\. 

To make sure that EMR hosts can access the images stored in Amazon ECR, your cluster must have the permissions from the `AmazonEC2ContainerRegistryReadOnly` policy associated with the instance profile\. For more information, see [`AmazonEC2ContainerRegistryReadOnly` Policy](https://docs.aws.amazon.com/AmazonECR/latest/userguide/ecr_managed_policies.html#AmazonEC2ContainerRegistryReadOnly)\.

In this example, the cluster must be created with the following additional configuration to ensure that the Amazon ECR registry is trusted\. Replace the *123456789123\.dkr\.ecr\.us\-east\-1\.amazonaws\.com* endpoint with your Amazon ECR endpoint\.

```
[
  {
    "Classification": "container-executor",
    "Configurations": [
        {
            "Classification": "docker",
            "Properties": {
                "docker.trusted.registries": "local,centos,123456789123.dkr.ecr.us-east-1.amazonaws.com",
                "docker.privileged-containers.registries": "local,centos,123456789123.dkr.ecr.us-east-1.amazonaws.com"
            }
        }
    ]
  }
]
```

**Using PySpark with Amazon ECR**

The following example uses the PySpark Dockerfile, which will be tagged and uploaded to Amazon ECR\. After the Dockerfile is uploaded, you can run the PySpark job and refer to the Docker image from Amazon ECR\.

After you launch the cluster, use SSH to connect to a core node and run the following commands to build the local Docker image from the PySpark Dockerfile example\.

First, create a directory and a Dockerfile\.

```
mkdir pyspark
vi pyspark/Dockerfile
```

Paste the contents of the PySpark Dockerfile and run the following commands to build a Docker image\.

```
sudo docker build -t local/pyspark-example pyspark/
```

Create the `emr-docker-examples` ECR repository for the examples\.

```
aws ecr create-repository --repository-name emr-docker-examples
```

Tag and upload the locally built image to ECR, replacing *123456789123\.dkr\.ecr\.us\-east\-1\.amazonaws\.com* with your ECR endpoint\.

```
sudo docker tag local/pyspark-example 123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:pyspark-example
sudo docker push 123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:pyspark-example
```

Use SSH to connect to the master node and prepare a Python script with the filename `main.py`\. Paste the following content into the `main.py` file and save it\.

```
from pyspark.sql import SparkSession
spark = SparkSession.builder.appName("docker-numpy").getOrCreate()
sc = spark.sparkContext

import numpy as np
a = np.arange(15).reshape(3, 5)
print(a)
```

On EMR 6\.0\.0, to submit the job, reference the name of the Docker image\. Define the additional configuration parameters to make sure that the job execution uses Docker as the runtime\. When using Amazon ECR, the `YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG` must reference the `config.json` file containing the credentials used to authenticate to Amazon ECR\.

```
DOCKER_IMAGE_NAME=123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:pyspark-example
DOCKER_CLIENT_CONFIG=hdfs:///user/hadoop/config.json
spark-submit --master yarn \
--deploy-mode cluster \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG=$DOCKER_CLIENT_CONFIG \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG=$DOCKER_CLIENT_CONFIG \
--num-executors 2 \
main.py -v
```

On EMR 6\.1\.0 and later, to submit the job, reference the name of the Docker image\. When ECR auto authentication is enabled, run the following command\.

```
DOCKER_IMAGE_NAME=123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:pyspark-example
spark-submit --master yarn \
--deploy-mode cluster \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--num-executors 2 \
main.py -v
```

When the job completes, take note of the YARN application ID, and use the following command to obtain the output of the PySpark job\.

```
yarn logs --applicationId application_id | grep -C2 '\[\['
LogLength:55
LogContents:
[[ 0  1  2  3  4]
 [ 5  6  7  8  9]
 [10 11 12 13 14]]
```

**Using SparkR with Amazon ECR**

The following example uses the SparkR Dockerfile, which will be tagged and uploaded to ECR\. Once the Dockerfile is uploaded, you can run the SparkR job and refer to the Docker image from Amazon ECR\.

After you launch the cluster, use SSH to connect to a core node and run the following commands to build the local Docker image from the SparkR Dockerfile example\.

First, create a directory and the Dockerfile\.

```
mkdir sparkr
vi sparkr/Dockerfile
```

Paste the contents of the SparkR Dockerfile and run the following commands to build a Docker image\.

```
sudo docker build -t local/sparkr-example sparkr/
```

Tag and upload the locally built image to Amazon ECR, replacing *123456789123\.dkr\.ecr\.us\-east\-1\.amazonaws\.com* with your Amazon ECR endpoint\.

```
sudo docker tag local/sparkr-example 123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:sparkr-example
sudo docker push 123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:sparkr-example
```

Use SSH to connect to the master node and prepare an R script with the name `sparkR.R`\. Paste the following contents into the `sparkR.R` file\.

```
library(SparkR)
sparkR.session(appName = "R with Spark example", sparkConfig = list(spark.some.config.option = "some-value"))

sqlContext <- sparkRSQL.init(spark.sparkContext)
library(randomForest)
# check release notes of randomForest
rfNews()

sparkR.session.stop()
```

On EMR 6\.0\.0, to submit the job, refer to the name of the Docker image\. Define the additional configuration parameters to make sure that the job execution uses Docker as the runtime\. When using Amazon ECR, the `YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG` must refer to the `config.json` file containing the credentials used to authenticate to ECR\.

```
DOCKER_IMAGE_NAME=123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:sparkr-example
DOCKER_CLIENT_CONFIG=hdfs:///user/hadoop/config.json
spark-submit --master yarn \
--deploy-mode cluster \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG=$DOCKER_CLIENT_CONFIG \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_CLIENT_CONFIG=$DOCKER_CLIENT_CONFIG \
sparkR.R
```

On EMR 6\.1\.0 and later, to submit the job, reference the name of the Docker image\. When ECR auto authentication is enabled, run following command\.

```
DOCKER_IMAGE_NAME=123456789123.dkr.ecr.us-east-1.amazonaws.com/emr-docker-examples:sparkr-example
spark-submit --master yarn \
--deploy-mode cluster \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.executorEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_TYPE=docker \
--conf spark.yarn.appMasterEnv.YARN_CONTAINER_RUNTIME_DOCKER_IMAGE=$DOCKER_IMAGE_NAME \
sparkR.R
```

When the job has completed, note the YARN application ID, and use the following command to obtain the output of the SparkR job\. This example includes testing to make sure that the randomForest library, version installed, and release notes are available\.

```
yarn logs --applicationId application_id | grep -B4 -A10 "Type rfNews"
randomForest 4.6-14
Type rfNews() to see new features/changes/bug fixes.
Wishlist (formerly TODO):

* Implement the new scheme of handling classwt in classification.

* Use more compact storage of proximity matrix.

* Allow case weights by using the weights in sampling?

========================================================================
Changes in 4.6-14:
```

## Using a Docker image from Docker Hub<a name="emr-spark-dockerhub"></a>

To use Docker Hub, you must deploy your cluster to a public subnet and configure it to use Docker Hub as a trusted registry\. For more information, see [Configure Docker integration](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-docker.html)\. 

In this example, the cluster needs the following additional configuration to make sure that the your\-public\-repo repository on Docker Hub is trusted\. When using Docker Hub, replace this repository name with your actual repository\.

```
[
  {
    "Classification": "container-executor",
    "Configurations": [
        {
            "Classification": "docker",
            "Properties": {
                "docker.trusted.registries": "local,centos,your-public-repo",
                "docker.privileged-containers.registries": "local,centos,your-public-repo"
            }
        }
    ]
  }
]
```