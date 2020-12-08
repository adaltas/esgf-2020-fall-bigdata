
# Hive

[Read the summary](./recap.md).

## Hive Overview

- is a Data Warehouse platform
- provides for OLAP
- is a query engine on top of HDFS
- has SQL syntax: HiveQL (HQL)
- it translates HQL to MapReduce jobs
- it can handle:
  - csv, json ...
  - ORC, Parquet, Avro
  - HBase tables
- it handles tables with schema

## OLTP vs OLAP

**OLTP** - online transaction processing

- update
- read
- delete
- ...

**OLAP** - online analytical processing

- analyze - aggregations, min & max ...

## Type of data

- structured - (RDBMS - MySQL, Oracle, PostgresQL ...)
- semi-structured - csv, json, xml (excel)
- unstructured - video, images (excel)

## Computing resources 

- CPU (central processing unit)
- RAM (random access memory)
- disk (SSD or HD) - **slowest part of the computer**
- network

## Data Lake vs Data Warehouse

**Data Lake**
- raw data (unstructured, semi-structured)
- schema on read

**Data Warehouse**
- clean/optimised data (structured)
- schema on write

## Example: file size optimisation

Since a disk I/O is the slowest resource of the computer, we need to optimise file and data format in it. 

Consider a file containing customers of a bank:

**Schema:**

```
name,age,gender,bank_account,company_id
```

**Data (in CSV format)** (it could weigh many Gb)

```
sergei,30,m,35678899032,0
jules,27,m,15466765432,0
prisca,44,f,76545657687,0
david,42,m,345766564343,12
...
```

Optimising the file:

1. **Transpose file** (from row oriented to column oriented)

```
sergei,jules,prisca,david
30,27,44,42
10032,10031,10067,10034
0,0,0,12
```
  
2. **Calculate metadata** (and keep it close to the data)

```
{name:0:26,age:27:39,bank_account:40:64,company_id:65:74}
```

3. Compress **sparse values** (zero-values)

```
0,0,0,12 -> 3:0,12
```

It takes up less disk space.

4. Use binary formats

Integer value is 2 byte

Example:

- 32767 (integer) -> 2 bytes
- 32767 (string) -> 5 bytes

5. etc.

There are more optimisation ways such as [partitioning](https://data-flair.training/blogs/apache-hive-partitions/) and [bucketing](https://data-flair.training/blogs/bucketing-in-hive/).

## File formats

- **line format** (CSV) -> aggregation on a column implies reading the whole file
- **column format** (ORC - Optimized Row Columnar) -> aggregation: we only read the column

## ORC format

- Optimized Row Columnar
- allow compression

## Hive: 2 types of tables

- **EXTERNAL** tables - points on a folder anywhere on HDFS (ex: in your own HDFS home)
- **MANAGED** (internal) tables - located in Hive folders (ex: `/warehouse/tablespace/managed/hive/your_db.db/your_table`)

## Hive: data ingestion pipeline example

-> cars.csv
-> put on HDFS
-> Hive: External table
-> **SQL map** reading data
-> Hive: (Managed or External) Table, ORC format
-> cars.orc
