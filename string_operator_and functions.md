## String Operator and Functions

**1. Join a two strings**
```bash
|| 

[OR]

CONCAT()
```
**2. Returns a lower case**
```bash
LOWER()
```
**3. Returns a upper case**
```bash
UPPER()
```
**4. Returns a number of characters in a string**
```bash
LENGTH()
```
**5. The GREATEST function returns the greatest value in a list of expressions.**
```bash
GREATEST( expr_1, expr_2, ... expr_n )
```
---

**Examples:**

`SELECT name || ' , '|| country AS combine FROM cities;`

**Output**
|combine|
|---|
|ashli, india|
