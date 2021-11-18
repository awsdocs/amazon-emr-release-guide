# Retry Amazon S3 requests with EMRFS<a name="emr-spark-emrfs-retry"></a>

This topic provides information about the retry strategies that you can use when making requests to Amazon S3 with EMRFS\. When your request rate increases, S3 tries to scale to support the new rate\. During this process S3 can throttle requests and return a `503 Slow Down` error\. To improve the success rate of your S3 requests, you can adjust your retry strategy by configuring properties in your `emrfs-site` configuration\.

You can adjust your retry strategy in the following ways\.
+ Increase the maximum retry limit for the default exponential backoff retry strategy\.
+ Enable and configure the additive\-increase/multiplicative\-decrease \(AIMD\) retry strategy\. AIMD is supported for Amazon EMR versions 6\.4\.0 and later\.

## Use the default exponential backoff strategy<a name="emr-spark-emrfs-retry-exponential-backoff"></a>

By default, EMRFS uses an exponential backoff strategy to retry Amazon S3 requests\. The default EMRFS retry limit is 15\. To avoid an S3 `503 Slow Down` error, you can increase the retry limit when you create a new cluster, on a running cluster, or at application runtime\.

To increase the retry limit, you must change the value for `fs.s3.maxRetries` in your `emrfs-site` configuration\. The following example configuration sets `fs.s3.maxRetries` to a custom value of 30\.

```
[
    {
      "Classification": "emrfs-site",
      "Properties": {
        "fs.s3.maxRetries": "30"
      }
    }
]
```

For more information about working with configuration objects, see [Configure applications](emr-configure-apps.md)\.

## Use the AIMD retry strategy<a name="emr-spark-emrfs-retry-aimd"></a>

With Amazon EMR versions 6\.4\.0 and later, EMRFS supports an alternative retry strategy based on an additive\-increase/multiplicative\-decrease \(AIMD\) model\. The AIMD retry strategy is especially useful when you work with large Amazon EMR clusters\.

AIMD calculates a custom request rate using data about recent successful requests\. This strategy decreases the number of throttled requests and the total attempts required per request\.

To enable the AIMD retry strategy, you must set the `fs.s3.aimd.enabled` property to `true` in your `emrfs-site` configuration as in the following example\.

```
[
    {
      "Classification": "emrfs-site",
      "Properties": {
        "fs.s3.aimd.enabled": "true"
      }
    }
]
```

For more information about working with configuration objects, see [Configure applications](emr-configure-apps.md)\.

## Advanced AIMD retry settings<a name="emr-spark-emrfs-retry-advanced-properties"></a>

You can configure the properties listed in the following table to refine retry behavior when you use the AIMD retry strategy\. For most use cases, we recommend that you use the default values\.


**Advanced AIMD retry strategy properties**  

| Property | Default value | Description | 
| --- | --- | --- | 
| fs\.s3\.aimd\.increaseIncrement | 0\.1 | Controls how quickly the request rate increases when consecutive requests are successful\. | 
| fs\.s3\.aimd\.reductionFactor | 2 | Controls how quickly the request rate decreases when Amazon S3 returns a 503 response\. The default factor of 2 cuts the request rate in half\. | 
| fs\.s3\.aimd\.minRate | 0\.1 | Sets the lower bound for the request rate when requests experience sustained throttling by S3\. | 
| fs\.s3\.aimd\.initialRate | 5500 | Sets the initial request rate, which then changes according to the values that you specify for fs\.s3\.aimd\.increaseIncrement and fs\.s3\.aimd\.reductionFactor\.The initial rate is also used for GET requests, and scaled proportionally \(3500/5500\) for PUT requests\. | 
| fs\.s3\.aimd\.adjustWindow | 2 | Controls how frequently the request rate is adjusted, measured in number of responses\. | 
| fs\.s3\.aimd\.maxAttempts | 100 | Sets the maximum number of attempts to try a request\. | 