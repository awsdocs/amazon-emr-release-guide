# Using Hive LLAP<a name="emr-hive-llap"></a>

Amazon EMR 6\.0\.0 supports the Live Long and Process \(LLAP\) functionality for Hive\. LLAP uses persistent daemons with intelligent in\-memory caching to improve query performance compared to the previous default Tez container execution mode\.

The Hive LLAP daemons are managed and run as a YARN Service\. Since a YARN service can be considered a long\-running YARN application, some of your cluster resources are dedicated to Hive LLAP and cannot be used for other workloads\. For more information, see [LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) and [YARN Service API](https://hadoop.apache.org/docs/r3.2.1/hadoop-yarn/hadoop-yarn-site/yarn-service/YarnServiceAPI.html)\.

## How to enable Hive LLAP on Amazon EMR<a name="emr-llap-enable"></a>

To enable Hive LLAP on Amazon EMR, supply the following configuration when you launch a cluster\. 

```
[
  {
    "Classification": "hive",
    "Properties": {
      "hive.llap.enabled": "true"
    }
  }
]
```

For more information, see [Configuring Applications](https://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-configure-apps.html)\.

By default, Amazon EMR allocates about 60 percent of cluster YARN resources to Hive LLAP daemons\. You can configure the percentage of cluster YARN resource allocated to Hive LLAP and the number of task and core nodes to be considered for the Hive LLAP allocation\.

For example, the following configuration starts Hive LLAP with three daemons on three task or core nodes and allocates 40 percent of the three core or task nodes' YARN resource to the Hive LLAP daemons\.

```
[
  {
    "Classification": "hive",
    "Properties": {
      "hive.llap.enabled": "true",
      "hive.llap.percent-allocation": "0.4",
      "hive.llap.num-instances": "3"
    }
  }
]
```

You can use the following `hive-site` configurations in the classification API to override default LLAP resource settings\.


| Property | Description | 
| --- | --- | 
| hive\.llap\.daemon\.yarn\.container\.mb | Total LLAP daemon container size \(in MB\) | 
| hive\.llap\.daemon\.memory\.per\.instance\.mb |  The total memory used by executors in the LLAP daemon container \(in MB\)  | 
| hive\.llap\.io\.memory\.size |  Cache size for LLAP Input/Output  | 
| hive\.llap\.daemon\.num\.executors |  Number of executors per LLAP daemon  | 

## To manually start LLAP on your cluster<a name="emr-llap-manually"></a>

All dependencies and configurations used by LLAP are packaged into the LLAP tar archive as part of cluster startup\. If LLAP is enabled using `"hive.llap.enabled": "true"`, we recommend that you use Amazon EMR reconfiguration to make configuration changes to LLAP\.

Otherwise, for any manual changes to `hive-site.xml`, you must rebuild the LLAP tar archive by using the `hive --service llap` command, as the following example demonstrates\. 

```
# Define how many resources you want to allocate to Hive LLAP

LLAP_INSTANCES=<how many llap daemons to run on cluster>
LLAP_SIZE=<total container size per llap daemon>
LLAP_EXECUTORS=<number of executors per daemon>
LLAP_XMX=<Memory used by executors>
LLAP_CACHE=<Max cache size for IO allocator>

yarn app -enableFastLaunch

hive --service llap \
--instances $LLAP_INSTANCES \
--size ${LLAP_SIZE}m \
--executors $LLAP_EXECUTORS \
--xmx ${LLAP_XMX}m \
--cache ${LLAP_CACHE}m \
--name llap0 \
--auxhbase=false \
--startImmediately
```

## To check hive LLAP status<a name="emr-llap-check"></a>

Use the following command to check the status of Hive LLAP through Hive\.

```
hive --service llapstatus
```

Use the following command to check the status of Hive LLAP using YARN\.

```
yarn app -status (name-of-llap-service)

# example: 
yarn app -status llap0 | jq
```

## To start or stop Hive LLAP<a name="emr-llap-start"></a>

Since Hive LLAP runs as a persistent YARN service, you stop or restart Hive LLAP by stopping or restarting the YARN service, as the following command demonstrates\. 

```
yarn app -stop llap0

yarn app -start llap0
```

## To resize the number of Hive LLAP daemons<a name="emr-llap-resize"></a>

Use the following command to reduce the number of LLAP instances\. 

```
yarn app -flex llap0 -component llap -1
```

For more information, see [Flex a component of a service](https://hadoop.apache.org/docs/r3.2.1/hadoop-yarn/hadoop-yarn-site/yarn-service/QuickStart.html#Flex_a_component_of_a_service)\. 