Example:
```
SELECT * FROM person WHERE email LIKE '%.com';
```
Example:
```
SELECT * FROM person WHERE email LIKE '%@bloomberg.com';
```
Example:
```
SELECT * FROM person WHERE email LIKE '%@google.%';
```

---
Example:
```
SELECT * FROM person WHERE email LIKE '___o@%';
```

`___` stands fro exactly 3 places.

---
`ILIKE` ignores case sensitive.
Example:
```
SELECT * FROM person WHERE country_of_birth ILIKE 'p%';
```

Same as:
```
SELECT * FROM person WHERE country_of_birth LIKE 'P%';
```
