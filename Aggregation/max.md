---
layout: default
title: Max
parent: Aggregation
---

# The `MAX()` function
The `MAX()` function returns the maximum of the set of values. It is similar in use as the [MIN()](min.html) function.

## Syntax
```
SELECT MAX(column)
FROM table;
```

## Example
Consider the following table.

**purchase:**
| product | unit_price | quantity |
| ------- | ----- | -------- |
| Bagel | 3 | 20 |
| Bagel | 1.5 | 20 |
| Banana | 0.5 | 50 |
| Banana | 2 | 10 |
| Banana | 4 | 10 | 

Let's say we want to find the value of the maximum sale.
```
SELECT MAX(unit_price * quantity)
FROM purchase;
```
| max |
| --- |
| 60 |

Suppose we want to return the tuple with the maximum sale. We can accomplish this by using `MAX()` in a subquery.
```
SELECT *
FROM purchase
WHERE unit_price * quantity = (
    SELECT MAX(price * quantity)
    FROM purchase
);
```
| product | unit_price | quantity |
| ------- | ----- | -------- |
| Bagel | 3 | 20 |

We can combine `MAX()` with [[GROUP BY|GROUP BY]] to retrieve the maximum over a particular grouping.
```
SELECT product, MAX(unit_price * quantity)
FROM purchase
GROUP BY product;
```
| product | max |
| ------- | --- |
| Bagel | 60 |
| Banana | 40 |