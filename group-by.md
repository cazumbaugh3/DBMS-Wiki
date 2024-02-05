---
layout: default
title: GROUP BY
parent: Aggregation
---

# The `GROUP BY` statement
The `GROUP BY` statement groups tuples with the same value for a given attribute, and is typically used with [aggregate functions](aggregation.html). Queries using `GROUP BY` do not need `DISTINCT` because duplicate values are removed when the data is collapsed into a group. If `GROUP BY` is used, the attributes used in the `SELECT` clause is limited (see below). In general, filtering on attributes should be done in the `WHERE` clause and not the [HAVING](having.html) clause. Only filtering done on grouped aggregates should by done in the `HAVING` clause. Executing a condition in the `HAVING` clause in which the attribute is not in `GROUP BY` or an aggregate will result in an error.


The following attributes may be used in the `SELECT` clause with `GROUP BY`:
* Attributes listed in `GROUP BY`
* Any aggregates


Attributes not listed in `GROUP BY` may **<u>NOT</u>** appear in `SELECT`. When `GROUP BY` is used, the query execution order is as follows:
1. Compute the `FROM` and `WHERE` clause
2. Group the tuples
3. Compute the `HAVING` clause (filter on groups)
4. Select the attributes

## Syntax
```
SELECT column(s)
FROM table
WHERE condition
GROUP BY column(s)
HAVING condition;
```

## Examples
Consider the following tables.

**store:**

| sid | sname |
| --- | ----- |
| 1 | Electronics Store |
| 2 | University Store |

**product:**

| pid | pname | price | store |
| --- | ----- | ----- | ----- |
| 1 | Powergizmo | 248 | 1 |
| 2 | SingleTouch | 149 | 1 |
| 3 | MultiTouch | 203 | 2 |
| 4 | Incrediblegizmo | 248 | 1 |
| 5 | Doublepowergizmo | 556 | 2 |

Find the maximum price at each store.
```
SELECT store, MAX(price) AS max_price
FROM store
JOIN product ON product.store = store.sid
GROUP BY store;
```

| store | max_price |
| ----- | --------- |
| 2 | 556 |
| 1 | 248 |

`GROUP BY` can be used to simplify nested queries. Take for example, the below query, which finds the total quantity for all sales over $1 by product.
```
SELECT DISTINCT x.product, (
                            SELECT SUM(y.quantity)
                            FROM purchase y
                            WHERE x.product = y.product
                                  AND price > 1
                           ) AS TotalSales
FROM purchase x
WHERE price > 1;
```

Not only is this a correlated subquery, it is not clear as to what they query seeks to answer. The same query can be re-written as follows.
```
SELECT product, sum(quantity)
FROM purchase
WHERE price > 1
GROUP BY product;
```