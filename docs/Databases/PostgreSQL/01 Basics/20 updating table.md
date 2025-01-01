# Updating table 

```sql
/* remove the primary key */
ALTER TABLE person DROP CONSTRAINT person_pkey;

/* add primary key */
ALTER TABLE person ADD PRIMARY KEY (id);
```
