---
layout: default
title: INTERSECT
parent: Set Operators
---

# Intersect

Intersect takes the intersection (A $\cap$ B) of sets A and B. That is, it will return all of the tuples that are present in both A and B. Similar to [UNION](union.html), `INTERSECT` removes duplicates by default but the behavior is different from that of `UNION`. By definition, the intersection selects values that are present in *both* sets A and B, and both will appear in the result set. However, if this match is duplicated the duplicate pairs will be removed by default. If `INTERSECT ALL` is specified, duplicate matches will be preserved.

## Syntax
```
(Subquery A)
INTERSECT [ALL]
(Subquery B)
```
