The **`math` module** in Python provides access to **mathematical functions and constants** for working with numbers (especially floats). It is part of Python’s standard library and is widely used in scientific computing, engineering, data analysis, simulations, and education.

---
## 1. Why We Need the `math` Module

Basic operators like:
```
+  -  *  /  **  %
```
are built into Python.

But advanced mathematical operations like:

- Square root
    
- Logarithms
    
- Trigonometric functions
    
- Factorials
    
- Constants like π and e
    

are provided by the `math` module.

---

## 2. Importing the Module
```
import math
```
or:
```
from math import sqrt, pi
```

---
## 3. Mathematical Constants

The module provides important constants:

| Constant   | Meaning                   |
| ---------- | ------------------------- |
| `math.pi`  | π (3.14159...)            |
| `math.e`   | Euler’s number (2.718...) |
| `math.tau` | 2π                        |
| `math.inf` | Infinity                  |
| `math.nan` | Not a number              |
### Example:
```
import math

print(math.pi)
print(math.e)
```

---
## 4. Rounding and Absolute Functions

### Absolute Value
```
math.fabs(-5.3)
```
Note: `abs()` is built-in, but `math.fabs()` always returns a float.
### Ceiling and Floor
```
math.ceil(4.2)   # 5
math.floor(4.9)  # 4
```
### Truncate
```
math.trunc(4.9)  # 4
```

---
## 5. Power and Logarithmic Functions

### Square Root
```
math.sqrt(16)  # 4.0
```
### Power
```
math.pow(2, 3)  # 8.0
```
Note:

- `math.pow()` returns float
    
- `2 ** 3` may return int
    
### Logarithms
```
math.log(10)        # Natural log (base e)
math.log10(100)     # Base 10 log
math.log2(8)        # Base 2 log
math.log(8, 2)      # Log base 2
```
### Exponential
```
math.exp(2)  # e^2
```

---
## 6. Trigonometric Functions

⚠ Important: All trigonometric functions use **radians**, NOT degrees.
### Sine, Cosine, Tangent
```
math.sin(math.pi/2)
math.cos(0)
math.tan(math.pi/4)
```
### Convert Degrees ↔ Radians
```
math.radians(90)
math.degrees(math.pi/2)
```
### Inverse Trig Functions
```
math.asin(1)
math.acos(1)
math.atan(1)
```

---
## 7. Hyperbolic Functions
```
math.sinh(x)
math.cosh(x)
math.tanh(x)
```
Less common in beginner courses but important in advanced math.

---

## 8. Factorial and Combinatorics

### Factorial
```
math.factorial(5)  # 120
```
### GCD (Greatest Common Divisor)
```
math.gcd(24, 36)  # 12
```
### LCM (Python 3.9+)
```
math.lcm(4, 6)  # 12
```
### Combinations and Permutations (Python 3.8+)
```
math.comb(5, 2)  # 10
math.perm(5, 2)  # 20
```
Very useful for probability and statistics.

---
## 9. Special Functions

### Check Infinity
```
math.isinf(math.inf)
```
### Check NaN
```
math.isnan(math.nan)
```
### Check Finite
```
math.isfinite(10)
```

---
## 10. Difference Between `math` and Built-in Functions
|Built-in|math module|
|---|---|
|`abs()`|`math.fabs()`|
|`pow()`|`math.pow()`|
|`round()`|No direct equivalent|
|`**`|`math.pow()`|
## 11. Important Notes for Exams

1. All trig functions use radians.
    
2. `math.sqrt()` only works for non-negative numbers.
    
    - For complex numbers → use `cmath`
        
3. `math.factorial()` only accepts integers.
    
4. `math.pow()` returns float.
    

---

## 12. Real-World Example

### Area of a Circle
```
import math

radius = 5
area = math.pi * radius**2
print(area)
```
### Compound Interest Formula
```
import math

P = 1000
r = 0.05
t = 3

A = P * math.exp(r * t)
print(A)
```

---
## 13. Summary

The `math` module provides:

✔ Mathematical constants  
✔ Rounding functions  
✔ Power and logarithmic functions  
✔ Trigonometric functions  
✔ Factorials and combinatorics  
✔ Special number checks

It is essential for:

- Engineering
    
- Physics
    
- Data science
    
- Mathematics education
    
- Competitive exams