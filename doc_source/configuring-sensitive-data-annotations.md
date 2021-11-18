# Mask sensitive data<a name="configuring-sensitive-data-annotations"></a>

You can configure sensitive data to never be exposed via any Amazon EMR API using the annotation `EMR.mask@`\. This annotation denotes that a key\-value pair contains sensitive information and replaces the value with placeholder `********` when returning configurations via an external API\. This substitution complements and extends Amazon EMR's existing sensitive field substitution, which selectively blocks information exposure when a known sensitive field is detected\. The `EMR.mask@` annotation also provides you with the functionality to mark any field as sensitive instead of relying on EMR to detect every possible sensitive field existing in free\-form configuration\. You can use this annotation to mask any application's configuration\.

The following is an example of configuring a field as sensitive:

```
{
 "Classification": "core-site",
 "Properties": {
   "presto.s3.access-key": "<sensitive-access-key>",
   "EMR.mask@presto.s3.secret-key": "<my-secret-key>"
  }
}
```

After you submit your annotated configuration when creating your cluster, Amazon EMR validates the configuration properties\. Currently, EMR only recognizes the `EMR.mask@` annotation as valid\. If your configuration is valid, Amazon EMR strips the annotation from the configuration to create the actual configuration before applying it to the cluster:

```
{
 "Classification": "core-site",
 "Properties": {
   "presto.s3.access-key": "<sensitive-access-key>",
   "presto.s3.secret-key": "<my-secret-key>"
  }
}
```

When you call an action like DescribeCluster, Amazon EMR returns the current application configuration on the cluster\. If an application configuration property is masked by sensitive annotation, then the application configuration returned by the DescribeCluster call will be redacted:

```
{
 "Classification": "core-site",
 "Properties": {
   "presto.s3.access-key": "<sensitive-access-key>",
   "EMR.mask@presto.s3.secret-key": "********"
  }
}
```