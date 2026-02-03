## 1. **Arithmetic Operators**

These are used to perform basic mathematical operations.

| Operator | Description         | Example       |
| -------- | ------------------- | ------------- |
| `+`      | Addition            | `3 + 2 = 5`   |
| `-`      | Subtraction         | `5 - 2 = 3`   |
| `*`      | Multiplication      | `3 * 2 = 6`   |
| `/`      | Division            | `7 / 2 = 3.5` |
| `//`     | Floor division      | `7 // 2 = 3`  |
| `%`      | Modulus (remainder) | `7 % 2 = 1`   |
| `**`     | Exponentiation      | `2 ** 3 = 8`  |
- // (floor division) returns the quotient of the division rounded down to the nearest integer.

- % gives the remainder when one number is divided by another.

---
## 2. **Comparison Operators**

These are used to compare two values or variables.

| Operator | Description              | Example                 |
| -------- | ------------------------ | ----------------------- |
| `==`     | Equal to                 | `5 == 5` returns `True` |
| `!=`     | Not equal to             | `5 != 3` returns `True` |
| `>`      | Greater than             | `5 > 3` returns `True`  |
| `<`      | Less than                | `3 < 5` returns `True`  |
| `>=`     | Greater than or equal to | `5 >= 5` returns `True` |
| `<=`     | Less than or equal to    | `3 <= 5` returns `True` |
- These operators return a Boolean value: `True` or `False`.

---
## 3. **Logical Operators**

Used to combine conditional statements.

| Operator | Description                          | Example                          |
| -------- | ------------------------------------ | -------------------------------- |
| `and`    | True if both operands are true       | `True and False` returns `False` |
| `or`     | True if at least one operand is true | `True or False` returns `True`   |
| `not`    | Inverts the Boolean value            | `not True` returns `False`       |

---
## 4. Assignment Operators

Used to assign values to variables.

| Operator | Description             | Example                              |
| -------- | ----------------------- | ------------------------------------ |
| `=`      | Simple assignment       | `x = 5`                              |
| `+=`     | Add and assign          | `x += 3` (equivalent to `x = x + 3`) |
| `-=`     | Subtract and assign     | `x -= 2` (equivalent to `x = x - 2`) |
| `*=`     | Multiply and assign     | `x *= 4` (equivalent to `x = x * 4`) |
| `/=`     | Divide and assign       | `x /= 2` (equivalent to `x = x / 2`) |
| `//=`    | Floor divide and assign | `x //= 2`                            |
| `%=`     | Modulus and assign      | `x %= 3`                             |
| `**=`    | Exponentiate and assign | `x **= 2`                            |

---
## 5. **Identity Operators**

Used to compare the memory locations of two objects.

| Operator | Description                                                         | Example      |
| -------- | ------------------------------------------------------------------- | ------------ |
| `is`     | Returns `True` if both variables point to the same object in memory | `a is b`     |
| `is not` | Returns `True` if both variables do not point to the same object    | `a is not b` |
Example:
```
a = [1, 2, 3]
b = a
print(a is b)  # True because they point to the same list object
```

---
## 6. **Membership Operators**

Used to check if a value is present in a sequence (like a list, string, or tuple).

| Operator | Description                                              | Example                    |
| -------- | -------------------------------------------------------- | -------------------------- |
| `in`     | Returns `True` if a value exists in the sequence         | `5 in [1, 2, 3, 4, 5]`     |
| `not in` | Returns `True` if a value does not exist in the sequence | `6 not in [1, 2, 3, 4, 5]` |

---
## 7. **Bitwise Operators**

Used for **bit-level operations** (working with individual bits of a number).

| Operator | Description | Example                                                |
| -------- | ----------- | ------------------------------------------------------ |
| `&`      | Bitwise AND | `5 & 3 = 1` (binary `0101 & 0011 = 0001`)              |
| `        | `           | Bitwise OR                                             |
| `^`      | Bitwise XOR | `5 ^ 3 = 6` (binary `0101 ^ 0011 = 0110`)              |
| `~`      | Bitwise NOT | `~5 = -6` (binary `~0101 = 1010`, in two’s complement) |
| `<<`     | Left shift  | `5 << 1 = 10` (binary `0101 << 1 = 1010`)              |
| `>>`     | Right shift | `5 >> 1 = 2` (binary `0101 >> 1 = 0010`)               |

---
## 8. **Ternary (Conditional) Operator**

This is a shorthand for an `if-else` condition.
```
x = 5
result = "Even" if x % 2 == 0 else "Odd"
```
If `x % 2 == 0`, `result` is "Even". Otherwise, it’s "Odd".

---
## Summary of Most Common Operators

- **Arithmetic:** `+`, `-`, `*`, `/`, `//`, `%`, `**`
    
- **Comparison:** `==`, `!=`, `>`, `<`, `>=`, `<=`
    
- **Logical:** `and`, `or`, `not`
    
- **Assignment:** `=`, `+=`, `-=`, `*=`, `/=`, `//=`, `%=` etc.
    
- **Identity:** `is`, `is not`
    
- **Membership:** `in`, `not in`
    
- **Bitwise:** `&`, `|`, `^`, `~`, `<<`, `>>`
    
- **Ternary:** `condition_if_true if condition else condition_if_false`