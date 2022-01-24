# Retry logic<a name="emrfs-retry-logic"></a>

EMRFS tries to verify list consistency for objects tracked in its metadata for a specific number of retries\. The default is 5\. In the case where the number of retries is exceeded the originating job returns a failure unless `fs.s3.consistent.throwExceptionOnInconsistency` is set to `false`, where it will only log the objects tracked as inconsistent\. EMRFS uses an exponential backoff retry policy by default but you can also set it to a fixed policy\. Users may also want to retry for a certain period of time before proceeding with the rest of their job without throwing an exception\. They can achieve this by setting `fs.s3.consistent.throwExceptionOnInconsistency` to `false`, `fs.s3.consistent.retryPolicyType` to `fixed`, and `fs.s3.consistent.retryPeriodSeconds` for the desired value\. The following example creates a cluster with consistency enabled, which logs inconsistencies and sets a fixed retry interval of 10 seconds:

**Example Setting retry period to a fixed amount**  

```
aws emr create-cluster --release-label emr-5.34.0 \
--instance-type m5.xlarge --instance-count 1 \
--emrfs Consistent=true,Args=[fs.s3.consistent.throwExceptionOnInconsistency=false, fs.s3.consistent.retryPolicyType=fixed,fs.s3.consistent.retryPeriodSeconds=10] --ec2-attributes KeyName=myKey
```

**Note**  
Linux line continuation characters \(\\\) are included for readability\. They can be removed or used in Linux commands\. For Windows, remove them or replace with a caret \(^\)\.

For more information, see [Consistent view](emr-plan-consistent-view.md)\.

## EMRFS configurations for IMDS get region calls<a name="randomized-exponential-backoff-retry"></a>

EMRFS relies on the IMDS \(instance metadata service\) to get instance region and Amazon S3, DynamoDB, or AWS KMS endpoints\. However, IMDS has a limit on how many requests it can handle, and requests that exceed that limit will fail\. This IMDS limit can cause EMRFS failures to initialize and cause the query or command to fail\. You can use the following randomized exponential backoff retry mechanism and a fallback region configuration properties in emrfs\-site\.xml to address the scenario where all retries fail\.

```
<property>
    <name>fs.s3.region.retryCount</name>
    <value>3</value>
    <description>
    Maximum retries that would be attempted to get AWS region.
    </description>
</property>
<property>
    <name>fs.s3.region.retryPeriodSeconds</name>
    <value>3</value>
    <description>
    Base sleep time in second for each get-region retry.
    </description>
</property>
<property>
    <name>fs.s3.region.fallback</name>
    <value>us-east-1</value>
    <description>
    Fallback to this region after maximum retries for getting AWS region have been reached.
    </description>
</property>
```