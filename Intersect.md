## Intersect

|S.No.|Symbol|Details|
|-----|------|----------|
|1.|`UNION`|Join together the results of 2 queries and remove duplicate rows.|
|2.|`UNION ALL`|Join together the results of 2 queries.|
|3.|`INTERSECT`|find the rows common in the results of two queries. remove duplicates.|
|4.|`INTERSECT ALL`|find the rows common in the results of two queries.|
|5.|`EXCEPT`|find the rows that are present in first query but not second query. remove duplicates.|
|6.|`EXCEPT ALL`|find the rows that are present in first query but not second query.|

### Example

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
