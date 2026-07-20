`NULLIF` returns **NULL** if two expressions are equal, otherwise it returns the first expression. It's essentially a conditional NULL generator.

### Syntax:
```
NULLIF(expression1, expression2)
```

Example:
```
SELECT NULLIF(5, 5);
-- Returns: NULL (because they're equal)

SELECT NULLIF(5, 10);
-- Returns: 5 (because they're different)

SELECT NULLIF('apple', 'apple');
-- Returns: NULL

SELECT NULLIF('apple', 'orange');
-- Returns: 'apple'
```

Example:
```
-- Convert empty strings to NULL
SELECT 
    username,
    NULLIF(email, '') as email
FROM users;
-- Empty emails become NULL, actual emails stay as-is
```

#### A usage
Example:
```
SELECT 10 / 0;

# output: ERROR:  division by zero
```

To avoid getting an error:
```
SELECT 10 / NULLIF(0,0);

# output: Nothing
```

Look at the example below; The second zero is the default value:
```
SELECT COALESCE(10 / NULLIF(0, 0), 0);

# output: 0
```
