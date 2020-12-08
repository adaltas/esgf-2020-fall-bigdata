# Lab

The goal of this lab is to demonstrate how to submit a YARN job and extract information about its running parameters through the YARN UI.

We will use one of the benchmarking tool as an example application - **TeraSort benchmark** - that are included in the Apache Hadoop distribution and therefore represented in the Adaltas Clouds cluster.

## Objectives

You will submit following YARN jobs:

1. TeraGen
2. TeraSort
3. TeraValidate

## About TeraSort benchmark

Hadoop TeraSort is a well-known benchmark that aims to sort big volume of data as fast as possible using Hadoop MapReduce. TeraSort benchmark stresses almost every part of the Hadoop MapReduce framework as well as the HDFS filesystem making it an ideal choice to fine-tune the configuration of a Hadoop cluster. This benchmark consists of 3 components that run sequentially:

- **TeraGen** - generates random data
- **TeraSort** - does the sorting using MapReduce
- **TeraValidate** - used to validate the output

The following steps will show you how to run the TeraSort benchmark on the Hadoop Adaltas Cloud cluster:

[[info | Clean up]]
| After performing all these steps, don’t forget to delete input and output directories for TeraSort, so that the next benchmark can be run without any storage issue.

## 1. Submit TeraGen job 

The first step of the TeraSort benchmark is the data generation. You can use the `teragen` command to generate the input data for the TeraSort benchmark. The first parameter of `teragen` is the number of records and the second parameter is the HDFS directory to generate the data. The following command generates 1 GB of data consisting of 10 million records to the `tera-in` directory in HDFS:

```bash{outputLines: 2-3}{promptUser: sergei}{promptHost: edge-1.au.adaltas.cloud}
yarn jar \
/usr/hdp/3.1.0.0-78/hadoop-mapreduce/hadoop-mapreduce-examples-*.jar \
teragen 10000000 tera-in
```

Once you've submitted a YARN application you can monitor its execution via YARN ResourceManager UI described in [the next section](/#monitoring-with-yarn-resourcemanager-ui). It also will output a log information to the console. Where after establishing connection and passing Kerberos authentication, you can see a job submission log and its execution process with the percentage of the Map and Reduce tasks performed. After the job is finished it will output a summary information about executed process and the used resources:

```
...
20/06/17 18:11:14 INFO impl.YarnClientImpl: Submitted application application_1587994786721_0137
20/06/17 18:11:14 INFO mapreduce.Job: The url to track the job: http://yarn-rm-1.au.adaltas.cloud:8088/proxy/application_1587994786721_0137/
20/06/17 18:11:14 INFO mapreduce.Job: Running job: job_1587994786721_0137
20/06/17 18:11:21 INFO mapreduce.Job: Job job_1587994786721_0137 running in uber mode : false
20/06/17 18:11:21 INFO mapreduce.Job:  map 0% reduce 0%
20/06/17 18:11:30 INFO mapreduce.Job:  map 50% reduce 0%
20/06/17 18:11:32 INFO mapreduce.Job:  map 100% reduce 0%
20/06/17 18:11:32 INFO mapreduce.Job: Job job_1587994786721_0137 completed successfully
20/06/17 18:11:32 INFO mapreduce.Job: Counters: 33
	File System Counters
		FILE: Number of bytes read=0
		FILE: Number of bytes written=483096
		FILE: Number of read operations=0
		FILE: Number of large read operations=0
		FILE: Number of write operations=0
    ...
	Job Counters 
		Launched map tasks=2
		Other local map tasks=2
		Total time spent by all maps in occupied slots (ms)=81080
		...
	Map-Reduce Framework
		Map input records=10000000
		Map output records=10000000
		Input split bytes=167
		Spilled Records=0
		Failed Shuffles=0
		Merged Map outputs=0
		GC time elapsed (ms)=236
		CPU time spent (ms)=20050
		...
	File Input Format Counters 
		Bytes Read=0
	File Output Format Counters 
		Bytes Written=1000000000
```

## 2. Submit TeraSort job

The second step of the TeraSort benchmark is the execution of the TeraSort MapReduce computation on the data generated in step 1 using the following command. TeraSort reads the input data and uses MapReduce to sort the data. The first parameter of the `terasort` command is the input of HDFS data directory, and the second part of the `terasort` command is the output of the HDFS data directory.

```bash{outputLines: 2-3}{promptUser: sergei}{promptHost: edge-1.au.adaltas.cloud}
yarn jar \
/usr/hdp/3.1.0.0-78/hadoop-mapreduce/hadoop-mapreduce-examples-*.jar \
terasort tera-in tera-out
```

## 3. Submit TeraValidate job

The last step of the TeraSort benchmark is the validation of the results. TeraValidate validates the sorted output to ensure that the keys are sorted within each file. If anything is wrong with the sorted output, the output of this reducer reports the problem. This can be done using the `teravalidate` application as follows. The first parameter is the directory with the sorted data and the second parameter is the directory to store the report containing the results.

```bash{outputLines: 2-3}{promptUser: sergei}{promptHost: edge-1.au.adaltas.cloud}
yarn jar \
/usr/hdp/3.1.0.0-78/hadoop-mapreduce/hadoop-mapreduce-examples-*.jar \
teravalidate tera-out tera-validate
```

In the result of these 3 steps we submitted 3 YARN applications sequentially.
