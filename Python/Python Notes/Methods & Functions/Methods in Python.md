In Python, **methods** are functions that are **associated with an object**. They define what an object _can do_. Since Python is an object-oriented language, almost everything in Python has methods.

---
## 1. What is a Method?

A **method** is a function that belongs to a **class** and is called on an **instance (object)** of that class.
```
text = "hello"
print(text.upper())

#Output:
"HELLO"
```
Here:

- `"hello"` is a **string object**
    
- `upper()` is a **method** of the `str` class

---
## 2. Method vs Function
| Function          | Method                          |
| ----------------- | ------------------------------- |
| Stands alone      | Belongs to an object            |
| Called directly   | Called using dot (`.`) notation |
| Example: `len(x)` | Example: `x.append()`           |
Example:
```
numbers = [1, 2, 3]

len(numbers)        # function
numbers.append(4)  # method
```

---
## 3. Built-in Methods (Common Examples)

### String Methods
```
name = "Python"

name.lower()      # 'python'
name.upper()      # 'PYTHON'
name.replace("P", "J")  # 'Jython'
name.split("t")   # ['Py', 'hon']
```
### List Methods
```
nums = [3, 1, 2]

nums.append(4)
nums.sort()
nums.remove(1)
```
### Dictionary Methods
```
student = {"name": "Milad", "age": 22}

student.keys()
student.values()
student.get("age")
```

---
## 4. User-Defined Methods (Inside a Class)

You can create your own methods by defining a **class**.
```
class Student:
    def greet(self):
        print("Hello!")
```
Usage:
```
s = Student()
s.greet()
```
**Output:**
```
Hello
```
### Why `self`?

- `self` refers to the **current object**
    
- It allows methods to access object data and other methods

---
## 5. Instance Methods

The most common type of method.
```
class Dog:
    def bark(self):
        print("Woof!")
```
Called on an object:
```
dog = Dog()
dog.bark()
```

---
## 6. Class Methods

Belong to the **class**, not the instance.
```
class MyClass:
    @classmethod
    def info(cls):
        print("This is a class method")
```
Call:
```
MyClass.info()
```
- Uses `cls` instead of `self`
    
- Often used for **factory methods**
>The `@classmethod` decorator in Python transforms a method into a **class method**, which is bound to the class rather than an instance of the class.  This means the method receives the class (`cls`) as its first implicit argument, instead of the instance (`self`).

---
## 7. Static Methods

Do **not** use `self` or `cls`.
```
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```
Call:
```
Math.add(2, 3)
```
Used when:

- The method logically belongs to the class
    
- But does not need class or instance data

---
## 8. Special (Magic / Dunder) Methods

Methods with double underscores.
```
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return self.title
```
Examples:

- `__init__()` → constructor
    
- `__str__()` → string representation
    
- `__len__()` → length of object
    
- `__eq__()` → equality comparison

---
## 9. Calling Methods
```
object.method(arguments)
```
Example:
```
"hello".capitalize()
```
Behind the scenes:
```
str.capitalize("hello")
```

---
## 10. Why Methods Are Important

Methods:

- Define **behavior** of objects
    
- Support **encapsulation**
    
- Make code **organized and reusable**
    
- Are essential for **object-oriented programming**

---
## 11. Quick Summary

- A method is a function tied to an object
    
- Called using dot (`.`) notation
    
- Types:
    
    - Instance methods
        
    - Class methods
        
    - Static methods
        
    - Special (dunder) methods
        
- Used to define object behavior