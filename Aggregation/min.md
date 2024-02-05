---
layout: default
title: Min
parent: Aggregation
---

# The `MIN()` function
The `MIN()` function returns the smallest value in the set of values.

## Syntax
```
SELECT MIN(column)
FROM table;
```

## Examples
Consider the following table.

**purchase:**
| product | unit_price | quantity |
| ------- | ----- | -------- |
| Bagel | 3 | 20 |
| Bagel | 1.5 | 20 |
| Banana | 0.5 | 50 |
| Banana | 2 | 10 |
| Banana | 4 | 10 | 

Let's say we want to find the smallest unit price.
```
SELECT MIN(unit_price)
FROM purchase;
```
| min |
| --- |
| 0.5 |

We can also find the smallest sale as follows.
```
SELECT MIN(unit_price * quantity)
FROM purchase;
```
| min |
| --- |
| 20 |

The `MIN()` function can be used with [GROUP BY](group-by.html) to retrieve the minimum value for each group.
```
SELECT product, MIN(unit_price)
FROM purchase
GROUP BY product;
```
| product | min |
| ------- | --- |
| Bagel | 1.5 |
| Banana | 0.5 |

We may want to find the tuple which represents the smallest sale (i.e. the smallest `unit_price * quantity`). Assume we are interested in finding the entire tuple (or the product name). We can use a subquery combines with `MIN()` to achieve this.
```
SELECT *
FROM purchase
WHERE unit_price * quantity = (
    SELECT MIN(unit_price * quantity)
    FROM purchase;
);
```
| product | price | quantity |
| ------- | ----- | -------- |
| Banana | 2 | 10 |