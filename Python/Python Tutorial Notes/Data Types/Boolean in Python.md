A **Boolean** is a data type that can have **only two possible values**:
```
True
False
```
In Python, the Boolean type is called `bool`.

Example:
```
is_student = True
is_raining = False
```

---
## The `bool` type

You can check the type:
```
type(True)    # <class 'bool'>
type(False)   # <class 'bool'>
```
⚠️ Note:

- `True` and `False` **must start with a capital letter**
    
- `true` or `false` will cause an error

---
## Boolean expressions
A Boolean expression is any expression that evaluates to True or False.
### a. Comparison operators
| Operator | Meaning          | Example  | Result  |
| -------- | ---------------- | -------- | ------- |
| `==`     | equal to         | `5 == 5` | `True`  |
| `!=`     | not equal to     | `5 != 3` | `True`  |
| `>`      | greater than     | `5 > 3`  | `True`  |
| `<`      | less than        | `5 < 3`  | `False` |
| `>=`     | greater or equal | `5 >= 5` | `True`  |
| `<=`     | less or equal    | `5 <= 4` | `False` |
Example:
```
age = 18
age >= 18    # True
```

---
## Logical operators

Logical operators combine or modify Boolean values.

| Operator | Meaning                      | Example          | Result  |
| -------- | ---------------------------- | ---------------- | ------- |
| `and`    | True if both are True        | `True and False` | `False` |
| `or`     | True if at least one is True | `True or False`  | `True`  |
| `not`    | Reverses the value           | `not True`       | `False` |
Example:
```
age = 20
has_id = True

age >= 18 and has_id    # True
```

---
## Booleans in `if` statements

Booleans control program flow.
```
age = 16

if age >= 18:
    print("Adult")
else:
    print("Minor")
```
The condition inside `if` **must evaluate to a Boolean**.

---
## Truthy and Falsy values (VERY IMPORTANT)

In Python, many values behave like `True` or `False` even if they are not Boolean.

### Falsy values:

These evaluate to `False`:
```
False
0
0.0
""
[]
()
{}
None
```
### Truthy values:

Everything else is considered `True`.

Example:
```
if "":
    print("Won't run")

if [1, 2, 3]:
    print("This will run")
```

---
## Using `bool()` function

The `bool()` function converts a value to `True` or `False`.
```
bool(0)        # False
bool(10)       # True
bool("")       # False
bool("hi")     # True
bool([])       # False
```

---
## Boolean values in arithmetic

In Python:

- `True` behaves like `1`
    
- `False` behaves like `0`
```
True + True      # 2
True + False     # 1
False * 10       # 0
```
This is because `bool` is a **subclass of `int`**.

---
## Boolean comparisons vs assignment (COMMON ERROR)

❌ Wrong:
```
if x = 5:
    ...
```
✔ Correct:
```
if x == 5:
    ...
```
- `=` assigns a value
    
- `==` compares values

---
## Boolean operators short-circuiting

Python uses **short-circuit evaluation**:
```
False and something()   # something() is NOT called
True or something()    # something() is NOT called
```
This improves efficiency and avoids errors.

---
## Identity vs equality (advanced but important)
```
a = True
b = True

a == b    # True (same value)
a is b    # True (same object)
```
Usually:

- Use `==` to compare values
    
- Use `is` for identity checks (like `None`)
```
if x is None:
    ...
```

---
## One-line exam definition (memorize)

> **A Boolean in Python is a data type with two values, `True` and `False`, used to represent logical conditions.**

---
## Common mistakes students make

- Writing `true` instead of `True`
    
- Confusing `=` with `==`
    
- Forgetting that empty collections are `False`
    
- Overusing `is` instead of `==`