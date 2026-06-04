In Python OOP, **class properties** (more commonly called **class variables**) are attributes that belong to the **class itself**, not to individual objects. They are shared by **all instances** of that class.

---
## 1. What are class properties (class variables)?

A **class property** is a variable defined **inside a class but outside any method**.
```
class Student:
    school_name = "Green Valley School"  # class property
```
- `school_name` belongs to the **Student class**
    
- All `Student` objects share the **same value**

---
## 2. Class properties vs instance properties

### Instance property

- Created using `self`
    
- Unique to each object
    

### Class property

- Created using the class name
    
- Shared by all objects
    

Example:
```
class Student:
    school = "Green Valley"
    
    def __init__(self, name):
        self.name = name
        
s1 = Student("Milad")
s2 = Student("Faraz")

print(s1.school)   # Green Valley
print(s2.school)   # Green Valley
```
Here:

- `name` → instance property
    
- `school` → class property

---
## 3. How Python looks up class properties

When you access `obj.property`, Python checks in this order:

1. Instance namespace (`obj.__dict__`)
    
2. Class namespace (`Class.__dict__`)
    
3. Parent classes (inheritance)
    

That’s why this works:
```
print(s1.school)
```
Even though `school` is not inside `s1`.

---
## 4. Modifying class properties

### ❌ Modifying via an object (common mistake)
```
s1.school = "Blue Valley"
```
This does **not** change the class property.

Instead:

- Python creates a **new instance variable** named `school` for `s1`
```
print(s1.school)   # Blue Valley
print(s2.school)   # Green Valley
```
### ✅ Correct way: modify via the class
```
Student.school = "Blue Valley"

print(s1.school)   # Blue Valley
print(s2.school)   # Blue Valley
```
Now all objects see the change.

---
## 5. When should you use class properties?

Use class properties when data is:

✔ Common to all objects  
✔ Conceptually belongs to the class, not individuals

Examples:

- School name
    
- Company name
    
- Interest rate
    
- Maximum limit
    
- Counter for number of objects created

---
## 6. Example: counting objects using class property
```
class Student:
    count = 0  # class property

    def __init__(self, name):
        self.name = name
        Student.count += 1
        
s1 = Student("Milad")
s2 = Student("Faraz")

print(Student.count)  # 2
```
All objects share the same `count`.

---
## 7. Class methods and class properties

Class properties are usually accessed or modified using **class methods**.
```
class Student:
    school = "Green Valley"

    @classmethod
    def change_school(cls, new_name):
        cls.school = new_name

Student.change_school("Blue Valley")

obj_1 = Student()
obj_2 = Student()

print(obj_1.school)
print(obj_2.school)

#Output:
Blue Valley
Blue Valley
```
Here:

- `cls` refers to the **class**
    
- Best practice for modifying class properties

---
## 8. Class property vs `@property` (important clarification)

⚠️ These two are often confused.

### Class property (what we discussed)
```
class A:
    x = 10
```
### `@property` decorator

- Used for **instance attributes**
    
- Provides getter/setter behavior
```
class A:
    def __init__(self):
        self._x = 10

    @property
    def x(self):
        return self._x
```
They are **different concepts**.

---
## 9. Class properties and inheritance
```
class Parent:
    x = 10

class Child(Parent):
    pass

print(Child.x)  # 10
```
If you modify:
```
Child.x = 20
```
- Only `Child` changes
    
- `Parent.x` remains `10`

---
## 10. Common mistakes

### ❌ Using `self` for class properties
```
self.school = "ABC"
```
This creates an **instance property**, not a class one.

❌ Assuming changes via object affect all objects
```
obj.school = "XYZ"  # creates instance variable
```

---
## 11. Summary table
| Feature       | Class Property        | Instance Property |
| ------------- | --------------------- | ----------------- |
| Defined using | Class name            | `self`            |
| Belongs to    | Class                 | Object            |
| Shared        | Yes                   | No                |
| Access via    | `Class.prop`          | `obj.prop`        |
| Modified via  | Class or class method | Object            |