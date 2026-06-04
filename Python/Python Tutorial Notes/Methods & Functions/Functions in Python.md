In Python, a **function** is a **reusable block of code** that performs a specific task. Functions help you organize programs, avoid repetition, and make code easier to read and maintain.

---
## 1. What Is a Function?

A **function** is a named block of code that:

- Runs only when it is **called**
    
- Can **accept input** (parameters)
    
- Can **return output**
    

Example:
```
def greet():
    print("Hello!")
```
Calling the function:
```
greet()

#Output:
Hello!
```

---
## 2. Why Use Functions?

Functions help to:

- Reduce code duplication
    
- Improve readability
    
- Make debugging easier
    
- Break large programs into smaller parts
    
- Reuse code across programs

---
## 3. Defining a Function

Syntax:
```
def function_name(parameters):
    # function body
    return value
```
Example:
```
def add(a, b):
    return a + b
```
Call:
```
result = add(3, 5)
print(result)
```

---
## 4. Function Parameters and Arguments

### Parameters vs Arguments

- **Parameters** → variables in the function definition
    
- **Arguments** → values passed to the function when calling it

```
def multiply(x, y):  # parameters
    return x * y

multiply(4, 6)       # arguments
```

---
## 5. Types of Function Arguments

### 1. Positional Arguments
```
def power(base, exp):
    return base ** exp

power(2, 3)
```
### 2. Keyword Arguments
```
power(exp=3, base=2)
```
### 3. Default Arguments
```
def greet(name="User"):
    print("Hello", name)

greet()
greet("Milad")

#Output:
Hello User
Hello Milad
```
### 4. Variable-Length Arguments

#### `*args` (multiple positional arguments)
```
def total(*numbers):
    return sum(numbers)
```
#### `**kwargs` (multiple keyword arguments)
```
def show_info(**data):
    print(data)
```

---
## 6. Return Statement

- Sends a value back to the caller
    
- Ends the function execution
```
def square(n):
    return n * n
```
A function can return:

- One value
    
- Multiple values (as a tuple)
```
def calc(a, b):
    return a + b, a - b

print(calc(3, 4))

#Output:
(7, -1)
```

---
## 7. Built-in Functions

Python provides many built-in functions:
```
len()
print()
type()
input()
range()
sum()
max()
min()
```
Example:
```
numbers = [1, 2, 3]
print(len(numbers))
```

---
## 8. User-Defined Functions

Functions created by the programmer.
```
def is_even(n):
    return n % 2 == 0
```

---
## 9. Anonymous (Lambda) Functions

Short, one-line functions.
```
square = lambda x: x * x
print(square(5))
```
Used when:

- A small function is needed temporarily
    
- Often with `map()`, `filter()`

---
## 10. Scope of Variables

### Local Scope
```
def test():
    x = 10  # local variable
```
### Global Scope
```
x = 5

def show():
    print(x)
```
Using `global` keyword:
```
def change():
    global x
    x = 20
```

---
## 11. Docstrings (Documentation)

Describe what a function does.
```
def add(a, b):
    """Returns the sum of two numbers"""
    return a + b
```
Access:
```
print(add.__doc__)
```
**Output:**
```
Returns the sum of two numbers
```

---
## 12. Function vs Method (Quick Comparison)
| Function        | Method                    |
| --------------- | ------------------------- |
| Independent     | Belongs to an object      |
| Called directly | Called using dot notation |
| `len(x)`        | `x.append()`              |

---
## 13. Summary

- Functions are reusable blocks of code
    
- Defined using `def`
    
- Can accept arguments and return values
    
- Types include:
    
    - Built-in
        
    - User-defined
        
    - Lambda (anonymous)
        
- Help make code modular and maintainable