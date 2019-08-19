# Considerations for Using Pig on Amazon EMR 4\.x<a name="emr-Pig-4x"></a>

Pig version 0\.14\.0 is installed on clusters created using Amazon EMR 4\.x release versions\. Pig was upgraded to version 0\.16\.0 in Amazon EMR 5\.0\.0\. Significant differences are covered below\.

## Different Default Execution Engine<a name="emr-Pig-engine-4x"></a>

Pig version 0\.14\.0 on Amazon EMR 4\.x release versions uses MapReduce as the default execution engine\. Pig 0\.16\.0 and later use Apache Tez\. You can explicitly set `exectype=mapreduce` in the `pig-properties` configuration classification to use MapReduce\.

## Dropped Pig User\-Defined Functions \(UDFs\)<a name="emr-Pig-udf-4x"></a>

Custom UDFs that were available in Pig on Amazon EMR 4\.x release versions were dropped beginning with Pig 0\.16\.0\. Most of the UDFs have equivalent functions you can use instead\. The following table lists dropped UDFs and equivalent functions\. For more information, see [Built\-in Functions](https://pig.apache.org/docs/r0.16.0/func.html) on the Apache Pig site\.


| Dropped UDF | Equivalent Function | 
| --- | --- | 
|  FORMAT\_DT\(dtformat, date\)  |  GetHour\(date\), GetMinute\(date\), GetMonth\(date\), GetSecond\(date\), GetWeek\(date\), GetYear\(date\), GetDay\(date\)  | 
|  EXTRACT\(string, pattern\)  |  REGEX\_EXTRACT\_ALL\(string, pattern\)  | 
|  REPLACE\(string, pattern, replacement\)  |  REPLACE\(string, pattern, replacement\)  | 
|  DATE\_TIME\(\)  |  ToDate\(\)  | 
|  DURATION\(dt, dt2\)  |  WeeksBetween\(dt, dt2\), YearsBetween\(dt, dt2\), SecondsBetween\(dt, dt2\), MonthsBetween\(dt, dt2\), MinutesBetween\(dt, dt2\), HoursBetween\(dt, dt2\)  | 
|  EXTRACT\_DT\(format, date\)  |  GetHour\(date\), GetMinute\(date\), GetMonth\(date\), GetSecond\(date\), GetWeek\(date\), GetYear\(date\), GetDay\(date\)  | 
|  OFFSET\_DT\(date, duration\)  |  AddDuration\(date, duration\), SubtractDuration\(date, duration\)  | 
|  PERIOD\(dt, dt2\)  |  WeeksBetween\(dt, dt2\), YearsBetween\(dt, dt2\), SecondsBetween\(dt, dt2\), MonthsBetween\(dt, dt2\), MinutesBetween\(dt, dt2\), HoursBetween\(dt, dt2\)  | 
|  CAPITALIZE\(string\)  |  UCFIRST\(string\)  | 
|  CONCAT\_WITH\(\)  |  CONCAT\(\)  | 
|  INDEX\_OF\(\)  |  INDEXOF\(\)  | 
|  LAST\_INDEX\_OF\(\)  |  LAST\_INDEXOF\(\)  | 
|  SPLIT\_ON\_REGEX\(\)  |  STRSPLT\(\)  | 
|  UNCAPITALIZE\(\)  |  LCFIRST\(\)  | 

The following UDFs were dropped with no equivalent: FORMAT\(\), LOCAL\_DATE\(\), LOCAL\_TIME\(\), CENTER\(\), LEFT\_PAD\(\), REPEAT\(\), REPLACE\_ONCE\(\), RIGHT\_PAD\(\), STRIP\(\), STRIP\_END\(\), STRIP\_START\(\), SWAP\_CASE\(\)\.

## Discontinued Grunt Commands<a name="emr-pig-gruntcmd-4x"></a>

Some Grunt commands were discontinued beginning with Pig 0\.16\.0\. The following table lists Grunt commands in Pig 0\.14\.0 and the equivalent commands in the current version, where applicable\. 


**Pig 0\.14\.0 and Equivalent Current Grunt Commands**  

| Pig 0\.14\.0 Grunt command | Pig Grunt command in 0\.16\.0 and later | 
| --- | --- | 
|  cat <non\-hdfs\-path>\)  |  fs \-cat <non\-hdfs\-path>;  | 
| cd <non\-hdfs\-path>; |  No equivalent  | 
| ls <non\-hdfs\-path>; | fs \-ls <non\-hdfs\-path>; | 
|  move <non\-hdfs\-path> <non\-hdfs\-path>;  |  fs \-mv <non\-hdfs\-path> <non\-hdfs\-path>;  | 
| copy <non\-hdfs\-path> <non\-hdfs\-path>; |  fs \-cp <non\-hdfs\-path> <non\-hdfs\-path>;  | 
| copyToLocal <non\-hdfs\-path> <local\-path>; |  fs \-copyToLocal <non\-hdfs\-path> <local\-path>;  | 
| copyFromLocal <local\-path> <non\-hdfs\-path>; |  fs \-copyFromLocal <local\-path> <non\-hdfs\-path>;  | 
| mkdir <non\-hdfs\-path>; |  fs \-mkdir <non\-hdfs\-path>;  | 
| rm <non\-hdfs\-path>; |  fs \-rm \-r \-skipTrash <non\-hdfs\-path>;  | 
|  rmf <non\-hdfs\-path>;  |  fs \-rm \-r \-skipTrash <non\-hdfs\-path>;  | 

## Capability Removed for Non\-HDFS Home Directories<a name="emr-Pig-users-4x"></a>

Pig 0\.14\.0 on Amazon EMR 4\.x release versions has two mechanisms to allow users other than the `hadoop` user, who don't have home directories, to run Pig scripts\. The first mechanism is an automatic fallback that sets the initial working directory to the root directory if the home directory doesn't exist\. The second is a `pig.initial.fs.name` property that allows you to change the initial working directory\.

These mechanisms are not available beginning with Amazon EMR version 5\.0\.0, and users must have a home directory on HDFS\. This doesn't apply to the `hadoop` user because a home directory is provisioned at launch\. Scripts run using Hadoop jar steps default to the Hadoop user unless another user is explicitly specified using `command-runner.jar`\.