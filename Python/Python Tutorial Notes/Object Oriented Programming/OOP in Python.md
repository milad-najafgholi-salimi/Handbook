**Object-Oriented Programming (OOP)** in Python is a way of organizing code by **grouping data and behavior together** using **objects and classes**. Python fully supports OOP and it is a **core topic for exams, interviews, and real-world programming**.

---
## 1. What Is OOP?

**OOP** is a programming paradigm based on the concept of **objects**.

An **object**:

- Represents a real-world entity
    
- Contains **data (attributes)** and **behavior (methods)**
    

Example (real world):

- Object: _Student_
    
- Attributes: name, age
    
- Methods: study(), attend_class()

---
## 2. Class and Object

### Class

A **class** is a **blueprint** for creating objects.
```
class Student:
    pass
```
### Object

An **object** is an **instance** of a class.
```
s1 = Student()
```

---
## 3. Attributes and Methods
```
class Student:
    def __init__(self, name, age):
        self.name = name     # attribute
        self.age = age       # attribute

    def greet(self):         # method
        print("Hello, my name is", self.name)

s = Student("Milad", 22)
s.greet()

#Output:
Hello, my name is Milad
```

---
## 4. The `__init__()` Method (Constructor)

- Automatically called when an object is created
    
- Used to initialize attributes
```
def __init__(self):
    pass
```
📌 `self` refers to the **current object**

---
## 5. The Four Pillars of OOP (VERY IMPORTANT)

### 1. Encapsulation

**Binding data and methods together** and restricting access.
```
class Account:
    def __init__(self, balance):
        self.__balance = balance  # private

    def get_balance(self):
        return self.__balance
```
- `__balance` is **private**
    
- Accessed via methods
### 2. Abstraction

**Hiding implementation details** and showing only essentials.
```
from abc import ABC, abstractmethod

class Shape(ABC):
    @abstractmethod
    def area(self):
        pass
```
### 3. Inheritance

One class **inherits** another class.
```
class Animal:
    def sound(self):
        print("Some sound")

class Dog(Animal):
    def sound(self):
        print("Bark")
        
d = Dog()
d.sound()

#Output:
Bark
```
### 4. Polymorphism

Same method name, **different behavior**.
```
class Cat:
    def sound(self):
        print("Meow")

class Dog:
    def sound(self):
        print("Bark")

for animal in (Cat(), Dog()):
    animal.sound()
    
#Output:
Meow
Bark
```

---
## 6. Types of Inheritance
| Type         | Description                 |
| ------------ | --------------------------- |
| Single       | One parent                  |
| Multiple     | Multiple parents            |
| Multilevel   | Parent → Child → Grandchild |
| Hierarchical | One parent, many children   |
| Hybrid       | Combination                 |
##### Example (Multiple):
```
class A:
    pass

class B:
    pass

class C(A, B):
    pass
```

---
## 7. Instance, Class, and Static Methods
```
class Example:
    def instance_method(self):
        pass

    @classmethod
    def class_method(cls):
        pass

    @staticmethod
    def static_method():
        pass
```

---
## 8. Special (Magic / Dunder) Methods
```
class Book:
    def __init__(self, title):
        self.title = title

    def __str__(self):
        return self.title
```
Common dunder methods:

- `__init__`
    
- `__str__`
    
- `__len__`
    
- `__eq__`

---
## 9. Access Modifiers in Python
| Modifier  | Syntax   | Meaning               |
| --------- | -------- | --------------------- |
| Public    | `name`   | Accessible everywhere |
| Protected | `_name`  | Convention only       |
| Private   | `__name` | Name mangling         |

---
## 10. OOP vs Procedural Programming
| OOP             | Procedural     |
| --------------- | -------------- |
| Object-based    | Function-based |
| Data + behavior | Separate       |
| Reusable        | Less reusable  |
| Secure          | Less secure    |

---
## 11. Why Use OOP?

✔ Code reusability  
✔ Better organization  
✔ Easier maintenance  
✔ Models real-world problems  
✔ Scalable programs

---
## 12. Exam-Ready Definitions

- **Class**: Blueprint for objects
    
- **Object**: Instance of a class
    
- **Encapsulation**: Binding data and methods
    
- **Inheritance**: Acquiring properties from another class
    
- **Polymorphism**: One interface, multiple behaviors
    
- **Abstraction**: Hiding implementation details

---
## 13. Final Summary

- Python supports full OOP
    
- Core concepts: class, object, methods, attributes
    
- Four pillars: encapsulation, abstraction, inheritance, polymorphism
    
- OOP makes programs modular and reusable