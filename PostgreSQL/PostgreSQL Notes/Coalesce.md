The `COALESCE` keyword allows us to have a default value in case the first one is not present. 

### Syntax:
```
COALESCE(value1, value2, value3, ...)
```

Example:
```
SELECT COALESCE(NULL, NULL, 'Hello', 'World');
-- Returns: 'Hello'

SELECT COALESCE(NULL, 5, 10);
-- Returns: 5

SELECT COALESCE('Apple', NULL, 'Orange');
-- Returns: 'Apple'
```

---
Example:
```
SELECT COALESCE(email, "Email not provided") FROM person;
```
