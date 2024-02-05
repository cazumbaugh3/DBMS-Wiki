---
layout: default
title: AVG
parent: Aggregation
---
# The `AVG()` function
The `AVG()` function calculates the average of a set of values. The values passed to `AVG()` must make sense to average.

## Syntax
```
SELECT AVG(column)
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

Let's say we want to get the average quantity of all purchases.
```
SELECT AVG(quantity)
FROM purchase;
```

| avg |
| --- |
| 22.00 |

Similarly, we can retrieve the average total price as follows.
```
SELECT AVG(unit_price * quantity)
FROM purchase;
```

| avg |
| --- |
| 35 |

The `AVG()` function can be used with [GROUP BY](group-by.html) to retrieve the aggregate values for each group. For example, find the average total sales price for each product.
```
SELECT product, AVG(unit_price * quantity)
FROM purchase
GROUP BY product;
```

| product | avg |
| ------- | --- |
| Bagel | 45 |
| Banana | 28.33 |