# Tables

## Show all the existing tables

## Create a tables

```sql
# CREATE TABLE <name> (
#     <column name> <data type> <constraints if any>
# );

CREATE TABLE public.person (
    id INT NOT NULL PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    age INT NOT NULL,
    bday DATE NOT NULL
);
```

## List tables

`\d` to list table, views and sequences
`\dt` to list only tables

```
test=# \d
             List of relations
 Schema |     Name      |   Type   | Owner
--------+---------------+----------+-------
 public | person        | table    | root
 public | person_id_seq | sequence | root
(2 rows)
```

## Get table details

```
test=# \d person
                                   Table "public.person"
 Column |         Type          | Collation | Nullable |              Default
--------+-----------------------+-----------+----------+------------------------------------
 id     | bigint                |           | not null | nextval('person_id_seq'::regclass)
 name   | character varying(50) |           | not null |
 age    | integer               |           | not null |
 bday   | date                  |           | not null |
Indexes:
    "person_pkey" PRIMARY KEY, btree (id)
```

## Delete tables

```sql
# DROP TABLE <name>;
DROP TABLE person;
```

## Insert data into table

```
# INSERT INTO <table name> (
#     <column name>
# ) VALUES (
#     'value'
# );

INSERT INTO person (
    name,
    age,
    bday
) VALUES (
    's1n7ax',
    30,
    DATE '1993-11-16'
);
```
