---
layout: default
title: UNION
parent: Set Operators
---

# Union
The `UNION` operator takes the union of two tables. That is, it return all values that exist in either of the two tables. By default, `UNION` removes duplicate values from the result set. Therefore, `DISTINCT` is not needed if `UNION` is used. If duplicate values are required, `UNION ALL` can be used to preserve them. Because `UNION ALL` does not need to sort the values to remove duplicates, it is a less expensive operation and can speed up the query if the tables being combined are large.

A requirement of using `UNION` is that the tables being combined are compatible. They must have the same number of columns, and the data types in each column must be compatible.

## Syntax
```
(subquery)
UNION [ALL]
(subquery);
```

## Examples

Consider the following tables.

**beer:**

| name |
| ---- |
| IPA |
| Lager |
| Sour |
| Stout |
| Double IPA |

**wine:**

| name |
| ---- |
| Cabernet Sauvignon |
| Chardonnay |
| Norton |
| Chambourcin |
| Sour |

(I don't think sour wines actually exist, but let's say they do for the sake of argument)

The union of these two tables would be as follows:
```
SELECT name
FROM beer
UNION
SELECT name
FROM wine;
```

| name |
| ---- |
| IPA |
| Lager |
| Sour |
| Stout |
| Double IPA |
| Cabernet Sauvignon |
| Chardonnay |
| Norton |
| Chambourcin |

Note that 'Sour' only appears once, despite being in both tables. If it should appear twice, `UNION ALL` must be used.
```
SELECT name
FROM beer
UNION ALL
SELECT name
FROM wine;
```

| name |
| ---- |
| IPA |
| Lager |
| Sour |
| Stout |
| Double IPA |
| Cabernet Sauvignon |
| Chardonnay |
| Norton |
| Chambourcin |
| Sour |