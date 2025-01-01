# Extract values from date time

```sql
SELECT EXTRACT( YEAR FROM NOW() );
/*
 date_part
-----------
      2023
*/

SELECT EXTRACT( MONTH FROM NOW() );
/*
 date_part
-----------
        12
*/

/* DAW - day of the week */
SELECT EXTRACT( DOW FROM NOW() );
/*
 date_part
-----------
         4
*/
```
