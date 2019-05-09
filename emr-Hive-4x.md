# Considerations for Using Hive on Amazon EMR 4\.x<a name="emr-Hive-4x"></a>

This section covers differences to consider when using Hive version 1\.0\.0 on Amazon EMR 4\.x release versions, as compared to Hive 2\.x on Amazon EMR 5\.x release versions\.

## ACID Transactions Not Supported<a name="emr-Hive-acid-4x"></a>

Hive on Amazon EMR 4\.x release versions does not support ACID transactions with Hive data stored in Amazon S3 when using 4\.x release versions\. If you try to create a transactional table in Amazon S3, an exception occurs\.

## Reading and Writing to Tables in Amazon S3<a name="emr-Hive-s3table-4x"></a>

Hive on Amazon EMR 4\.x release versions can write directly to Amazon S3 without using temporary files\. This improves performance, but a consequence is that you cannot read and write to the same table in Amazon S3 within the same Hive statement\. A workaround is to create and use a temporary table in HDFS\.

The following example shows how to use multiple Hive statements to update a table in Amazon S3\. The statements create a temporary table in HDFS named `tmp` based on a table in Amazon S3 named `my_s3_table`\. The table in Amazon S3 is then updated with the contents of the temporary table\.

```
CREATE TEMPORARY TABLE tmp LIKE my_s3_table;
INSERT OVERWRITE TABLE tmp SELECT ....;
INSERT OVERWRITE TABLE my_s3_table SELECT * FROM tmp;
```

## Log4j vs\. Log4j 2<a name="emr-Hive-log4j-4x"></a>

Hive on Amazon EMR 4\.x release versions uses Log4j\. Beginning with version 5\.0\.0, Log4j 2 is the default\. These versions may require different logging configurations\. See [Apache Log4j 2](http://logging.apache.org/log4j/2.x/) for details\.

## MapReduce is the Default Execution Engine<a name="emr-Hive-tez-4x"></a>

Hive on Amazon EMR 4\.x release versions uses MapReduce as the default execution engine\. Beginning with Amazon EMR version 5\.0\.0, Tez is the default, which provides improved performance for most workflows\.

## Hive Authorization<a name="emr-Hive-authz-4x"></a>

Hive on Amazon EMR 4\.x release versions supports [Hive Authorization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+Authorization) for HDFS but not for EMRFS and Amazon S3\. Amazon EMR clusters run with authorization disabled by default\.

## Hive File Merge Behavior with Amazon S3<a name="emr-Hive-filemerge-4x"></a>

Hive on Amazon EMR 4\.x release versions merges small files at the end of a map\-only job if `hive.merge.mapfiles` is `true`\. A merge is triggered only if the average output size of the job is less than the `hive.merge.smallfiles.avgsize` setting\. Amazon EMR Hive has exactly the same behavior if the final output path is in HDFS\. If the output path is in Amazon S3, however, the `hive.merge.smallfiles.avgsize` parameter is ignored\. In that situation, the merge task is always triggered if `hive.merge.mapfiles` is set to `true`\.