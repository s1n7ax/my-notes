# Wildcards

```sql
SELECT * FROM person WHERE email LIKE '%.edu';
SELECT * FROM person WHERE email LIKE '%@google.%';
SELECT * FROM person WHERE email LIKE '%@___.%'; /* domain only 3 characters */
SELECT * FROM person WHERE country LIKE 'P%';
SELECT * FROM person WHERE country ILIKE 'p%'; /* ILIKE ignore the case */
```
