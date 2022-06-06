## Aggregates Functions

**1. Returns the number of values in a group of values**
```bash
COUNT()
```
**2. Finds the sum of a group of numbers**
```bash
SUM()
```
**3. Finds the average of a group of numbers**
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
2. SELECT user_id, `MAX(id)` FROM comments GROUP BY user_id;
