Example:
```
SELECT NOW() - INTERVAL '10 YEARS';

# output: 2016-07-15 08:15:32.917833+04:30
```

```
SELECT NOW() - INTERVAL '10 MONTHS';

# output: 2025-09-15 08:17:05.553041+03:30
```

```
SELECT NOW() - INTERVAL '10 DAYS';

# output: 2026-07-05 08:17:18.354145+03:30
```

---
Also adding is the same:
```
SELECT NOW() + INTERVAL '1 YEAR';

# output: 2027-07-15 08:18:36.386866+03:30
```
