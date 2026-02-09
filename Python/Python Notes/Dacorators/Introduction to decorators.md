Decorators are a **powerful Python feature** that let you **modify or extend the behavior of functions or methods without changing their source code**. They’re commonly used for logging, access control, timing, caching, and more.

---
## 1. Functions are first-class objects in Python

In Python, functions:

- Can be assigned to variables
    
- Can be passed as arguments
    
- Can be returned from other functions
```
def greet():
    return "Hello!"

say_hello = greet
print(say_hello())
```
This flexibility is what makes decorators possible.

---

## 2. Functions inside functions (closures)

A decorator is built on **nested functions**.
```
def outer():
    def inner():
        print("I'm inside!")
    inner()

outer()
```
Now let’s return the inner function instead:
```
def outer():
    def inner():
        print("I'm inside!")
    return inner

fn = outer()
fn()
```
Here, `inner` “remembers” the environment it was created in. This is called a **closure**.

---

## 3. The core idea of a decorator

A decorator is a function that:

1. Takes another function as input
    
2. Returns a new function that adds extra behavior
```
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper
```
Using it manually:
```
def say_hi():
    print("Hi!")

say_hi = my_decorator(say_hi)
say_hi()
```
**Output:**
```
Before function call
Hi!
After function call
```

---
## 4. The `@decorator` syntax (syntactic sugar)

Python provides a cleaner way to apply decorators:
```
def my_decorator(func):
    def wrapper():
        print("Before function call")
        func()
        print("After function call")
    return wrapper

@my_decorator
def say_hi():
    print("Hi!")
```
This is equivalent to:
```
say_hi = my_decorator(say_hi)
```

---
## 5. Decorators with arguments (`*args` and `**kwargs`)

Most real functions take arguments, so decorators must handle them:
```
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Before")
        result = func(*args, **kwargs)
        print("After")
        return result
    return wrapper
```
Example:
```
@my_decorator
def add(a, b):
    return a + b

print(add(3, 4))
```

---
## 6. Preserving function metadata (`functools.wraps`)

Decorators hide the original function’s name and docstring unless you preserve them.
```
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        return func(*args, **kwargs)
    return wrapper
```
Without `@wraps`, this happens:
```
print(add.__name__)  # wrapper
```
With `@wraps`:
```
print(add.__name__)  # add
```

---
## 7. Decorators with parameters

Sometimes **the decorator itself needs arguments**.
```
def repeat(times):
    def decorator(func):
        def wrapper(*args, **kwargs):
            for _ in range(times):
                func(*args, **kwargs)
        return wrapper
    return decorator
    
@repeat(3)
def say_hi():
    print("Hi!")
    
say_hi()

#Output:
Hi!
Hi!
Hi!
```

---
## 8. Common real-world uses

### Logging
```
def log(func):
    def wrapper(*args, **kwargs):
        print(f"Calling {func.__name__}")
        return func(*args, **kwargs)
    return wrapper
```
### Timing
```
import time

def timer(func):
    def wrapper(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
        print(f"Took {end - start:.4f} seconds")
        return result
    return wrapper
```
### Access control
```
def requires_login(func):
    def wrapper(user, *args, **kwargs):
        if not user.is_logged_in:
            raise PermissionError("Login required")
        return func(user, *args, **kwargs)
    return wrapper
```

---
## 9. Decorators on methods and classes

Decorators work on:

- Functions
    
- Methods
    
- Classes
    

Built-in examples:

- `@staticmethod`
    
- `@classmethod`
    
- `@property`
```
class Person:
    def __init__(self, name):
        self._name = name

    @property
    def name(self):
        return self._name
```

---
## 10. Mental model (important for exams & interviews)

When you see:
```
@decorator
def f():
    pass
```
Think:
```
f = decorator(f)
```
And remember:

- Decorators **wrap** functions
    
- They don’t modify the original code
    
- They rely on **closures**