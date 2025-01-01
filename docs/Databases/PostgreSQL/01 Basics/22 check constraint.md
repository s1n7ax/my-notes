# Check constraint

- check constraint allows us to insert value that passes the check

```sql
ALTER TABLE person
ADD CONSTRAINT check_gender
CHECK (gender IN ('Genderqueer', 'Bigender', 'Genderfluid', 'Male', 'Polygender', 'Non-binary', 'Female', 'Agender'));


/*
When tried to insert a value other than the listed, following error will be thrown

ERROR:  new row for relation "person" violates check constraint "check_gender"
DETAIL:  Failing row contains (1, asotn, rosnto, arsitn@rsotn.com, Femalee, United States, 2007-12-13).
*/
```
