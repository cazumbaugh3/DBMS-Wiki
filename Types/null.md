---
layout: default
title: NULL
---

# NULL

Null is not technically a type, but indicates the absense of a value; that is, the value is not known. This can occur for a large variety of reasons. The schema of the table can place a constraint on whether an attibute is nullable or not. If the value must be non-null, an error will be generated if the value is not supplied (or if it is supplied as null). Because `NULL` is unknown, it is neither true nor false. As a result, operations on `NULL` result in an unknown result. For example, the expression `x / 4 * NULL` will result in `NULL`. With binary logic, the result will depend on the operators used. Binary logic can be thought of as follows. Assuming a and b are boolean values with `TRUE = 1`, `FALSE = 0`, and `NULL = 0.5`

* `A AND B = MIN(A, B)`
* `A OR B = MAX(A, B)`
* `NOT(A) = 1 - A`

For example, consider the following simple predicates:

* `TRUE AND FALSE = MIN(1, 0) = 0 = FALSE`
* `TRUE OR FALSE = MAX(1, 0) = 1 = TRUE`
* `TRUE AND NULL = MIN(1, 0.5) = 0.5 = NULL`
* `FALSE AND NULL = MIN(0, 0.5) = 0 = FALSE`
* `TRUE OR NULL = MAX(1, 0.5) = 1 = TRUE`
* `FALSE OR NULL = MAX(0, 0.5) = 0.5 = NULL`
* `NOT(NULL) = 1 - 0.5 = 0.5 = NULL`

In the above examples it can be observed that the truth value of an expression involving `NULL` depends on both the subjects and the operator. `TRUE AND NULL` results in an unknown value while `FALSE AND NULL` results in `FALSE`. On the other hand, `TRUE OR NULL` results in `TRUE` while `FALSE OR NULL` results in an unknown value. This difference can be explained by the method these comparisons are done and the fact that `NULL` is *between* `TRUE` and `FALSE`.

## Ternary vs. binary logic
Null uses ternary logic: the value (or predicate) is either true (1), false (0), or unknown (0.5). However, SQL uses binary logic when determining whether to return a tuple or not. If the tuple returns true for the given condition it is returned, otherwise it is not. As a result, a comparison resulting in `NULL` will not be returned.

## Null is not a value
`NULL` is not a value- it indicates the absense of a value. Therefore, a given value **cannot** *equal* `NULL`. It can be null or not be null, but it cannot be equal to null. As a result, the following will result in an empty result set. This is because the test `attribute = NULL` is unknown, and because it is not true, the tuple will not be returned.

```
SELECT column(s)
FROM table
WHERE attribute = null;
``` 

To filter data where an attribute is or is not null, the following must be used.

```
SELECT column(s)
FROM table
WHERE attribute IS [NOT] NULL;
```