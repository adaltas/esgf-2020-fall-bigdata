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
 
- allocates resources (*CPU (GPU), RAM,* Disk space, Network)

**Example:**

A user wants to:
- analize 100TB data, on 10 server (the whole cluster)
- it takes all the cluster resources for 6 hours

What others do?
- they wait

## OLTP vs OLAP

**OLTP** - online transaction processing

- update
- read
- delete
- ...

**OLAP** - online analytical processing

- analyze - aggregations, min&max ...

## Data type

- structured - (RDBMS - MySQL, Oracle, PostgresQL ...)
- semi-structured - csv, json, xml (excel)
- unstructured - video, images (excel)

## Basics

Bit - 0 or 1
Byte - 8 bits

To read 1 GB from Disk -> takes a lot of time
To read 1 TB -> much longer time

## Data Lake vs Data Warehouse

**Data Lake**
- raw data (unstructured, semi-structured)
- schema on read

**Data Warehouse**
- clean/optimised data (structured)
- schema on write

--

# Hive

- Data Warehouse platform
- OLAP
- query engine (SQL-like language - HQL)

## File formats

- **line format** (CSV) -> aggregation on a column implies reading the whole file
- **column format** (ORC - Optimized Row Columnar) -> aggregation: we only read the column

## 2 types of tables

- **EXTERNAL** tables - points on a folder anywhere on HDFS (ex: in your own HDFS home)
- **MANAGED** (internal) tables - located in Hive folders (ex: `/warehouse/tablespace/managed/hive/your_db.db/your_table`)
