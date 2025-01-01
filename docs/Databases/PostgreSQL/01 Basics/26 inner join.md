# Inner join

Selects common rows in two tables

```sql
/* retrives all the details in person & cars tables for people who has cars */
SELECT * FROM person
JOIN CARS ON PERSON.CAR_ID = CARS.ID;


/* selected columns */
SELECT person.first_name, cars.make FROM person
JOIN CARS ON PERSON.CAR_ID = CARS.ID;
```
