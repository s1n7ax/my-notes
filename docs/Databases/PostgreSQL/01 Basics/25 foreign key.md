# Foreign key

Creates a reference to a other column

```sql
/* create a foreign keys when creating tables */

CREATE TABLE cars (
	id BIGSERIAL NOT NULL PRIMARY KEY,
	make VARCHAR(50) NOT NULL,
	model VARCHAR(50) NOT NULL,
	price MONEY NOT NULL
);

CREATE TABLE person (
	id BIGSERIAL NOT NULL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	email VARCHAR(50),
	gender VARCHAR(50) NOT NULL,
	country VARCHAR(50) NOT NULL,
	bday DATE NOT NULL,
	car_id BIGINT,

	FOREIGN KEY(car_id) REFERENCES cars(id)
);
```
