**Encapsulation** is one of the **four pillars of Object-Oriented Programming (OOP)** (along with inheritance, polymorphism, and abstraction). It focuses on **data protection and controlled access**.

---
## 1. What is encapsulation?

Encapsulation means:
>Wrapping data (variables) and methods together inside a class and restricting direct access to some of the object’s internal details.

In simple words:
- Data is hidden
- Access is controlled through methods

---
## 2. Why do we need encapsulation?

Encapsulation provides:

✔ Data security
✔ Controlled modification of data
✔ Reduced complexity
✔ Better maintainability
✔ Prevention of accidental misuse

---
## 3. Encapsulation in Python (important concept)

Unlike languages like Java or C++, Python does not have true private variables.

Instead, Python uses naming conventions and name mangling.

---
## 4. Access levels in Python

Python supports three levels of access (by convention):
### 4.1 Public members
Accessible everywhere.
```
class Student:
    def __init__(self, name):
        self.name = name   # public variable

s = Student("Milad")
print(s.name)   # allowed

#Output:
Milad
```
### 4.2 Protected members (`_variable`)
- Prefix with a single underscore
- Meant to be accessed only within class and subclasses
- Still accessible from outside (convention only)
```
class Student:
    def __init__(self):
        self._roll = 101

print(s._roll)   # possible, but discouraged
```
### 4.3 Private members (`__variable`)

- Prefix with **double underscore**
    
- Python performs **name mangling**
```
class Student:
    def __init__(self):
        self.__marks = 90
```
Trying to access directly:
```
s = Student()
print(s.__marks)   # ERROR
```
But internally Python changes the name to:
```
_Student__marks
```

---
## 5. Name mangling explained
```
class Test:
    def __init__(self):
        self.__x = 10
```
Internally stored as:
```
_Test__x
```
This:
- Avoids accidental access
- Prevents name conflicts in inheritance

⚠ Still accessible if someone really wants:
```
print(obj._Test__x)
```
**which means:**
```
class Test:
    def __init__(self):
        self.__x = 10
        
s = Test()
print(s.__x)  #Error

#But:

s = Test()
print(s._Test__x)  #10
```
Encapsulation in Python is about discipline, not force.

---
## 6. Encapsulation using getter and setter methods

### Traditional way
```
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    def get_balance(self):
        return self.__balance

    def set_balance(self, amount):
        if amount >= 0:
            self.__balance = amount
            
person1 = BankAccount(100)

print(person1.get_balance())
person1.set_balance(200)
print(person1.get_balance())

#Output:
100
200
```
This ensures:
- Validation
- Controlled access

---
## 7. Encapsulation using @property (Pythonic way)
This is the preferred approach in Python.
```
class BankAccount:
    def __init__(self, balance):
        self.__balance = balance

    @property
    def balance(self):
        return self.__balance

    @balance.setter
    def balance(self, amount):
        if amount < 0:
            raise ValueError("Balance cannot be negative")
        self.__balance = amount
        
acc = BankAccount(1000)
print(acc.balance)     # getter
acc.balance = 2000     # setter
```
Looks like direct access, but still controlled.

---
## 8. Encapsulation and abstraction (difference)
| Encapsulation                 | Abstraction                     |
| ----------------------------- | ------------------------------- |
| Hides data                    | Hides implementation            |
| Focuses on data protection    | Focuses on design               |
| Achieved using access control | Achieved using abstract classes |

---
## 9. Encapsulation in inheritance
Private variables are not directly accessible in child classes.
```
class Parent:
    def __init__(self):
        self.__x = 10

class Child(Parent):
    def show(self):
        print(self.__x)   # ERROR
```
Correct approach:
```
class Parent:
    def __init__(self):
        self.__x = 10

    def get_x(self):
        return self.__x
```

---
## 10. Common mistakes
### ❌ Believing private means “completely inaccessible”
Python uses name mangling, not strict privacy.
### ❌ Avoiding encapsulation because Python is dynamic
Encapsulation is still essential for clean design.
### ❌ Overusing getters/setters unnecessarily
Use them only when validation or control is needed.

---
## 11. Real-world analogy

Think of a bank ATM:
- You don’t access money directly
- You use methods (withdraw, deposit)
- Internal data is hidden

That’s encapsulation.

---
## 12. Summary
- Encapsulation = data hiding + controlled access
- Python uses:
	- Public (`var`)
	- Protected (`_var`)
	- Private (`__var`)
- Best practice:
	- Use `@property` for clean encapsulation
- Improves security, maintainability, and clarity
