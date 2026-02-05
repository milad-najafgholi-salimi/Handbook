In **object-oriented programming (OOP)**, **inheritance** is a mechanism that allows one class to **reuse, extend, or modify** the behavior of another class. Python supports inheritance in a very clean and flexible way.

---
## 1. What is inheritance?

**Inheritance** means:

> A _child (derived) class_ acquires properties and methods of a _parent (base) class_.

This helps with:

- Code reusability
    
- Logical hierarchy
    
- Easier maintenance
    
- Extensibility
    

---

## 2. Basic syntax of inheritance
```
class Parent:
    def show(self):
        print("This is parent")

class Child(Parent):
    pass

c = Child()
c.show()   # inherited from Parent

#Output:
This is parent
```

---
## 3. Types of inheritance in Python
Python supports multiple inheritance, so there are several types.
### 3.1 Single inheritance
One child, one parent.
```
class Animal:
    def speak(self):
        print("Animal speaks")

class Dog(Animal):
    def bark(self):
        print("Dog barks")
        
dog = Dog()
dog.bark()

animal = Animal()
animal.speak()

#Output:
Dog barks
Animal speaks
```
Also good to see:
```
class Animal:
	@classmethod
	def speak(cls):
		print("Animal speaks")
		
class Dog(Animal):
	def bark(self):
		print("Dog barks")
		
dog = Dog()
dog.bark()

Animal.speak()

#Output:
Dog barks
Animal speaks
```
Also this one:
```
class Animal:
	@classmethod
	def speak(self):
		print("Animal speaks")

class Dog(Animal):
	def bark(self):
		print("Dog barks")

dog = Dog()
dog.bark()

animal = Animal()
animal.speak()
Animal.speak()

#Output:
Dog barks
Animal speaks
Animal speaks
```
### 3.2 Multilevel inheritance
A chain of inheritance.
```
class Animal:
    def eat(self):
        print("Eating")

class Dog(Animal):
    def bark(self):
        print("Barking")

class Puppy(Dog):
    def play(self):
        print("Playing")
        
my_dog = Puppy()

my_dog.eat()
my_dog.bark()
my_dog.play()

#Output:
Eating
Barking
Playing
```
### 3.3 Multiple inheritance
A class inherits from **more than one parent**.
```
class Father:
    def skill_1(self):
        print("Gardening")

class Mother:
    def skill_2(self):
        print("Cooking")

class Child(Father, Mother):
    pass
    
son = Child()

son.skill_1()
son.skill_2()

#Output:
Gardening
Cooking
```
Python resolves conflicts using **MRO (Method Resolution Order)**.

---
### 3.4 Hierarchical inheritance
Multiple children from one parent.
```
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    pass

class Cat(Animal):
    pass
```
### 3.5 Hybrid inheritance

Combination of more than one type (possible due to multiple inheritance).

---

## 4. `super()` in inheritance
`super()` is used to call **parent class methods** from a child class.
```
class Parent:
    def __init__(self):
        print("Parent constructor")

class Child(Parent):
    def __init__(self):
        super().__init__()
        print("Child constructor")
```

---
## 5. Method overriding
When a child class provides its **own implementation** of a parent’s method.
```
class Animal:
    def speak(self):
        print("Animal sound")

class Dog(Animal):
    def speak(self):
        print("Bark")
        
d = Dog()
d.speak()   # Bark
```
### Calling the overridden method
```
class Dog(Animal):
    def speak(self):
        super().speak()
        print("Bark")
```

---
## 6. Constructor inheritance (`__init__`)

Parent constructors are **not called automatically** unless:

- You explicitly call them using `super()`
```
class Parent:
    def __init__(self, name):
        self.name = name

class Child(Parent):
    def __init__(self, name, age):
        super().__init__(name)
        self.age = age
```

---
## 7. Inheritance and class properties
Class properties are inherited too.
```
class A:
    x = 10

class B(A):
    pass
    
print(B.x)  # 10

B.x = 20

print(B.x)  # 20
```
- Only affects `B`
    
- `A.x` remains unchanged

---
## 8. Method Resolution Order (MRO)

In multiple inheritance, Python follows **C3 linearization**.
```
class A:
    pass

class B(A):
    pass

class C(A):
    pass

class D(B, C):
    pass
    
print(D.mro())

#Output:
[D, B, C, A, object]

#Real format output:
[<class '__main__.D'>, <class '__main__.B'>, <class '__main__.C'>, <class '__main__.A'>, <class 'object'>]
```
This determines which method is called first.

---
## 9. `is-a` relationship

Inheritance models an **“is-a” relationship**.

✔ Dog _is an_ Animal  
✔ Car _is a_ Vehicle

❌ Engine _is a_ Car (wrong → use composition)

---
## 10. When NOT to use inheritance

Avoid inheritance when:

- Relationship is **“has-a”**, not “is-a”
    
- Classes become tightly coupled
    
- You only want code reuse → consider **composition**
    

Example (composition):
```
class Engine:
    pass

class Car:
    def __init__(self):
        self.engine = Engine()
```

---
## 11. Common mistakes
### ❌ Forgetting super() in constructors
- Parent attributes won’t be initialized.
### ❌ Overusing inheritance
- Deep hierarchies make code hard to maintain.
### ❌ Conflicts in multiple inheritance
- Method name clashes if MRO is not understood.

---
## 12. Summary
- Inheritance allows code reuse
- Child classes can:
	- Use parent methods
	- Override parent methods
	- Extend functionality
- Python supports multiple inheritance
- super() ensures proper parent method calls
- Use inheritance for “is-a” relationships