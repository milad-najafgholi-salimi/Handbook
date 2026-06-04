## 1. What is `self`?

`self` represents **the current object (instance) of a class**.

When you create an object from a class and call one of its methods, Python automatically passes the **object itself** as the first argument to that method. By convention, we name that parameter `self`.

> `self` lets methods **access and modify the object’s own data and behavior**.

---

## 2. Why is `self` needed?

Each object created from a class has its **own copy of instance variables**.

`self` tells Python:

> “Use the variables and methods that belong to _this specific object_.”

Without `self`, Python wouldn’t know **which object’s data** you are referring to.

---

## 3. Basic example
```
class Student:
    def greet(self):
        print("Hello!")

s1 = Student()
s1.greet()

#Output:
Hello!
```
What actually happens behind the scenes
```
Student.greet(s1)
```
Python automatically passes `s1` as `self`.

---
## 4. `self` and instance variables

Instance variables are **defined using `self`**.
```
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def show(self):
        print(self.name, self.age)

s1 = Student("Milad", 22)
s2 = Student("Faraz", 20)

s1.show()   # Milad 22
s2.show()   # Faraz 20
```
- `self.name` belongs to **that specific object**
    
- `s1.name` and `s2.name` are **different**

---
## 5. `self` vs local variables
```
class Example:
    def set_value(self):
        x = 10          # local variable
        self.y = 20     # instance variable
```
- `x` exists **only inside the method**
    
- `self.y` exists **as long as the object exists**
    

Trying this:
```
obj = Example()
obj.set_value()
print(obj.y)   # works
print(obj.x)   # ERROR
```

---
## 6. Can we use a name other than `self`?

Yes, but **you should not**.
```
class Test:
    def show(this):
        print("Hello")
```
This works, but:

- It breaks conventions
    
- Makes code confusing
    
- Other developers expect `self`
    

**Best practice:** always use `self`.

---
## 7. `self` is not a keyword

- `self` is **not a Python keyword**
    
- It’s just a **naming convention**
    
- Python only cares that it’s the **first parameter**

---
## 8. `self` in calling other methods
```
class Calculator:
    def add(self, a, b):
        return a + b

    def double_sum(self, a, b):
        return self.add(a, b) * 2
```
Here, `self.add()` means:

> “Call the `add` method of **this same object**”

---
## 9. Common mistakes with `self`

### ❌ Forgetting `self`
```
class A:
    def set(self, x):
        value = x   # WRONG
```
### ✅ Correct version
```
class A:
    def set(self, x):
        self.value = x
```
### ❌ Forgetting `self` in method definition
```
class A:
    def show():
        print("Hi")
```
This will cause an error when called on an object.

---
## 10. Quick summary

- `self` refers to **the current object**
    
- It is automatically passed by Python
    
- Used to access **instance variables and methods**
    
- Required as the **first parameter** of instance methods
    
- Not a keyword, but a strong convention
