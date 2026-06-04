In **Python OOP**, an **inner class** is a class that is **defined inside another class**.  
They are not used very frequently, but they are important conceptually and sometimes appear in **exams and design discussions**.

---
## 1. What is an inner class?
An inner class is a class defined inside the body of another class.
```
class Outer:
    class Inner:
        pass
```
- Outer → outer class
- Inner → inner class
The inner class is logically associated with the outer class.

---
## 2. Why use inner classes?
Inner classes are used when:

✔ A class is meaningful only within another class
✔ You want better logical grouping
✔ You want to hide implementation details
✔ There is a strong “has-a” relationship

Example:
- `Car` has an `Engine`
- `Engine` exists only in the context of `Car`

---
## 3. Basic example
```
class Car:
    def __init__(self, name):
        self.name = name
        self.engine = self.Engine()

    class Engine:
        def start(self):
            print("Engine started")
            
c = Car("BMW")
c.engine.start()

#Output:
Engine startedEngine started
```

---
## 4. Accessing inner class
### 4.1 Using outer class name
```
engine = Car.Engine()
engine.start()
```
This works, but:
- Often avoided
- Breaks the idea of encapsulation
### 4.2 Using outer class object (preferred)
```
car = Car("Audi")
car.engine.start()
```
This keeps the inner class tied to the outer class.

---
## 5. Relationship between outer and inner class
Important point:
>Inner class does NOT automatically get access to outer class members.

```
class Outer:
    def __init__(self):
        self.x = 10

    class Inner:
        def show(self):
            print(self.x)   # ERROR
```
To fix this, explicitly pass the outer object:
```
class Outer:
    def __init__(self):
        self.x = 10
        self.inner = self.Inner(self)

    class Inner:
        def __init__(self, outer):
            self.outer = outer

        def show(self):
            print(self.outer.x)
```

---
## 6. Inner class vs nested functions
| Inner Class              | Nested Function        |
| ------------------------ | ---------------------- |
| Used for object modeling | Used for logic scoping |
| Can create objects       | Cannot persist objects |
| Supports OOP concepts    | Limited scope          |

---
## 7. Inner classes and encapsulation

Inner classes help in encapsulation by:
- Hiding complex components
- Restricting usage scope
- Improving code organization
But note:
- Python does not enforce strict access control

---
## 8. Multiple inner classes
```
class University:
    class Student:
        pass

    class Teacher:
        pass
```
Each inner class represents a component of the outer class.

---
## 9. Real-world example
```
class Bank:
    class Account:
        def __init__(self, balance):
            self.balance = balance

        def deposit(self, amount):
            self.balance += amount
            
        def balance(self):
	        self.balance = balance

balance = 0
acc = Bank.Account(1000)
acc.deposit(500)
print(acc.balance)

#Output:
1500
```

---
## 10. Inner classes and inheritance
Inner classes can be inherited, just like normal classes.
```
class A:
    class B:
        def show(self):
            print("Hello")

class C(A.B):
    pass
```

---
## 11. When NOT to use inner classes

Avoid inner classes when:
- They add unnecessary complexity
- The class is useful independently
- Simpler composition is enough

---
## 12. Common mistakes
### ❌ Assuming inner class automatically accesses outer class data
You must explicitly pass the outer instance.
### ❌ Overusing inner classes
They reduce readability if used unnecessarily.
### ❌ Confusing inner classes with access control
Python does not enforce strict privacy.

---
## 13. Exam-oriented key points
- Inner class = class inside another class
- Used for logical grouping
- Represents strong association
- No automatic access to outer class members
- Access via outer class or object

---
## 14. Summary
- Inner classes improve logical structure
- Used when one class depends strongly on another
- Helps with encapsulation and design clarity
- Not commonly used but important conceptually