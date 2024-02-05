---
layout: default
title: COUNT
parent: Aggregation
---

# The COUNT() function
The `COUNT()` function returns the number of rows in the query. Depending on the column passed to the function, `NULL` may be ignored.

## Syntax
```
SELECT COUNT(column)
FROM table;
```

## Example

The below query will return the number of rows in the specified table.
```
SELECT COUNT(*)
FROM table;
```

To retrieve the number of values in a given column, the below query can be used. If a tuple contains a `NULL` value for the column, that tuple is omitted from the count. However, in the below example, duplicates will be counted.
```
SELECT COUNT(column)
FROM table;
```

If duplicate counts should be ignored (i.e. duplicates are only counted once), `DISTINCT` must be specified before the column name.
```
SELECT COUNT(DISTINCT column)
FROM table;
```