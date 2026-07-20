### Syntax:
```
SELECT * FROM table_name WHERE condition = something(somthings);
```

For example:
```
SELECT * FROM person WHERE gender = "Female";
```

Using `And`:
```
SELECT * FROM person WHERE gender = "Male" AND (country_of_birth = "Poland") OR (country_of_birth = "Iran");
```
