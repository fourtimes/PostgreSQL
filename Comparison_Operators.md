## Math Operators

**1. Are the equal values**
```bash
=
```
**2. Greater than**
```bash
>
```
**3. Less than**
```bash
<
```
**4. Greater than or equal to**
```bash
>=
```
**5. Less than or equal to**
```bash
<=
```
**6. Values not equal to**
```bash
<> and !=
```
**7. Values between two other values**
```bash
BETWEEN
```
**8. The value not present in a list?**
```bash
NOT IN
```
**9. Present value in a list**
```bash
IN
```
### Examples:

1. SELECT name, area FROM cities WHERE area `BETWEEN` 2000 AND 4000;
2. SELECT * FROM cities WHERE area `<>` 4000;
3. SELECT name, population / area AS population FROM cities WHERE `population / area > 6000`;
