# Coalesce

Use the default value if the passed value/s is null

```sql

/*
coalesce will check the values from left to right
If the left value is null, and right value is not, the the right value will be used
*/
SELECT coalesce(null, null, 1, null)
/* 1 */

SELECT first_name, COALESCE(email, 'No Email') FROM person;
```
