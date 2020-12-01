# Recap

## What is Big data? Vs of Big Data

- volume
- variety
- velocity (speed)

## Why we need Big Data

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
  - 1 commodity server (10 Tb, 32 CPU, 64 RAM) -> 10 Server  

## Benefits horizontal

- reliability (prevents server crashes)
- cost (hardware and software, but not for support)
- scalable
- open source
- heterogenous
- shared resources

## Disadvantage

- very difficult to manage

## HDFS (Storage)

- distributed file system
- written in java
- client-server architecture

## MapReduce

- algorithm (programming model)

Steps:
- Map
- Shuffle and sort
- Reduce

## YARN
 
- allocates resources (*CPU (GPU), RAM,* Disk space, Network)

sergei wants to:
- analize 100TB data, on 10 server (the whole cluster)
- it takes all the resources cluster for 6 hours

What others do?
- they wait

## OLTP vs OLAP

**OLTP** - online transaction processing

- update
- read
- delete
- ...

**OLAP** - online analytical processing

- analize - aggregations, min&max ...

## Data type

- structured - (RDBMS - MySQL, Oracle, PosgresQL ...)
- semi-structured - csv, json, xml (excel)
- unstructured - video, images (excel)

Bit - 0 or 1
Byte - 8 bits

1 GB from Disk -> takes a lot of time
1 TB -> much longer time

## Data Lake vs Data Warehouse

**Data Lake**
- structured

**Data Warehouse**
- structured

## Hive

to be continued ...
