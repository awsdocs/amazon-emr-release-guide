# Process Data with Streaming<a name="UseCase_Streaming"></a>

Hadoop Streaming is a utility that comes with Hadoop that enables you to develop MapReduce executables in languages other than Java\. Streaming is implemented in the form of a JAR file, so you can run it from the Amazon EMR API or command line just like a standard JAR file\. 

This section describes how to use Streaming with Amazon EMR\. 

**Note**  
Apache Hadoop Streaming is an independent tool\. As such, all of its functions and parameters are not described here\. For more information about Hadoop Streaming, go to [http://hadoop\.apache\.org/docs/stable/hadoop\-streaming/HadoopStreaming\.html](http://hadoop.apache.org/docs/stable/hadoop-streaming/HadoopStreaming.html)\.

## Using the Hadoop Streaming Utility<a name="HadoopStreamCommands"></a>

This section describes how use to Hadoop's Streaming utility\.


**Hadoop Process**  

|  |  | 
| --- |--- |
| 1 |  Write your mapper and reducer executable in the programming language of your choice\. Follow the directions in Hadoop's documentation to write your streaming executables\. The programs should read their input from standard input and output data through standard output\. By default, each line of input/output represents a record and the first tab on each line is used as a separator between the key and value\.  | 
| 2 |  Test your executables locally and upload them to Amazon S3\.  | 
| 3 |  Use the Amazon EMR command line interface or Amazon EMR console to run your application\.   | 

Each mapper script launches as a separate process in the cluster\. Each reducer executable turns the output of the mapper executable into the data output by the job flow\.

The `input`, `output`, `mapper`, and `reducer` parameters are required by most Streaming applications\. The following table describes these and other, optional parameters\.


| Parameter | Description | Required | 
| --- | --- | --- | 
| \-input |  Location on Amazon S3 of the input data\. Type: String Default: None Constraint: URI\. If no protocol is specified then it uses the cluster's default file system\.   | Yes | 
| \-output |  Location on Amazon S3 where Amazon EMR uploads the processed data\. Type: String Default: None Constraint: URI Default: If a location is not specified, Amazon EMR uploads the data to the location specified by `input`\.  | Yes | 
| \-mapper |  Name of the mapper executable\. Type: String Default: None  | Yes | 
| \-reducer |  Name of the reducer executable\. Type: String Default: None  | Yes | 
| \-cacheFile |  An Amazon S3 location containing files for Hadoop to copy into your local working directory \(primarily to improve performance\)\. Type: String Default: None Constraints: \[URI\]\#\[symlink name to create in working directory\]   | No | 
| \-cacheArchive |  JAR file to extract into the working directory Type: String Default: None Constraints: \[URI\]\#\[symlink directory name to create in working directory   | No | 
| \-combiner |  Combines results Type: String Default: None Constraints: Java class name  | No | 

The following code sample is a mapper executable written in Python\. This script is part of the WordCount sample application\.

```
 1. #!/usr/bin/python
 2. import sys
 3. 
 4. def main(argv):
 5.   line = sys.stdin.readline()
 6.   try:
 7.     while line:
 8.       line = line.rstrip()
 9.       words = line.split()
10.       for word in words:
11.         print "LongValueSum:" + word + "\t" + "1"
12.       line = sys.stdin.readline()
13.   except "end of file":
14.     return None
15. if __name__ == "__main__":
16.   main(sys.argv)
```