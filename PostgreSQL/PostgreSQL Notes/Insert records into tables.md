### Syntax:
```
INSERT INTO table_name (..., ..., ...)
VALUES (..., ..., ...);
```

For example:
```
INSERT INTO person (
	first_name,
	last_name,
	gender,
	date_of_birth)
VALUES ('Milad', 'Salimi', 'MALE', DATE '2003-07-05');
```

**NOTE:** `\dt` command, shows only tables.

To see all records from a table:
```
SELECT * FROM table_name;
```

For example:
```
SELECT first_name, last_name FROM person;
```
