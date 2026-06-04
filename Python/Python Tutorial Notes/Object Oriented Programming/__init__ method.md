## 1. What Is `__init__`?

`__init__` is a **special (dunder) method** in Python that is **automatically called when an object is created** from a class.

📌 It is called a **constructor**, but technically:

- `__new__` creates the object
    
- `__init__` **initializes** the object

---
## 2. Basic Example
```
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age
        
s = Student("Milad", 22)
```
What happens:

1. Memory is allocated for `s`
    
2. `__init__` runs automatically
    
3. Attributes are assigned

---
## 3. Why Do We Use `__init__`?

`__init__` is used to:  
✔ Initialize object data  
✔ Ensure objects start in a valid state  
✔ Avoid repeating setup code  
✔ Customize each object

Without `__init__`:
```
s = Student()
s.name = "Milad"
s.age = 22
```
❌ Error-prone and repetitive

---
## 4. Role of `self` in `__init__`
```
def __init__(self, name):
    self.name = name
```
- self refers to the current object
- self.name becomes an instance variable
- Each object has its own copy
```
s1 = Student("Milad")
s2 = Student("Faraz")
```

---
## 5. Instance Variables vs Local Variables
```
def __init__(self, x):
    self.x = x   # instance variable
    y = 10       # local variable
```
self.x → stored in the object

y → destroyed after __init__ ends

📌 Only variables attached to self persist.

---
## 6. Default Values in __init__
```
class Student:
    def __init__(self, name="Guest", age=0):
        self.name = name
        self.age = age
        
s1 = Student("Milad")
print(s1.name, s1.age)

#Output:
Milad 0
```

---
## 7. __init__ with Validation (Best Practice)
```
class Account:
    def __init__(self, balance):
        if balance < 0:
            raise ValueError("Balance cannot be negative")
        self.balance = balance
```
✔ Objects always start in a valid state

---
## 8. Multiple Objects, Same Class
```
class Car:
    def __init__(self, color):
        self.color = color
        
c1 = Car("Red")
c2 = Car("Blue")

print(c1.color)
print(c2.color)

#Output:
Red
Blue
```
Each object has separate data.

---
## 9. __init__ and Inheritance
### Parent Class
```
class Animal:
    def __init__(self, name):
        self.name = name
```
### Child Class
```
class Dog(Animal):
    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
```
📌 super().__init__() calls the parent’s constructor.

---
## 10. What Happens If You Don’t Define __init__?

Python provides a default constructor:
```
class A:
    pass

a = A()
```
✔ Object is created
❌ No attributes initialized

---
## 11. `__init__` Is NOT a Normal Function
| Feature              | `__init__`           |
| -------------------- | -------------------- |
| Called automatically | ✔                    |
| Returns a value      | ❌ (must return None) |
| Name                 | Fixed                |
| Purpose              | Initialize object    |
❌ This is wrong:
```
def __init__(self):
    return 10
```

---
## 12. __new__ vs __init__ (Advanced but Important)
```
class Example:
    def __new__(cls):
        return super().__new__(cls)

    def __init__(self):
        print("Initialized")
```
__new__ → creates object

__init__ → initializes object

📌 Most of the time, you only need __init__.

---
## 13. Common Mistakes
❌ Forgetting self
```
def __init__(name):
    self.name = name  # Error
```
❌ Not using self when assigning
```
name = name  # useless
```
❌ Overloading __init__ (Python doesn’t support it)
```
✔ Use default arguments instead.
```

---
## 14. Exam-Ready Definition (Memorize This)

__init__ is a special method in Python that is automatically called when an object is created and is used to initialize the object’s data.

---
## 15. Final Summary

- `__init__` initializes objects
    
- Runs automatically on object creation
    
- Uses `self` to store instance variables
    
- Essential for clean OOP design
    
- Works with inheritance via `super()`