# PostgreSQL basics

- Technically, object relational database
  - It can create custom data types to store objects with properties
  - It can inherit from other objects
- Supports python and C languages in addition to SQL
- Arrays, matrices, json & key value pairs can be defined

## PostgreSQL commands

### Running PostgreSQL with docker

```shell
docker run -d -e POSTGRES_PASSWORD=root -e POSTGRES_USER=root postgres
```
