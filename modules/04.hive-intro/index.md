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

## Example: bank customers

**Schema:**

name,age,gender,bankaccount,company_id

**Data (in CSV format) - 10 Gb:**

```
sergei,30,m,35678899032,0
jules,27,m,15466765432,0
prisca,44,f,76545657687,0
david,42,m,345766564343,12
...
```

### Optimising the file:

1. Transpose file (from row oriented to column oriented)

```
sergei,jules,prisca,david
30,27,44,42
10032,10031,10067,10034
0,0,0,12
```
  
2. Calculate metadata and keep it

{name:0:26,age:27:39,...}
  
3. Compress **sparse values**

```
sergei,jules,prisca,david
30,27,44,42
10032,10031,10067,10034
3:0,12
```

4. Use binary formats

Integer value is 2 byte

Example: 
- 32767 (integer) -> 2 bytes
- 32767 (string) -> 5 bytes

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

## The end
