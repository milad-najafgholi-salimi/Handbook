In Python, **modules** and **packages** are ways to organize code so it’s reusable, readable, and easier to maintain.

---
## 1. What is a Module?

A **module** is simply a **single Python file** (`.py`) that contains:

- functions
    
- classes
    
- variables
    
- executable code
    

### Example: a module

**math_utils.py**
```
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

PI = 3.14159
```
This file is a **module** named `math_utils`.

### Importing a module
```
import math_utils

print(math_utils.add(3, 5))
print(math_utils.PI)
```
### Importing specific items
```
from math_utils import add, PI

print(add(2, 4))
print(PI)
```
### Renaming a module (alias)
```
import math_utils as mu

print(mu.add(1, 2))
```

---
## 2. Built-in Modules

Python comes with many **built-in modules**, such as:

- `math`
    
- `random`
    
- `datetime`
    
- `os`
    
- `sys`
    

Example:
```
import math

print(math.sqrt(16))
print(math.pi)
```
You don’t need to install these—they come with Python.

---
## 3. What is a Package?

A **package** is a **folder (directory)** that contains **multiple modules** (and possibly sub-packages).

It allows you to organize related modules together.

### Basic package structure
```
my_package/
│
├── __init__.py
├── math_utils.py
├── string_utils.py
```
- `my_package` → package
    
- `math_utils.py` → module
    
- `string_utils.py` → module
    
- `__init__.py` → tells Python this folder is a package  
    (required in older Python versions; still commonly used)

---
## 4. Importing from a Package

### Import a module from a package
```
import my_package.math_utils

print(my_package.math_utils.add(5, 3))
```
Import directly from the package
```
from my_package.math_utils import add

print(add(5, 3))
```
### Using aliases with packages
```
from my_package import math_utils as mu

print(mu.subtract(10, 4))
```

---
## 5. The `__init__.py` File

The `__init__.py` file runs **when the package is imported**.

### Example: `__init__.py`
```
from .math_utils import add
```
Now you can do:
```
from my_package import add

print(add(2, 3))
```
This controls **what the package exposes** to users.

---
## 6. Sub-packages (Packages inside Packages)

Packages can contain other packages.
```
school/
│
├── __init__.py
├── students/
│   ├── __init__.py
│   ├── records.py
│
├── teachers/
│   ├── __init__.py
│   ├── schedules.py
```
Usage:
```
from school.students.records import get_student
```

---
## 7. How Python Finds Modules and Packages

Python searches for modules in this order:

1. Current directory
    
2. Directories listed in `PYTHONPATH`
    
3. Standard library directories
    

You can inspect this using:
```
import sys
print(sys.path)
```

---
## 8. Modules vs Packages (Quick Comparison)
| Feature    | Module                        | Package                 |
| ---------- | ----------------------------- | ----------------------- |
| What it is | A single `.py` file           | A directory             |
| Contains   | Functions, classes, variables | Multiple modules        |
| Purpose    | Small unit of code            | Organize large projects |
| Example    | `utils.py`                    | `utils/`                |

---
## 9. Real-World Analogy 

- **Module** → One book
    
- **Package** → A bookshelf containing related books
    
- **Library** → Python standard library or third-party packages (like `numpy`)
    

---

## 10. Why Modules and Packages Matter

They help you:

- Avoid duplicate code
    
- Keep projects organized
    
- Collaborate with others
    
- Scale from small scripts to large applications