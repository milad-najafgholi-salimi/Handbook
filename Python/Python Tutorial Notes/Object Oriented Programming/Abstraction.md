In **Object-Oriented Programming (OOP)**, **abstraction** is the principle of **showing only what is necessary** and **hiding implementation details** from the user.  
It focuses on **what an object does**, not **how it does it**.

---
## 1. What is abstraction?
Abstraction means:
>Hiding internal implementation and exposing only essential features.

Real-world example:
- You use a car via steering, accelerator, and brakes
- You don’t need to know how the engine internally works

---
## 2. Why do we need abstraction?

Abstraction provides:

✔ Reduced complexity
✔ Better code organization
✔ Loose coupling
✔ Easier maintenance
✔ Enforced design rules

---
## 3. How Python supports abstraction

Python supports abstraction mainly through:
1) Abstract Base Classes (ABCs) → using the abc module
2) Abstract methods
3) Interfaces-like behavior (using ABCs)

---
## 4. Abstract Base Classes (ABC)

An abstract class is a class that:
- Cannot be instantiated
- May contain abstract methods
- Acts as a blueprint for child classes

To create one, use:
- `ABC` class
- `@abstractmethod` decorator

---
## 5. Creating an abstract class
```
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass
```
Key points:
- `Shape` cannot be instantiated
- Any subclass must implement `area()`

---
## 6. Implementing abstract methods in child classes
```
from abc import ABC, abstractmethod

class Shape(ABC):

    @abstractmethod
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, length, width):
        self.length = length
        self.width = width

    def area(self):
        return self.length * self.width

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius ** 2

r = Rectangle(10, 5)
c = Circle(7)

print(r.area())
print(c.area())

#Output:
50
153.86
```

---
## 7. What happens if a method is not implemented?
```
class Triangle(Shape):
    pass

t = Triangle()  # ERROR
```
Python raises:
```
TypeError: Can't instantiate abstract class ...
```
This forces correct implementation.

---
## 8. Abstract class with both abstract and concrete methods
Abstract classes can also have normal (concrete) methods.
```
class Vehicle(ABC):

    @abstractmethod
    def start(self):
        pass

    def fuel_type(self):
        print("Petrol or Diesel")

class Car(Vehicle):
    def start(self):
        print("Car starts with key")
```

---
## 9. Abstraction vs encapsulation (very important)
| Abstraction          | Encapsulation                 |
| -------------------- | ----------------------------- |
| Hides implementation | Hides data                    |
| Focuses on behavior  | Focuses on security           |
| Achieved using ABCs  | Achieved using access control |
| Design-level concept | Implementation-level concept  |

---
## 10. Abstraction and polymorphism together
Abstraction enables polymorphism.
```
def calculate_area(shape: Shape):
    print(shape.area())
```
>Point: This part of code is an example to above code in section 6.

This function works for:
- Rectangle
- Circle
- Any future shape

---
## 11. Interfaces in Python (conceptually)

Python doesn’t have a separate `interface` keyword like Java.

Instead:

- An abstract class with **only abstract methods** behaves like an interface
```
class Payment(ABC):

    @abstractmethod
    def pay(self, amount):
        pass
```

---
## 12. Abstract methods with parameters
```
class Employee(ABC):

    @abstractmethod
    def calculate_salary(self):
        pass
```
Each subclass defines its own logic.

---
## 13. Common mistakes
### ❌ Forgetting to inherit from ABC
```
class A:
    @abstractmethod
    def show(self):
        pass
```
This does **not** enforce abstraction.
### ❌ Instantiating abstract classes
Abstract classes are not meant to create objects.
### ❌ Changing method signature in child class
Breaks abstraction contract.

---
## 14. When should you use abstraction?

Use abstraction when:
- You want to define rules
- Multiple classes share common behavior
- Future extensions are expected
- You want to enforce implementation

---
## 15. Summary

- Abstraction hides implementation details
- Implemented using Abstract Base Classes
- Uses `abc` module
- Abstract methods must be overridden
- Helps achieve clean, scalable design
- Works closely with polymorphism
