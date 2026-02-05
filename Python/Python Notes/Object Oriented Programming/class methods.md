## 1. What is a class method?

A **class method** is a method that:

- Is bound to the **class**, not an object
    
- Uses the **`@classmethod` decorator**
    
- Takes **`cls`** (the class) as its first parameter
```
class Student:
    school = "Green Valley"

    @classmethod
    def show_school(cls):
        print(cls.school)

Student.show_school()

#Output:
Green Valley
```
Here:

- `cls` refers to the `Student` class
    
- `cls.school` accesses the class property

---
## 2. Why do we need class methods?

Use class methods when you want to:

✔ Work with **class variables (class properties)**  
✔ Represent behavior that belongs to the **class as a whole**  
✔ Create **alternative constructors**  
✔ Support **inheritance-friendly design**

---
## 3. Class method vs instance method

### Instance method
```
def method(self):
    pass
```
- Works on **individual objects**
    
- Uses `self`
    

### Class method
```
@classmethod
def method(cls):
    pass
```
- Works on the **class**
    
- Uses `cls`
    

Example comparison:
```
class Example:
    x = 10

    def instance_method(self):
        print(self.x)

    @classmethod
    def class_method(cls):
        print(cls.x)
        
obj = Example()
obj.instance_method()
Example.class_method()

#Output:
10
10
```

---
## 4. Accessing class methods
You can call a class method using:
```
ClassName.method()
```
or
```
obj.method()
```
But **best practice** is to call it via the **class name** to avoid confusion.

---
## 5. Modifying class properties using class methods
```
class Student:
    school = "Green Valley"

    @classmethod
    def change_school(cls, new_name):
        cls.school = new_name

Student.change_school("Blue Valley")
print(Student.school)

#Output:
Blue Valley
```
All objects see the change.

---
## 6. Alternative constructors (very important use case)

Class methods can create objects in **different ways**.
```
class Student:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, data):
        name, age = data.split(",")
        return cls(name, int(age))

s = Student.from_string("Milad,22")
```
Why this is powerful:

- `cls()` ensures the **correct class is created**
    
- Works correctly with **inheritance**

---
## 7. Class methods and inheritance
```
class Parent:
    @classmethod
    def who(cls):
        print(cls.__name__)

class Child(Parent):
    pass

Parent.who()  # Parent
Child.who()   # Child
```
This is why `cls` is preferred over hardcoding class names.

---
## 8. Class methods vs static methods (common exam topic)

### Class method

- Uses `cls`
    
- Can access class variables
    
- Knows which class called it
```
@classmethod
def method(cls):
    pass
```
### Static method

- Uses no `self` or `cls`
    
- Behaves like a normal function inside a class
```
@staticmethod
def method():
    pass
```

| Feature             | Class Method   | Static Method   |
| ------------------- | -------------- | --------------- |
| Decorator           | `@classmethod` | `@staticmethod` |
| First argument      | `cls`          | None            |
| Access class data   | Yes            | No              |
| Knows calling class | Yes            | No              |

---
## 9. Common mistakes

### ❌ Forgetting the decorator
```
def method(cls):
    pass
```
This is just an **instance method** with a bad name.
### ❌ Using `self` instead of `cls`
```
@classmethod
def method(self):
    pass
```
This works but breaks convention and causes confusion.
### ❌ Modifying class variables via objects
```
obj.school = "XYZ"
```
This creates an **instance variable**, not a class-level change.

---
## 10. When should you NOT use class methods?

Avoid class methods when:

- The behavior depends on **instance-specific data**
    
- You need to modify **object state**, not class state
    

Use instance methods instead.

---
## 11. Summary
- Class methods belong to the class
- Defined using @classmethod
- Use cls as the first parameter
- Common uses:
	- Working with class properties
	- Alternative constructors
	- Inheritance-friendly behavior