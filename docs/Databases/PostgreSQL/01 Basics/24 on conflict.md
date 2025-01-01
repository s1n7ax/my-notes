# On conflict

Gracefully handles conflict errors.

## Use case 1 - Do nothing on conflict

```sql
/* when the primary key or a unique value attempt to be added, conflict error will be thrown  */
INSERT INTO person (id, first_name, last_name, email, gender, country, bday)
VALUES (1001, 'srinesh', 'nisala', 'test@gmail.com', 'Male', 'Sri Lanka', '1993-11-16');

INSERT INTO person (id, first_name, last_name, email, gender, country, bday)
VALUES (1001, 'srinesh', 'nisala', 'test@gmail.com', 'Male', 'Sri Lanka', '1993-11-16');
/*
ERROR:  duplicate key value violates unique constraint "person_pkey"
DETAIL:  Key (id)=(1001) already exists
*/

/* To handle this gracefully, on conflict can be used */
INSERT INTO person (id, first_name, last_name, email, gender, country, bday)
VALUES (1001, 'srinesh', 'nisala', 'test@gmail.com', 'Male', 'Sri Lanka', '1993-11-16')
ON CONFLICT (id) DO NOTHING;
/*
INSERT 0 0
*/
```

## Use case 2

```sql
/* perform update action on conflict of some column */
INSERT INTO person (id, first_name, last_name, email, gender, country, bday)
VALUES (1001, 'srinesh', 'nisala', 'test@gmail.com', 'Male', 'Sri Lanka', '1993-11-16');

/* using on conflict, we can update an existing record instead of inserting a new record */
INSERT INTO person (id, first_name, last_name, email, gender, country, bday)
VALUES (1001, 'srinesh', 'nisala', 'testnew@gmail.com', 'Male', 'Sri Lanka', '1993-11-16')
ON CONFLICT (id) DO UPDATE SET email = EXCLUDED.email;
```
