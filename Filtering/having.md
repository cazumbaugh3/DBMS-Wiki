---
layout: default
title: HAVING
---

# The `HAVING` clause
The `HAVING` clause is used in conjunction with [GROUP BY](../Aggregation/group-by.html) to apply filtering on aggregate values. It should contain filtering <i>only</i> on the aggregate values, while `WHERE` should be used for filtering on an attribute.

## Syntax
```
SELECT column(s), aggregate(s)
FROM table
WHERE condition(s)
GROUP BY column(s)
HAVING condition(s);
``` 