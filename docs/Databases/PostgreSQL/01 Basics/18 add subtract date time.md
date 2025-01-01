# Add Subtract Date Time

```sql
SELECT NOW();
/* 2023-12-07 15:34:53.487828+00 */

SELECT NOW() + INTERVAL '1 YEAR';
/* 2024-12-07 15:36:28.317258+00 */

/* Following returns a TIMESTAMP. To get a DATE value, this result has to be cast to DATE */
SELECT NOW()::DATE - INTERVAL '10 MONTHS';
/* 2023-02-07 00:00:00 */

SELECT (NOW()::DATE - INTERVAL '10 MONTHS')::DATE;
/* 2023-02-07 */
```
