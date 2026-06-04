In Python, **`__name__`** is a **special built-in variable** that plays an important role in **modules and packages**, especially for controlling **how code is executed or imported**.

---
## 1. What is `__name__`?

Every Python file (module) has a built-in variable called **`__name__`**.

- When a file is **run directly**,
```
__name__ == "__main__"
```
When a file is **imported**,
```
__name__ == "module_name"
```

---
## 2. `__name__` in a Simple Module

### Example: `demo.py`
```
print(__name__)
```
### Run directly:
```
python demo.py
```
Output:
```
__main__
```
### Import it:
```
import demo
```
Output:
```
demo
```

> In general packages use only for importing but with `__name__` variable, it can be run directly.
---
## 3. Why `__name__ == "__main__"` is Used

It allows a file to:

- run test code when executed directly
    
- avoid running that code when imported
    

### Example:
```
def greet():
    print("Hello")

if __name__ == "__main__":
    greet()
```
- Runs `greet()` when file is executed
    
- Does **not** run `greet()` when imported

---
## 4. `__name__` in Packages

Now let’s focus on packages.
### Package structure:
```
mypackage/
├── __init__.py
├── module1.py
├── module2.py
```

---
## 5. `__name__` Inside Package Modules
Inside `module1.py`
```
print(__name__)
```
If you run:
```
import mypackage.module1
```
Output:
```
mypackage.module1
```
So:

- `__name__` becomes the **full dotted path**
    
- Not just the filename

---
## 6. `__name__` Inside `__init__.py`
mypackage/`__init__.py`
```
print(__name__)
```
When you run:
```
import mypackage
```
Output:
```
mypackage
```
So:
- `__name__` equals the **package name**
    
- `__init__.py` represents the package itself

---
## 7. Running a Module Inside a Package Directly

If you run:
```
python mypackage/module1.py
```
Then:
```
__name__ == "__main__"
```
⚠️ This often causes **import errors** because the package context is lost.

---
## 8. Correct Way: Run as a Module
Use:
```
python -m mypackage.module1
```
Now:
```
__name__ == "mypackage.module1"
```
✔ Package imports work correctly  
✔ Relative imports work properly

---
## 9. `__name__` and Relative Imports

Relative imports depend on `__name__`.

Example inside a package:
```
from .module2 import func
```
This works only if:

- `__name__` is **not** `"__main__"`
    

That’s why relative imports fail when you run files directly.

---
## 10. Summary Table
| Situation                  | `__name__` value   |
| -------------------------- | ------------------ |
| Script run directly        | `"__main__"`       |
| Imported module            | `"module_name"`    |
| Imported package           | `"package_name"`   |
| Imported module in package | `"package.module"` |
| `__init__.py`              | `"package"`        |

---
## 11. Exam-Style Definition

> `__name__` is a special built-in variable that stores the name of the current module or package. When a file is executed directly, `__name__` is set to `"__main__"`, and when it is imported, it is set to the module or package name. It is commonly used to control execution of code in modules and packages.