
# Recap

## Vs of Big Data

- volume
- variety
- velocity (speed)

## Why we need Big Data?

- data -> value (insights, information)

## What do we do with Data?

- capture: sensors, usage of web-sites, IoT devices
- store
- treat/process, analyze
- search

## Hadoop

- is ecosystem of technologies laying on HDFS (Hadoop distributed file system)

## Scaling

~1Tb -> 100TB

- Vertical (Oracle):
  - max Disk space: 100 Tb SSD (faster then HD)
  - max RAM: 256 GB
  - max CPU: 128 cores

- Horisontal (Hadoop)
  - 1 commodity server (10 Tb, 32 CPU, 64 RAM) -> 10 servers  

## Benefits of horizontal scaling

- reliability (prevents server crashes)
- cost (hardware and software, but not for support)
- scalable
- open source
- heterogenous
- shared resources

## Disadvantage

- it is hard to manage

## HDFS (Storage)

- distributed file system
- written in java
- client-server architecture

## MapReduce

- algorithm (programming model)

Steps:

1. Map
2. Shuffle and sort
3. Reduce

## YARN
 
- allocates resources (CPU (GPU), RAM, Disk space, Network)

**Example:**

A user wants to:
- analize 100TB data, on 10 server (the whole cluster)
- it takes all the cluster resources for 6 hours

What others do?
- they wait
