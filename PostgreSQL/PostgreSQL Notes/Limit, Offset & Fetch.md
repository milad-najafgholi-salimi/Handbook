Example for `LIMIT`:
```
SELECT * FROM person LIMIT 10;
```
Which means show only first 10 records.

Example for `OFFSET`:
```
SELECT * FROM person OFFSET 5 LIMIT 5;
```

`OFFSET 5` stands for show records after first 5 records;
`LIMIT 5` stands for show only 5 records as the output;

Example for `FETCH`:
```
SELECT * FROM person OFFSET 5 FETCH FIRST 5 ROW ONLY;
```
It's obvious what that means.
