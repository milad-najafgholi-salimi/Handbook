Error handling in Python is the set of tools and patterns you use to **detect, manage, and respond to runtime errors** (exceptions) so your program doesn’t crash unexpectedly and can fail gracefully.

---
## 1. What is an Error (Exception) in Python?

An **exception** is an event that occurs during program execution that disrupts the normal flow of the program.

Common examples:

- Dividing by zero
    
- Accessing a missing dictionary key
    
- Opening a file that doesn’t exist
    
- Passing the wrong type to a function

Example:
```
x = 10 / 0
```
This raises:
```
ZeroDivisionError: division by zero
```
Without handling, Python stops the program immediately.

---
## 2. The `try` / `except` Block

The core of Python error handling is the `try-except` structure.

### Basic Syntax
```
try:
    # code that might raise an error
except ErrorType:
    # code that runs if the error occurs
```
### Example
```
try:
    number = int("abc")
except ValueError:
    print("Conversion failed!")
```
**How it works:**

- Python runs the `try` block
    
- If an exception occurs, execution jumps to `except`
    
- If no exception occurs, `except` is skipped

---
## 3. Handling Multiple Exceptions

You can handle different errors in different ways.
```
try:
    x = int(input("Enter a number: "))
    result = 10 / x
except ValueError:
    print("That was not a number.")
except ZeroDivisionError:
    print("You cannot divide by zero.")
```
### Grouping Exceptions
```
except (ValueError, ZeroDivisionError):
    print("Invalid input.")
```

---
## 4. The `else` Clause

`else` runs **only if no exception occurred**.
```
try:
    x = int(input("Enter a number: "))
except ValueError:
    print("Invalid input.")
else:
    print("You entered:", x)
```
**Why use `else`?**

- Keeps success logic separate from error logic
    
- Makes code easier to read and reason about

---
## 5. The `finally` Clause

`finally` **always runs**, whether an exception occurred or not.
```
try:
    file = open("data.txt")
    content = file.read()
except FileNotFoundError:
    print("File not found.")
finally:
    file.close()
```
Typical uses:

- Closing files
    
- Releasing resources
    
- Cleaning up connections
    

⚠️ Note: If `file` might not exist, use safer patterns like `with`.

---
## 6. Using `with` (Context Managers)

Instead of `try-finally`, Python provides **context managers**.
```
with open("data.txt") as file:
    content = file.read()
```
Advantages:

- Automatically handles cleanup
    
- Cleaner and safer than manual `finally`
    

---

## 7. Raising Exceptions (`raise`)

You can **manually raise exceptions** to signal errors.
```
age = -5
if age < 0:
    raise ValueError("Age cannot be negative")
```
Use this when:

- Validating function inputs
    
- Enforcing business rules
    
- Creating clear failure points
    

---

## 8. Custom Exceptions

You can define your own exception types.
```
class InvalidAgeError(Exception):
    pass

def set_age(age):
    if age < 0:
        raise InvalidAgeError("Age must be positive")
```
Benefits:

- More meaningful error handling
    
- Easier debugging
    
- Cleaner exception separation in large projects
    

---

## 9. Catching All Exceptions (Be Careful!)
```
try:
    risky_code()
except Exception as e:
    print("Error:", e)
```
⚠️ **Avoid this unless necessary**

- Can hide bugs
    
- Makes debugging harder
    

❌ Never do:
```
except:
    pass
```
This silently ignores all errors — very dangerous.

---
## 10. Common Built-in Exceptions
| Exception           | Description               |
| ------------------- | ------------------------- |
| `TypeError`         | Wrong data type           |
| `ValueError`        | Correct type, wrong value |
| `IndexError`        | Invalid list index        |
| `KeyError`          | Missing dictionary key    |
| `FileNotFoundError` | File doesn’t exist        |
| `ZeroDivisionError` | Division by zero          |
| `ImportError`       | Module import failed      |

---
## 11. Best Practices for Error Handling

✔ Catch **specific exceptions**, not all  
✔ Keep `try` blocks **small**  
✔ Use `else` for success logic  
✔ Use `finally` or `with` for cleanup  
✔ Raise exceptions when something is logically wrong  
✔ Write clear error messages

### Good Example
```
def divide(a, b):
    if b == 0:
        raise ValueError("b must not be zero")
    return a / b
```

---
## 12. Error Handling vs Debugging

- **Error handling**: Planned, controlled responses to expected failures
    
- **Debugging**: Fixing unexpected bugs in code
    

You handle _expected_ problems; you debug _unexpected_ ones.