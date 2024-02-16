---
layout: default
title: MIN
parent: Aggregation
---

# The `SUM()` function
The `SUM()` function will return the sum of the set of values given to it as a single value. Note that the values passed to `SUM()` should make sense to sum (i.e. they must be numbers).

## Syntax
```
SELECT SUM(column)
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

Let's say we want to find the total sales (i.e. the sum of the `unit_price` * `quantity` for all purchases). We can use the following query.
```
SELECT SUM(unit_price * quantity)
FROM purchase;
```
This query will result in the following result:
| sum |
| --- |
| 175 |

We may also be interested in finding the total sales for a given product (ex. Bagel).
```
SELECT SUM(unit_price * quantity)
FROM purchase
WHERE product = 'Bagel';
```
This query returns the following result:
| sum |
| --- |
| 90 |

For example, we may want to find the total quantity of all sales where the unit price is > $1.
```
SELECT SUM(quantity)
FROM purchase
WHERE unit_price > 1;
```
| sum |
| --- |
| 60 |

The `SUM()` function can also be combined with [GROUP BY](group-by.html) to retrieve the aggregate for each group. For example, find the total quantity for all sales where the unit price is > $1, by product.
```
SELECT product, SUM(quantity)
FROM purchase
WHERE unit_price > 1
GROUP BY product;
```
| product | sum |
| ------- | --- |
| Bagel | 40 |
| Banana | 20 |