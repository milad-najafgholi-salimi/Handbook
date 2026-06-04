## 1. What Is a Python Package?

A **package** in Python is a **directory (folder)** that contains:

- one or more **modules** (`.py` files)
    
- a special file called **`__init__.py`**
    

Packages help organize related code and make large programs easier to manage.

---
## 2. Basic Requirements to Make a Package

To create a package, you need:

1. A **folder** (this becomes the package name)
    
2. An **`__init__.py`** file inside the folder
    
3. One or more **module files** (`.py`)

---
## 3. Step-by-Step: Creating a Simple Package

### Step 1: Create the package folder
```
mypackage/
```
### Step 2: Add `__init__.py`
```
mypackage/
├── __init__.py
```
This file can be empty or contain initialization code.

### Step 3: Add module files
```
mypackage/
├── __init__.py
├── module1.py
├── module2.py
```

---
## 4. Write Code Inside the Modules

### `module1.py`
```
def greet():
    return "Hello"
```
### `module2.py`
```
def farewell():
    return "Goodbye"
```

---
## 5. Use the Package in a Program

Create a Python file **outside** the package directory.
```
project/
├── mypackage/
│   ├── __init__.py
│   ├── module1.py
│   └── module2.py
└── main.py
```
### `main.py`
```
from mypackage.module1 import greet
from mypackage.module2 import farewell

print(greet())
print(farewell())
```

---
## 6. Using `__init__.py` to Simplify Imports

You can control what the package exposes.

### `mypackage/__init__.py`
```
from .module1 import greet
from .module2 import farewell
```
Now you can write:
```
from mypackage import greet, farewell
```

---
## 7. Relative Imports Inside a Package

When modules inside the same package import each other, use **relative imports**.
```
from .module1 import greet
```
- `.` → current package
    
- `..` → parent package

---
## 8. Creating Sub-Packages (Optional)

A package can contain other packages.
```
mypackage/
├── __init__.py
├── basic/
│   ├── __init__.py
│   ├── moduleA.py
│
├── advanced/
│   ├── __init__.py
│   ├── moduleB.py
```
Usage:
```
from mypackage.basic.moduleA import functionA
```

---
## 9. Making the Package Installable (Optional / Advanced)

To install your package using `pip`, add a setup file.

### Structure
```
mypackage_project/
├── mypackage/
│   ├── __init__.py
│
├── setup.py
```
### `setup.py`
```
from setuptools import setup, find_packages

setup(
    name="mypackage",
    version="1.0",
    packages=find_packages(),
)
```
Install locally:
```
pip install .
```

---
## 10. Common Mistakes to Avoid

- Forgetting `__init__.py`
    
- Running modules inside the package directly
    
- Incorrect relative imports
    
- Naming your package the same as a built-in module
    

---

## 11. Short Exam-Ready Answer

> A Python package is created by making a directory containing an `__init__.py` file and one or more module files. The directory name becomes the package name. Modules inside the package can be imported using dot notation, and `__init__.py` controls package initialization and exposed members.