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

- `SHOW DATABASES;` - lists all databases
- `SHOW TABLES;` - lists all tables in the current database
- `USE DATABASE_NAME;` - change current database (replace `<DATABASE_NAME>`)
- `SELECT * FROM TABLE_NAME` - show all data from the table (replace `<DATABASE_NAME>`)
- `SELECT * FROM TABLE_NAME LIMIT 10` - show 10 rows from the table (replace `<DATABASE_NAME>`)

You can try this for example:

```sql
USE esgf_2020_fall_1;
SHOW TABLES;
SELECT * FROM sergei_drivers_ext;
SELECT * FROM sergei_drivers_ext LIMIT 5;
```

## 2. Create an external table

For this lab we will be using a very small dataset of taxi drivers.

Using the official [Hive Data Definition Langage](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL):

1. Using the (HDFS CLI)[https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HDFSCommands.html#dfs], take a look at the data used for this lab at `/data/drivers/drivers.csv`

2. Copy the `drivers` folder to your user home directory on HDFS:

```sh
hdfs dfs -mkdir -p "drivers"
hdfs dfs -cp /data/drivers/drivers.csv drivers
```
   
3. Open a Beeline session by typing `beeline`. (To disconnect from Beeline press `CTRL + C`).

4. Use prepared database `esgf_2020_fall_1` and define your username (replace `YOUR_USERNAME`). **Don't forget to run it every time you open a Beeline session:**

```sql
use esgf_2020_fall_1;
SET hivevar:username=YOUR_USERNAME;
```

5. Create an external table targeting our data with this statement (complete missing parts):

```sql
CREATE EXTERNAL TABLE IF NOT EXISTS esgf_2020_fall_1.${username}_drivers_ext (
  driver_id INT,
  -- COMPLETE HERE
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
STORED AS TEXTFILE
LOCATION 'drivers/'
TBLPROPERTIES ('skip.header.line.count'='1');
```

6. Check that the table is correctly created by selecting all the data in it. **If you see only `NULL` values, your schema is not correct.**

## 3. Create a managed ORC table

1. Create a managed ORC table (**not external**) that must have the same schema as the external table created above (`${username}_drivers_ext`) but with:
   1. The `_ext` prefix removed from the name: `${username}_drivers`
   2. The column `name` divided into `first_name` and `last_name`
   3. The column `location` renamed as `address` (because `LOCATION` is a Hive keyword)
   4. The column `certified` as a `BOOLEAN`
2. Check that your table was created using the HDFS CLI at `/warehouse/tablespace/managed/hive/esgf_2020_fall_1.db/YOUR_USERNAME_drivers` (should be empty)

**Tip:** to create a managed ORC table, you don't have to specify a `LOCATION` nor a `SERDE`.

```sql
CREATE TABLE IF NOT EXISTS esgf_2020_fall_1.${username}_drivers (
  driver_id INT,
  -- COMPLETE HERE
)
STORED AS ORC;
```

## 4. Load data from the CSV table to the ORC table

Now we want to populate our ORC table from our CSV table. Using the [Hive Data Manipulation Language](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DML):

1. Write a statement to insert data to the ORC table by applying 2 transformations (check the available [HiveQL string functions](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF#LanguageManualUDF-StringFunctions)):
   - Split `name` into `first_name` and `last_name`
   - Transform `certified` from `STRING` to `BOOLEAN`
   - Rename `location` to `address`
2. Execute your query
3. Check what the data looks like in the managed table using the HDFS CLI at `/warehouse/tablespace/managed/hive/esgf_2020_fall_1.db/$USER_nyc_drivers`

```sql
INSERT OVERWRITE TABLE esgf_2020_fall_1.${username}_drivers
SELECT 
  driver_id,
  -- COMPLETE HERE
FROM esgf_2020_fall_1.${username}_drivers_ext;
```

4. Check that the data were correctly inserted by selecting all data.

## Bonus 1. Analyze the data

1. Count certified drivers
2. Find the maximum `ssn` value

## Bonus 2. Play with a bigger data set

1. Chose an interesting data set in `/data` folder on HDFS (explore with `hdfs dfs -ls /data`) and make a managed ORC table using the same way like in the steps 2-4 of the lab.

2. Explore created ORC files and compare it with the original CSV (the file size for example).

3. Make some analyze on your choice.
