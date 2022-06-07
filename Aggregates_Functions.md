## Aggregates Functions
Like most other relational database products, PostgreSQL supports aggregate functions. An aggregate function computes a **single result from multiple input rows**. PostgreSQL provides all standard SQL’s aggregate functions as follows:

---
**1. Returns the number of values in a group of values**
```bash
COUNT()
```
**2. Returns the sum of a group of numbers**
```bash
SUM()
```
**3. Returns the average of a group of numbers**
```bash
AVG()
```
**4. Returns the minimum value from a group of numbers**
```bash
MIN()
```
**5. Returns the maximum value from a group of numbers**
```bash
MAX()
```
### Examples:

1. SELECT `MAX(id)` FROM comments;
2. SELECT user_id, `MIN(id)` FROM comments GROUP BY user_id;
