## What is an integer in Python?

An **integer (`int`)** represents a whole number:
```
x = 42
y = -7
z = 0
```
In Python, `int` is a **built-in type**:
```
type(10)  # <class 'int'>
```

---
## The big Python superpower: unlimited size

Unlike many languages (C, Java, etc.), Python integers:

- **do not overflow**
    
- grow as large as memory allows
```
x = 10**100
print(x)
```
No wraparound. No silent bugs.

Under the hood, Python uses **arbitrary-precision arithmetic**.

---

## Creating integers

### From literals
```
a = 10
b = -3
```
From strings
```
int("123")     # 123
int("-42")     # -42
```
With different bases
```
int("1010", 2)    # binary → 10
int("ff", 16)     # hex → 255
```
Literals with bases
```
0b1010   # 10 (binary)
0o12     # 10 (octal)
0xA      # 10 (hex)
```

---
## Integer operations

### Arithmetic
```
5 + 2    # 7
5 - 2    # 3
5 * 2    # 10
5 ** 2   # 25
```
Division (important!)
```
5 / 2    # 2.5   → float
5 // 2   # 2     → integer (floor division)
```
Modulo
```
5 % 2    # 1
```
Modulo rule:
```
# a = 5
# b = 2

a == (a // b) * b + (a % b)  #output: True
```

---
### Negative numbers + floor division
```
-5 // 2   # -3
-5 % 2    # 1
```
Why?

- `//` always **rounds down**, not toward zero
    

This surprises a lot of people.

---
## Integers and booleans (Python quirk)

In Python:
```
True == 1    # True
False == 0  # True
```
Because:
```
issubclass(bool, int)  # True
```
So:
```
True + True   # 2
```
Useful sometimes. Dangerous if you forget.

---
## Immutability (very important)

Integers are **immutable**.
```
x = 10
y = x
x += 1
```
Result:
```
print(x)  #output: 11
print(y)  #output: 10
```
Python created a **new int object** for `11`.

---
## Object identity & small integer caching

Python caches small integers (usually `-5` to `256`):
```
a = 100
b = 100
a is b    # True
```
But:
```
a = 1000
b = 1000
a is b    # False (usually)
```
⚠️ Never rely on `is` for numeric comparison.  
Always use `==`.

---
## Performance characteristics
- Small ints → very fast
    
- Very large ints → slower (more memory, more math)
    

Example:
```
10**10      # fast
10**10000   # slower
```
Still safe. Just not free.

---
## Common integer-related bugs

❌ Using `/` when you want `//`  
❌ Assuming overflow exists  
❌ Using `is` instead of `==`  
❌ Forgetting negative floor division rules  
❌ Mixing ints with floats without noticing

---
## When ints auto-convert
```
5 + 2.0    # 7.0 (float)
```
Rule:

> Python promotes to the “wider” type.

---
## Useful integer functions
```
abs(-10)       # 10
pow(2, 10)     # 1024
divmod(5, 2)   # (2, 1)
```
`divmod(a, b)` gives:
```
(a // b, a % b)
```
