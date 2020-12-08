
# Hadoop introduction

- how you store, compute and serve data?
- distributed systems - set of computers

# Why distributed systems?

Scaling:
- vertical (cpu, disc, ram) - better for a little scaling
- horizontal - scale more. Logariphmique evolution of complexity

## Type of data

1. structured (RDBMS)
2. semi-structured (json, xml, ...) - NoSQL DB
3. unstructured data (image, sound) - 90% 

- Moore's Law not the case anymore - we need horizontal scaling.

## Advantages

- scalable
- open
- heterogenous
- shared resources 

## Disadvantages

- it is hard to manage

## Big Data Vs

- Volume
- Velocity
- Variety
- ...

## Hadoop ecosystem

- a set of technologies
- cluster - set of servers

## Origin

- Doug Cutting - 2003 - Nutch
- Google - 2004 - MR algorithm and Google FS (same like any file system but distributed to many servers)
- Doug Cutting -> Hadoop (2004) -> Hadoop 1 (2009) -> Hadoop 2 (2011) (still shifting to Hadoop 3) -> Hadoop 3 (2017)

## Hadoop 1

Hive, Pig
MR - not very well handle resources
HDFS

## Hadoop 2

Hive, ...
YARN
HDFS

## Hadoop 3

Differnces in technologies...

## Hadoop Distributions

Since it is Open Source - you can install, but it is hard.
The reason why Hadoop technologies is payed.

- Hortonworks Data Platform (HDP)
- Cloudera Data Platform (CDP)
- MapR
- Cloud (AWS, GCP, Azure ...)

## Open Source

- Apache Fondation
- you pay for the support
- but it is cheaper than vertical scaling systems like Oracle
- you install on commodity servers (normal ones - 64 Gb of RAM)

## Jobs in Big Data

- Data analyst (BI, data visualization, ...)
- Data science (ML, DL, visualization, *feature engineering*)
- Data engineering (ingest data) (ex: put data together of marketing and sells departments, also Data scientist should can handle this)
- Big Data architect, cluster administrators (know every technologies)
- System administrators
