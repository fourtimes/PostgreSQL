### POSTGRESQL
---
```bash
# CREATE DATABASE syntax:
CREATE DATABASE database_name;

# List the databases:
\l

# Enter into the specified database syntax:
\c database_name;

# CREATE TABLE syntax:
CREATE TABLE table_name(
   column1 datatype,
   column2 datatype,
   column3 datatype,
   .....
   columnN datatype,
   PRIMARY KEY( one or more columns )
);

# List all the tables in specified database:
 \d

# Describe the specified tables details:
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

# select the values in specified tables
SELECT * FROM table_name;

SELECT column1, column2, columnN FROM table_name;

# WHERE Condition
SELECT column1, column2, columnN
FROM table_name
WHERE [search_condition]
ex:
---
SELECT * FROM COMPANY WHERE AGE >= 25 OR SALARY >= 65000;

```
