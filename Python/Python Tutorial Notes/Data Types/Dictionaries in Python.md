A **dictionary** (often called `dict`) is a data structure that stores data as **key–value pairs**.

Think of it like a **real dictionary**:

- **Key** → word
    
- **Value** → definition
    

Example:
```
student = {
    "name": "Milad",
    "age": 22,
    "grade": "A"
}
```

---
## Key properties of dictionaries

A dictionary is:

- **Ordered** (Python 3.7+) → keeps insertion order
    
- **Mutable** → can be changed after creation
    
- **Key-based** → access values using keys, not indexes
    
- **Keys must be unique**
    
- **Keys must be immutable (hashable)**

---
## Creating dictionaries

### a. Using curly braces `{ }`
```
person = {"name": "Milad", "age": 22}
```
### b. Using `dict()`
```
person = dict(name="Milad", age=22)
```
### c. Empty dictionary
```
empty = {}
```
⚠️ `{}` is always a **dictionary**, never a set.

---
## Accessing values

### a. Using square brackets
```
person["name"]   # 'Milad'
```
⚠️ Raises `KeyError` if key doesn’t exist.

### b. Using `.get()` (safer)
```
person.get("name")        # 'Milad'
person.get("height")     # None
person.get("height", 0)  # 0 (default value)
```

---
## Adding and updating items
```
person["height"] = 170      # add new key-value
person["age"] = 26          # update existing value
```

---
## Removing items
```
person.pop("age")        # removes and returns value
del person["height"]    # removes key-value pair
person.clear()          # removes everything
```

---
## Dictionary methods (very important)
```
student = {"name": "Milad", "age": 22, "grade": "A"}

student.keys()      # dict_keys(['name', 'age', 'grade'])
student.values()    # dict_values(['Milad', 22, 'A'])
student.items()     # dict_items([('name', 'Milad'), ...])
```

---
## Looping through dictionaries
### a. Loop through keys (default)
```
for key in student:
    print(key)
```
### b. Loop through values
```
for value in student.values():
    print(value)
```
### c. Loop through key–value pairs (most common)
```
for key, value in student.items():
    print(key, value)
```

---
## Checking membership
```
"name" in student     # True
20 in student         # False (checks keys, not values!)
```

---
## Dictionary comprehensions

Similar to list comprehensions, but for dictionaries.
```
squares = {x: x**2 for x in range(5)}
```
With condition:
```
evens = {x: x for x in range(10) if x % 2 == 0}
```

---
## Nested dictionaries

Dictionaries can contain other dictionaries.
```
school = {
    "student1": {"name": "Milad", "age": 22},
    "student2": {"name": "Mehrdad", "age": 23}
}

school["student1"]["name"]   # 'Milad'
```

---
## Keys: what is allowed and what is not (EXAM TRAP)

### ✅ Allowed keys (immutable / hashable)
```
"age", 10, (1, 2)
```
### ❌ Not allowed as keys
```
[1, 2], {1, 2}, {"a": 1}
```
Rule to remember:

> **Dictionary keys must be immutable (hashable).**

---
## Copying dictionaries (common mistake)

### Reference copy
```
a = {"x": 1}
b = a
b["x"] = 99
# a is now {'x': 99}
```
### Proper copy
```
b = a.copy()
```

---
## One-line exam definition (memorize)

> **A dictionary is a mutable, ordered collection of key–value pairs accessed by keys.**