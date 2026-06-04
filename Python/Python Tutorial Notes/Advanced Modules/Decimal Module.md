The **`decimal`** module in Python provides support for **decimal floating-point arithmetic** with more precision and control than the built-in `float` type.

It is especially useful in **financial, accounting, and high-precision applications** where exact decimal representation is required.

---
## 1) Why Not Just Use `float`?

Python’s `float` uses **binary floating-point arithmetic** (IEEE 754). Some decimal numbers cannot be represented exactly in binary.

Example:
```
print(0.1 + 0.2)

#Output:
0.30000000000000004
```
This happens because `0.1` and `0.2` cannot be stored exactly in binary.

---
## 2) What Does `decimal` Fix?

The `decimal` module:

- Stores numbers as **base-10 (decimal)**
    
- Provides **exact representation**
    
- Allows control over:
    
    - Precision
        
    - Rounding
        
    - Exponent limits
        
    - Error handling
        

---

## 3) Basic Usage

### Importing
```
from decimal import Decimal
```
### Creating Decimal Numbers

⚠️ Always pass strings, not floats!
```
from decimal import Decimal

a = Decimal('0.1')
b = Decimal('0.2')

print(a + b)

#Output:
0.3
```
#### Why strings?
```
Decimal(0.1)   # BAD
```
This converts the _already inaccurate float_ into a Decimal.

Correct:
```
Decimal('0.1')  # GOOD
```

---
## 4) Setting Precision

The decimal module allows you to control precision using a **context**.
```
from decimal import getcontext

getcontext().prec = 4

a = Decimal('1') / Decimal('7')
print(a)

#Output:
0.1429
```
Without setting precision, default is usually 28 digits.

---

## 5) Rounding

You can control rounding behavior.
```
from decimal import ROUND_HALF_UP, getcontext

getcontext().rounding = ROUND_HALF_UP

num = Decimal('2.3456')
print(num.quantize(Decimal('0.01')))

#Output:
2.35
```
### Common Rounding Modes

- `ROUND_HALF_UP`
    
- `ROUND_HALF_DOWN`
    
- `ROUND_HALF_EVEN` (banker's rounding)
    
- `ROUND_UP`
    
- `ROUND_DOWN`
    
- `ROUND_CEILING`
    
- `ROUND_FLOOR`
    

---

## 6) The `quantize()` Method

Used to round to a fixed number of decimal places.
```
Decimal('5.6789').quantize(Decimal('0.01'))
```
Result:
```
5.68
```
This is heavily used in financial calculations.

---

## 7) Context and Error Handling

You can control how errors are handled.
```
from decimal import getcontext, DivisionByZero

getcontext().traps[DivisionByZero] = True
```
Now division by zero raises an exception instead of returning `Infinity`.

---

## 8) Comparing float vs Decimal
| Feature                      | float   | Decimal |
| ---------------------------- | ------- | ------- |
| Speed                        | Fast    | Slower  |
| Precision                    | Binary  | Decimal |
| Financial Use                | ❌ Risky | ✅ Safe  |
| Configurable Precision       | ❌       | ✅       |
| Exact Decimal Representation | ❌       | ✅       |

---
## 9) When Should You Use Decimal?

Use `decimal` when:

- Working with **money**
    
- Performing **financial/accounting calculations**
    
- Needing **exact rounding control**
    
- Avoiding floating-point representation errors
    

Do NOT use it when:

- You need high-performance scientific computing → use `float` or `numpy`
    
- You don’t care about tiny rounding differences
    

---

## 10) Example: Financial Calculation
```
from decimal import Decimal, getcontext, ROUND_HALF_UP

getcontext().rounding = ROUND_HALF_UP

price = Decimal('19.99')
tax_rate = Decimal('0.075')

tax = (price * tax_rate).quantize(Decimal('0.01'))
total = price + tax

print("Tax:", tax)
print("Total:", total)

#Output:
Tax: 1.50
Total: 21.49
```
This produces reliable financial results.

---

## 11) Advanced: Local Context

Temporary precision change:
```
from decimal import localcontext

with localcontext() as ctx:
    ctx.prec = 2
    print(Decimal('1') / Decimal('7'))

print(Decimal('1') / Decimal('7'))  # Back to default
```

---
## 12) Internal Representation

Decimal numbers are stored as:
```
sign × coefficient × 10^exponent
```
This allows exact decimal storage.

---

## Summary

The `decimal` module:

- Fixes floating-point accuracy problems
    
- Allows configurable precision
    
- Provides full rounding control
    
- Is ideal for financial applications
    
- Is slower but more precise than float