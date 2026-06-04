In **object-oriented programming (OOP)**, **polymorphism** means **“many forms.”**  
It allows the **same method name or operation** to behave **differently depending on the object** that is calling it.

---
## 1. What is polymorphism?

**Polymorphism** allows:

> Different objects to respond to the **same method call** in their own way.

Example idea:

- `Animal.speak()` → different sounds
    
- Same method name, different behavior
    

---

## 2. Why do we need polymorphism?

Polymorphism provides:  
✔ Flexibility  
✔ Code reusability  
✔ Loose coupling  
✔ Cleaner and extensible design

You can write **generic code** that works with many object types.

---

## 3. Types of polymorphism in Python

Python supports polymorphism mainly in **four ways**:

1. Method overriding (runtime polymorphism)
    
2. Duck typing
    
3. Operator overloading
    
4. Method overloading (simulated)
    

---

## 4. Polymorphism via method overriding (most important)

This happens with **inheritance**.
```
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Bark")

class Cat(Animal):
    def speak(self):
        print("Meow")
        
animals = [Dog(), Cat(), Animal()]

for animal in animals:
    animal.speak()
    
#Output:
Bark
Meow
Animal sound

# Extra point:
Dog().speak() # also works

#Output:
Bark
```
Same method call → different behavior.

---
## 5. Runtime polymorphism

Python decides which method to call at runtime, not compile time.

This is called dynamic binding.
```
obj.speak()
```
The method executed depends on:
- The actual object type, not the reference name

---
## 6. Duck typing (Python-specific polymorphism)

>“If it walks like a duck and quacks like a duck, it’s a duck.”

Python doesn’t care about class inheritance—only whether the object has the required method.
```
class Bird:
    def fly(self):
        print("Bird flies")

class Airplane:
    def fly(self):
        print("Airplane flies")

def make_it_fly(obj):
    obj.fly()
    
make_it_fly(Bird())
make_it_fly(Airplane())

#Output:
Bird flies
Airplane flies
```
No inheritance, yet polymorphism works.

---
## 7. Polymorphism with built-in functions
Python’s built-in functions are polymorphic.
### len()
```
len("Hello")     # 5
len([1, 2, 3])   # 3
len((1, 2))      # 2
```
Same function, different behavior.

---
## 8. Operator overloading
Operators behave differently based on operands.
```
print(10 + 5)        # addition
print("Hi" + "Bye")  # string concatenation
```
You can define this behavior using magic methods.
```
class Point:
    def __init__(self, x):
        self.x = x

    def __add__(self, other):
        return self.x + other.x

p1 = Point(3)
p2 = Point(4)
print(p1 + p2)   # 7
```

---
## 9. Method overloading (not native in Python)

Python does not support traditional method overloading.

❌ This does NOT work:
```
def add(a, b):
    pass

def add(a, b, c):
    pass
```
The last definition replaces the first.

### How Python simulates method overloading
Using default arguments
```
def add(a, b, c=0):
    return a + b + c
```
Using `*args`
```
def add(*args):
    return sum(args)
```

---
## 10. Polymorphism vs inheritance (important distinction)
- Inheritance → structure
- Polymorphism → behavior

You can have polymorphism:
✔ With inheritance
✔ Without inheritance (duck typing)

---
## 11. Real-world example
```
class Payment:
    def pay(self):
        pass

class CreditCard(Payment):
    def pay(self):
        print("Paid using credit card")

class UPI(Payment):
    def pay(self):
        print("Paid using UPI")

def process_payment(payment):
    payment.pay()
    
process_payment(CreditCard())
process_payment(UPI())

#Output:
Paid using credit card
Paid using UPI
```
This function works for any payment type.

---
## 12. Common mistakes

### ❌ Assuming inheritance is required
Duck typing works without inheritance.
### ❌ Breaking polymorphism

Changing method signatures in child classes incorrectly.
### ❌ Overusing operator overloading

Makes code hard to read if abused.

---
## 13. Summary

- Polymorphism = **one interface, many behaviors**
    
- Python supports polymorphism via:
    
    - Method overriding (_same name method, different behavior_)
        
    - Duck typing
        
    - Operator overloading
        
    - Dynamic typing
        
- Enables flexible and scalable design
    
- Often used together with inheritance