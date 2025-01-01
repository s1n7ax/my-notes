# Group by

```sql
/* get the number of people in each country */
SELECT country, COUNT(*) FROM person GROUP BY country;

/* get the number of people in each coutry but have less than 5 people */
SELECT country, COUNT(*) FROM person GROUP BY country HAVING COUNT(*) < 5;
```
