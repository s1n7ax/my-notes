# Unique constraint

```sql
/* when creating a table */
CREATE TABLE person (
    first_name VARCHAR(50) NOT NULL,
    last_name VARCHAR(50) NOT NULL,
    email VARCHAR(50) NOT NULL,
    CONSTRAINT unique_email_address UNIQUE (email)
);

/* updating the table to add unique columns */
ALTER TABLE person ADD CONSTRAINT unique_email_address UNIQUE (email);
```
