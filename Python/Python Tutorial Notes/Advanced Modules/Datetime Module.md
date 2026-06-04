The **`datetime` module** in Python is used to work with **dates and times**. It allows you to create, manipulate, format, and calculate with dates and times in a clean and structured way.

---
## 1. Why We Need `datetime`

Python has:

- `time` module → low-level time (timestamps, system time)
    
- `datetime` module → high-level, object-oriented date & time handling
    

The `datetime` module is more powerful and commonly used in real-world applications like:

- Logging
    
- Scheduling systems
    
- Data analysis
    
- Web development
    
- Time difference calculations
    

---

## 2. Main Classes in `datetime`

The module contains several important classes:

|Class|Description|
|---|---|
|`date`|Stores year, month, day|
|`time`|Stores hour, minute, second|
|`datetime`|Combines date and time|
|`timedelta`|Difference between dates/times|
|`tzinfo`|Time zone base class|
|`timezone`|Fixed offset time zone|

To use it:
```
import datetime
```
Or more commonly:
```
from datetime import date, time, datetime, timedelta
```

---
## 3. The `date` Class

Represents a date (year, month, day).

### Creating a Date
```
from datetime import date

d = date(2026, 2, 11)
print(d)

#Output:
2026-02-11
```
### Accessing Attributes
```
print(d.year)
print(d.month)
print(d.day)
```
### Today’s Date
```
today = date.today()
print(today)
```

---
## 4. The `time` Class

### Represents time (hour, minute, second, microsecond).
```
from datetime import time

t = time(14, 30, 45)
print(t)
```
### Access attributes:
```
print(t.hour)
print(t.minute)
print(t.second)
```

---
## 5. The `datetime` Class (Most Important)

This combines both date and time.
```
from datetime import datetime

dt = datetime(2026, 2, 11, 14, 30, 45)
print(dt)

#Output:
2026-02-11 14:30:45
```

### Current Date & Time
```
now = datetime.now()
print(now)
```
### UTC time:
```
utc_now = datetime.utcnow()
print(utc_now)
```

---
## 6. Formatting Dates (`strftime`)

`strftime()` converts datetime into a formatted string.

Example:
```
now = datetime.now()
formatted = now.strftime("%d-%m-%Y %H:%M:%S")
print(formatted)
```
### Common Format Codes
| Code | Meaning           |
| ---- | ----------------- |
| `%Y` | Full year (2026)  |
| `%y` | Short year (26)   |
| `%m` | Month (01–12)     |
| `%d` | Day (01–31)       |
| `%H` | Hour (00–23)      |
| `%I` | Hour (01–12)      |
| `%M` | Minute            |
| `%S` | Second            |
| `%A` | Full weekday name |
| `%B` | Full month name   |
Example:
```
print(now.strftime("%A, %B %d, %Y"))
```

---
## 7. Parsing Strings (`strptime`)

`strptime()` converts a string → datetime object.
```
date_string = "11-02-2026"
dt = datetime.strptime(date_string, "%d-%m-%Y")
print(dt)
```
Very useful when reading:

- User input
    
- CSV files
    
- Databases
    
- APIs
    

---

## 8. `timedelta` (Date Arithmetic)

Used to calculate differences or add/subtract time.
```
from datetime import timedelta, datetime

today = datetime.now()
future = today + timedelta(days=7)
print(future)
```
### Supported Arguments
```
timedelta(
    days=,
    seconds=,
    minutes=,
    hours=,
    weeks=
)
```
### Difference Between Dates
```
d1 = datetime(2026, 2, 11)
d2 = datetime(2026, 2, 1)

difference = d1 - d2
print(difference)
print(difference.days)

#Output:
10 days, 0:00:00
10
```

---
## 9. Comparing Dates
```
d1 = datetime(2026, 2, 11)
d2 = datetime(2025, 2, 11)

print(d1 > d2)  # True
print(d1 == d2) # False
```
You can compare them using:

- `>`
    
- `<`
    
- `==`
    
- `!=`
    

---

## 10. Timestamps

Convert datetime → Unix timestamp:
```
now = datetime.now()
timestamp = now.timestamp()
print(timestamp)
```
Convert timestamp → datetime:
```
dt = datetime.fromtimestamp(timestamp)
print(dt)
```

---
## 11. Timezones (Basic)
```
from datetime import timezone

utc_time = datetime.now(timezone.utc)
print(utc_time)
```
For advanced timezone handling, Python 3.9+ provides:
```
from zoneinfo import ZoneInfo

dt = datetime.now(ZoneInfo("Asia/Kolkata"))
print(dt)
```

---
## 12. Common Real-World Use Cases

### ✔ Calculate Age
```
birth = date(2000, 5, 10)
today = date.today()

age = today.year - birth.year
print(age)
```
(Real calculation needs month/day adjustment.)

---

### ✔ Check if a Deadline Passed
```
deadline = datetime(2026, 3, 1)
if datetime.now() > deadline:
    print("Deadline passed")
```
### ✔ Add 30 Days to Current Date
```
new_date = datetime.now() + timedelta(days=30)
print(new_date)
```

---
## 13. Common Mistakes Students Make

1. Mixing `date` and `datetime`
    
2. Forgetting to import correctly
    
3. Using wrong format codes in `strptime`
    
4. Confusing `%m` (month) with `%M` (minute)
    
5. Ignoring time zones
    

---

## 14. Summary (Big Picture)

The `datetime` module allows you to:

- Create dates and times
    
- Get current date/time
    
- Format dates as strings
    
- Convert strings to dates
    
- Perform date arithmetic
    
- Compare dates
    
- Work with time zones
    

It is one of the most important built-in Python modules for real-world programming.