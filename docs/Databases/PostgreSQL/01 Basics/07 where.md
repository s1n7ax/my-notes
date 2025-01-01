# Where clause

Where can be used to filter out the data using conditions

```sql
SELECT * FROM person WHERE country = 'China' AND gender = 'Male';
SELECT * FROM person WHERE ( country = 'China' OR country = 'Brazil' ) AND gender = 'Male';
SELECT * FROM person WHERE ( country = 'China' OR country = 'Brazil' ) AND email IS NOT NULL;
```
