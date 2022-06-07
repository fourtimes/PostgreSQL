**Sub-queries**
```bash
 SELECT name, price 
 FROM products 
 WHERE price > (
      SELECT MAX(price) FROM products WHERE department='toys'
);
```
```bash
SELECT * FROM (SELECT MAX(price) FROM products) AS p;
```
**subquery in a from**
```bash
FROM (
  SELECT user_id, COUNT(*) AS order_count 
  FROM orders
  GROUP BY user_id
) AS p;
```
**subquery JOIN clause**
```bash
SELECT first_name 
FROM users
JOIN(
  SELECT user_id, FROM orders WHERE product_id=3
) AS o
ON o.user_id = users.id
```
**subquery with WHERE clause**
```bash
SELECT id
FROM orders
WHERE product_id IN (
  SELECT id FROM products WHERE price / weight > 50
);
```
