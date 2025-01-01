# Left join

Left join takes all the records in left table and matching records from right table

```sql
/* all the rows in the person table will be retrieved */
SELECT * FROM person
LEFT JOIN cars ON person.car_id = cars.id;
```
