## What are data types in Python?

A **data type** tells Python:

- what kind of data a value is
    
- what you can do with it
    
- how it’s stored and behaves
    

Python is **dynamically typed**, meaning:
```
x = 5        # int
x = "hi"     # now it's str
```
No type declaration needed — Python figures it out at runtime.

---
## Core built-in data types (the ones you _must_ know)

### 1. `int` — Integers

Whole numbers:
```
a = 10
b = -3
```
Properties:

- arbitrary precision (no overflow)
    
- supports math ops: `+ - * // % **`
```
10 // 3   # 3
10 % 3    # 1
```

---
### 2. `float` — Floating-point numbers

Decimals:
```
x = 3.14
y = 0.1
```
⚠️ Floating-point precision issue:
```
0.1 + 0.2 == 0.3   # False
```
Use `decimal.Decimal` if precision matters.

---
## The problem: floating-point precision

### Using `float` (default in Python)
```
a = 0.1
b = 0.2

print(a + b)
print(a + b == 0.3)
```
### Output:
```
0.30000000000000004
False
```
Why? Because **floats are stored in binary**, and `0.1` and `0.2` cannot be represented exactly in base-2.

This is **not a Python bug** — it’s how computers work.
## The solution: `decimal.Decimal`

When **precision matters** (money, measurements, scores), use `Decimal`.

### Correct way
```
from decimal import Decimal

a = Decimal("0.1")
b = Decimal("0.2")

print(a + b)
print(a + b == Decimal("0.3"))
```
### Output:
```
0.3
True
```
✅ Exact  
✅ Predictable  
✅ Safe for financial / sensitive calculations

---
## ⚠️ Important rule with `Decimal`

**Always pass strings**, not floats:
```
Decimal(0.1)      # ❌ WRONG
Decimal("0.1")    # ✅ CORRECT
```
Why?
```
Decimal(0.1)
# Decimal('0.1000000000000000055511151231')
```
Because the float error already happened.

#### Real-world example: money
❌ Using float (dangerous)
```
price = 0.1
total = price * 3
print(total)
```
Output:
```
0.30000000000000004
```
Now imagine invoices, balances, taxes… nope.

✅ Using Decimal (correct)
```
from decimal import Decimal

price = Decimal("0.1")
total = price * 3
print(total)
```
Output:
```
0.3
```

#### Controlling precision (advanced but useful)
```
from decimal import Decimal, getcontext

getcontext().prec = 4

print(Decimal("1") / Decimal("3"))
```
Output:
```
0.3333
```
You control the math — not the other way around.

---
### 3. `complex`

Used in math/science:
```
z = 2 + 3j
```
Most people rarely need this.

---
### 4. `bool` — Boolean

True / False:
```
is_ready = True
```
Important:
```
bool(0)        # False
bool("")       # False
bool([])       # False
```
Everything else is `True`.

---
## Text type

### 5. `str` — Strings

Text data:
```
name = "Ali"
```
Strings are:

- immutable
    
- iterable
    
- Unicode
```
name[0]      # 'A'
name.upper()
```
Immutability:
```
name[0] = "a"   # ❌ error
```

---
## Collection types (very important)

### 6. `list`

Ordered, mutable collection:
```
items = [1, 2, 3]
items.append(4)
```
- allows duplicates
    
- mixed types allowed
    
- mutable

---
### 7. `tuple`

Ordered, immutable:
```
point = (3, 4)
```
Used when:

- data shouldn’t change
    
- as dict keys

---
### 8. `set`

Unordered, unique elements:
```
nums = {1, 2, 3}
nums.add(2)   # no effect
```
Great for:

- membership tests
    
- removing duplicates

---
### 9. `dict`

Key–value pairs:
```
user = {
    "name": "Sara",
    "age": 25
}
```
- keys must be hashable
    
- values can be anything
    
- extremely common in real code

---
## Special types

### 10. `NoneType`

Represents “no value”:
```
result = None
```
Common use:

- default arguments
    
- placeholders
    
- missing data

---
## Type conversion (casting)
```
int("10")       # 10
float("3.14")   # 3.14
str(100)        # "100"
list("abc")     # ['a','b','c']
```

---
## Checking types
```
type(x)
isinstance(x, int)
```
Prefer `isinstance`.

---
## Mutability (this is _huge_ in Python)

### Immutable

- `int`
    
- `float`
    
- `bool`
    
- `str`
    
- `tuple`
    

### Mutable

- `list`
    
- `dict`
    
- `set`
    

Example pitfall:
```
a = [1, 2]
b = a
b.append(3)
print(a)   # [1, 2, 3]
```

---
## Python-specific truthiness

These are **False**:

- `0`
    
- `""`
    
- `[]`
    
- `{}`
    
- `set()`
    
- `None`
    

Everything else is True.

---

## Type hints (modern Python)

Python doesn’t require types, but you _should_ use hints:
```
def greet(name: str) -> str:
    return f"Hello {name}"
```
Benefits:

- readability
    
- editor support
    
- fewer bugs