# Lab: Hive

## Objectives

1. Learn basic HQL commands
2. Create an external table on top of data stored as CSV
3. Create a managed ORC table
4. Load data from the CSV table to the ORC table (with some transformations)

## 1. Learn basic HQL commands

1. Enter to the Edge node of the cluster using VPN
2. Open a Beeline session by typing `beeline`
3. Try commands:

`SHOW DATABASES;` - lists all databases
`SHOW TABLES;` - lists all tables in the current database
`USE DATABASE_NAME;` - change current database (replace `<DATABASE_NAME>`)
`SELECT * FROM TABLE_NAME` - show all data from the table (replace `<DATABASE_NAME>`)
`SELECT * FROM TABLE_NAME LIMIT 10` - show 10 rows from the table (replace `<DATABASE_NAME>`)

You can try this for example:

```
USE esgf_2020_fall_1;
SHOW TABLES;
SELECT * FROM sergei_drivers_ext;
SELECT * FROM sergei_drivers_ext LIMIT 5;
```

## 2. Create an external table

For this lab we will be using a very small dataset of taxi drivers.

Using the official [Hive Data Definition Langage](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL):

1. Using the HDFS CLI, take a look at the data used for this lab at `/data/drivers/drivers.csv`
2. Copy the `drivers` folder to your user home directory on HDFS:
   ```sh
   hdfs dfs -mkdir -p "drivers"
   hdfs dfs -cp /data/drivers/drivers.csv drivers
   ```
3. Open a Beeline session by typing `beeline`
4. Create an external table targeting our data with this statement (to be completed, replace `YOUR_USERNAME`):
   ```sql
   use esgf_2020_fall_1;
   SET hivevar:username=YOUR_USERNAME;
   CREATE EXTERNAL TABLE ${username}_drivers_ext (
     driver_id INT,
     -- COMPLETE HERE
   )
   ROW FORMAT SERDE -- COMPLETE HERE
   STORED AS TEXTFILE
   LOCATION -- COMPLETE HERE
   TBLPROPERTIES ('skip.header.line.count'='1');
   ```
5. Check that the table is correctly created by selecting all the data in it. **If you see only `NULL` values, your schema is not correct.**

## 3. Create a managed ORC table

**Tip:** to create a managed ORC table, you don't have to specify a `LOCATION` nor a `SERDE`:

```sql
CREATE ...
STORED AS ORC;
```

1. Create a managed ORC table (**not external**) that must have the same schema as the external table created above (`${username}_drivers_ext`) but with:
   1. The `_ext` prefix removed from the name: `${username}_drivers`
   2. The column `name` devided into `first_name` and `last_name`
   3. The columne `location` renamed as `address` (because `LOCATION` is a Hive keyword)
   4. The column `certified` as a `BOOLEAN`
2. Check that your table was created using the HDFS CLI at `/warehouse/tablespace/managed/hive/esgf_2020_fall_1.db/YOUR_USERNAME_drivers` (should be empty)

## 4. Load data from the CSV table to the ORC table

Now we want to populate our ORC table from our CSV table. Using the [Hive Data Manipulation Language](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML):

1. Write a statement to insert data to the ORC table by applying 2 transformations (check the available [HiveQL string functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-StringFunctions)):
   - Split `name` into `first_name` and `last_name`
   - Transform `certified` from `STRING` to `BOOLEAN`
   - Rename `location` to `address`
2. Execute your query
3. Check what the data looks like in the managed table using the HDFS CLI at `/warehouse/tablespace/managed/hive/esgf_2020_fall_1.db/$USER_nyc_drivers`
