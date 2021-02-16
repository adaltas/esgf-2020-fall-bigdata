# Lab

## Objectives

1. Communicate with HBase via `hbase shell`
2. Try queries
3. Create the IMDB reviews table

## Prerequisites

To execute the following code you have to be connected to the `edge-1.au.adaltas.cloud` node via SSH (and VPN).

## 1. Communicate with HBase via `hbase shell`

1. Run `hbase shell` to start HBase client

2. Run different commands:

- `list` - lists tables
- `status` - status of the system
- `version` - prints HBase version
- `whoami` - prints user details of HBase
- `help` or `table_help` - prints help information about existing commands

## 2. Try queries

1. Scan tables

Using the `scan '<table name>'` command explore existing tables.

2. Read data 

Explore existing tables using these commands:

- `get '<table name>','<row>'` - reads a specific row
- `get '<table name>','<row>',{COLUMN => '<colfamily:colname>'}` - reads a specific row and a column

2. Create a table 

- `create '<table name>','<column family>'` - creates table with column family name

> Note, create a table in a namespace with a name prefixed with `esgf_2021_spring:`. 

For example, to create a table for IMDB opinions with 2 column families `meta` and `review`, run the command (replace `<your name>`):

```
create 'esgf_2021_spring:<your name>', 'meta', 'review'
```

3. Write data into a table

- `put '<table name>','<row>','<colfamily:colname>','<value>'` - writes a value into specific column

Try to write something, for example like this (replace `<your name>`):

```
put 'esgf_2021_spring:<your name>', '1', 'meta:name', 'Pulp Fiction'
```

## 3. Create the IMDB reviews table

Create a table containing reviews of IMDB movies.

Extract manually several reviews about [this movie](https://www.imdb.com/title/tt0110912/reviews?ref_=tt_ov_rt) and insert it into HBase.

1. Create columns such as "tconst" (alphanumeric unique identifier of the title), title, user id, comment and rating. Split them into two column families `meta` and `review`.

2. Design the Row key.

> Tip, you need to think about how this data is used. For example, there is a filtering functionality on the page. It filters by "rating" number from 1 to 10, so, you have to retrieve the data from the database by the specific rating value. Don't forget to include the identifier of the movie, because it extracts reviews about the specific movie.

3. Insert some data into the table using similar commands from part 2.
