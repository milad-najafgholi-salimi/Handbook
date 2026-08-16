### Syntax:
```
CREATE TABLE table_name (
	Column name + data type + constraints if any	
)
```

Example:
```
CREATE TABLE person (
	id int,
	first_name VARCHAR(50), # 50 here means maximum can have 50 characters
	last_name VARCHAR(50),
	gender VARCHAR(6),
	date_of_birth DATE);
```

#### To see table or tables:
```
\d      # stands for 'describe'
```

To see table's data:
```
\d table_name
```
Example:
```
\d person
```

### Creating Tables with Constraints
#### Pay Attention:
NOT good:
```
CREATE TABLE person (
	id int,
	first_name VARCHAR(50),
	last_name VARCHAR(50),
	gender VARCHAR(5),
	date_of_birth DATE );
```

Good:
```
CREATE TABLE person (
	id BIGSERIAL NOT NULL PRIMARY KEY,
	first_name VARCHAR(50) NOT NULL,
	last_name VARCHAR(50) NOT NULL,
	gender VARCHAR(5) NOT NULL,
	date_of_birth DATE NOT NULL );
```
