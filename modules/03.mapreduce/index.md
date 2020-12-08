
# Hadoop MapReduce

**Hadoop MapReduce** is a software framework and programming model used for processing huge amounts of data in-parallel on large clusters (thousands of nodes) of commodity hardware in a reliable, fault-tolerant manner.


## How does MapReduce work?

It work in two phases:

1. Map - tasks of splitting and mapping of data
2. Reduce - tasks of shuffle and reduce the data

A MapReduce job usually splits the input data-set into independent chunks which are processed by the **map tasks** in a completely parallel manner. The framework sorts the outputs of the maps, which are then input to the **reduce tasks**. Typically both the input and the output of the job are stored in a file-system. The framework takes care of scheduling tasks, monitoring them and re-executes the failed tasks.

Typically the compute nodes and the storage nodes are the same, that is, the MapReduce framework and the HDFS are running on the same set of nodes. This configuration allows the framework to effectively schedule tasks on the nodes where data is already present, resulting in very high aggregate bandwidth across the cluster.

## MapReduce example

![Wordcount example](image/mapreduce.png)

## Inputs and Outputs

The MapReduce framework operates exclusively on `<key, value>` pairs, that is, the framework views the input to the job as a set of `<key, value>` pairs and produces a set of `<key, value>` pairs as the output of the job, conceivably of different types.

Input and Output types of a MapReduce job:

(input) `<k1, v1>` -> **map** -> `<k2, v2>` -> **combine** -> `<k2, v2>` -> **reduce** -> `<k3, v3>`(output)
