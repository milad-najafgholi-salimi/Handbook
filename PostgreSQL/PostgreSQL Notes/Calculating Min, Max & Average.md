Example - Max and Min and Average:
```
SELECT MAX(price) FROM car;
```

```
SELECT MIN(price) FROM car;
```

```
SELECT AVG(price) FROM car;
```

To round the output number, simply use:
```
SELECT ROUND(AVG(price)) FROM car;
```

Example:
```
SELECT make, model, MIN(price) FROM car GROUP BY make, model;
```