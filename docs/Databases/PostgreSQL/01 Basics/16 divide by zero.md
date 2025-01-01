# Divide by zero

When a number is divided by zero, PostgreSQL throws following error

```
test=# select 10/0;
ERROR:  division by zero
```

To make sure, this will not happen, `NULLIF` can be used.

```sql
/* when a number is divided by NULL, the result will be NULL */
SELECT 10 / NULL;
/*
?column?
----------

(1 row)
*/

/* NULLIF returns NULL when the first and the second parameters are equal */
SELECT NULLIF(1, 2);
/*
nullif
--------
      1
(1 row)
*/

SELECT NULLIF(1, 1);
/*
nullif
--------

(1 row)
*/

/* So, following make sure that the column returns NULL if divided by zero */
SELECT <something>/NULLIF(<column>, 0)
```
