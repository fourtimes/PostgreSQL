### PostgreSQL DATABASE, TABLE Creation
---
```bash
# CREATE DATABASE syntax
CREATE DATABASE database_name;

# List the databases
\l

# Enter into the specified database syntax
\c database_name;

# CREATE TABLE syntax
CREATE TABLE table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
   PRIMARY KEY( one or more columns )
);

# List all the tables in specified database
 \d

# Describe the specified tables details
 \d table_name

# DROP TABLE
DROP TABLE table_name;
```
### INSERT, UPDATE, WHERE
---
```bash
# INSERT the values
INSERT INTO TABLE_NAME (column1, column2, column3,...columnN)
VALUES (value1, value2, value3,...valueN);

# SELECT the values in specified tables
SELECT * FROM table_name;
SELECT column1, column2, columnN FROM table_name;

# WHERE Condition syntax
SELECT column1, column2, columnN
FROM table_name
WHERE [search_condition]
ex
------
SELECT * FROM COMPANY WHERE AGE >= 25 OR SALARY >= 65000;

# UPDATE syntax
UPDATE table_name
SET column1 = value1, column2 = value2...., columnN = valueN
WHERE [condition];

# DELETE specified row and columns
DELETE FROM table_name
WHERE [condition];

# AND
SELECT column1, column2, columnN
FROM table_name
WHERE [condition1] AND [condition2]...AND [conditionN];

# OR
SELECT column1, column2, columnN
FROM table_name
WHERE [condition1] OR [condition2]...OR [conditionN]
ex
------
SELECT * FROM COMPANY WHERE AGE >= 25 OR SALARY >= 65000;
```
### ALTER TABLE syntax
---
```bash
# add a new column
ALTER TABLE table_name ADD column_name datatype;

# drop column
ALTER TABLE table_name DROP COLUMN column_name;

#Change the DATA TYPE of a column
ALTER TABLE table_name ALTER COLUMN column_name TYPE datatype;

# add a NOT NULL constraint to a column
ALTER TABLE table_name MODIFY column_name datatype NOT NULL;

#  ADD PRIMARY KEY
ALTER TABLE table_name
ADD CONSTRAINT MyPrimaryKey PRIMARY KEY (column1, column2...);

# DROP PRIMARY KEY
ALTER TABLE table_name DROP PRIMARY KEY;
```
