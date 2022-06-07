## Intersect

|S.No.|Symbol|Details|
|-----|------|----------|
|1.|`UNION`|Join together the results of 2 queries and remove duplicate rows.|
|2.|`UNION ALL`|Join together the results of 2 queries.|
|3.|`INTERSECT`|find the rows common in the results of two queries. remove duplicates.|
|4.|`INTERSECT ALL`|find the rows common in the results of two queries.|
|5.|`EXCEPT`|find the rows that are present in first query but not second query. remove duplicates.|
|6.|`EXCEPT ALL`|find the rows that are present in first query but not second query.|
|7.|`DISTRINCT`|DISTINCT clause to remove duplicate rows from a result set returned by a query.|
|8.|`GREATEST`|Returns the greatest value from the list of expressions|
9.|`LEAST`|Returns the least from the list of expressions.|


### Examples

 ```bash
# union all
 SELECT * FROM  company
 UNION ALL
 SELECT * FROM photos;
 ```
 ```bash
 # intersect
 SELECT col_name
FROM A
INTERSECT
SELECT col_name
FROM B
ORDER BY sort_expression;
```
```bash
# except
SELECT supplier_id, supplier_name
FROM suppliers
WHERE supplier_id >= 59
EXCEPT
SELECT company_id, company_name
FROM companies
WHERE state = 'California'
ORDER BY 2;
```
```bash
# greatest
SELECT GREATEST(1, 10, 64); #64
```
```bash
# least
SELECT LEAST(1,2,3); #1
```
