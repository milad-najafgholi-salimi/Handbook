`HAVING` keyword MUST BE before order by; So literally, right after group by.

Example:
```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth HAVING COUNT(*) > 5 ORDER BY country_of_birth;
```

The output will be countries with at least 6 people in our table.
