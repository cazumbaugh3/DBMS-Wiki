---
layout: default
title: WHERE
parent: Filtering
---

# The `WHERE` clause

The `WHERE` clause is used to filter the results of a given query. This can be used to return only tuples matching a given criteria, and several criteria can be combined using [boolean operators](Boolean%20Operators/boolean-operators.html). During execution of the query, filtering will be done early to reduce the number of tuples on the sets being operated on. This makes operations such as [joins](../Joins/joins.html) more efficient, as the join occurs on smaller sets.

## Syntax
```
SELECT column(s)
FROM table
WHERE condition(s);
```

## Examples
Consider the following table

**products:**

| id | name | price |
| -- | ---- | ----- |
| 1 | Widget | 10 |
| 2 | Phone | 100 |
| 3 | Computer | 1,000 |
| 4 | Tablet | 500 |

Let's say we wish to retrieve all products with a price less than 500.
```

SELECT name
FROM products
WHERE price < 500;
```

| name |
| ---- |
| Widget |
| Phone |

We can combine filtering conditions using boolean operators. For example, let's retrieve all products with a price less than 500 that are greater than 50.
```
SELECT name
FROM products
WHERE price < 500 AND price > 50;
```

| name |
| ---- |
| Phone |

We can add subqueries to the where clause, though the result must be compatible with the filtering condition. For example, we may with to find the product(s) with the greatest price.
```
SELECT name
FROM products
WHERE price = (
	SELECT max(price)
	FROM products
);
```

| name |
| ---- |
| Computer |

This query can also be written as follows.
```
SELECT name
FROM products
WHERE price >= ALL (
	SELECT price
	FROM products
);
```

While an unrealistic example, the following query will result in an error as they types are incompatible.
```
SELECT name
FROM products
WHERE price = (
	SELECT name
	FROM test
);
```