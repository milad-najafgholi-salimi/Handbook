Example:
```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth; 
```
The output will be look like:
```
Japan 23
Iran 6
Bangladesh 12
.
.
.
```

Example:
```
SELECT country_of_birth, COUNT(*) FROM person GROUP BY country_of_birth ORDER BY country_of_birth;
```
