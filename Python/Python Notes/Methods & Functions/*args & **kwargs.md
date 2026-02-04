## 1. What Are `*args` and `**kwargs`?

They allow a function to accept a **variable number of arguments**.

- `*args` → **many positional arguments**
    
- `**kwargs` → **many keyword arguments**
    

The names `args` and `kwargs` are **conventions**, not keywords.  
What matters is:

- `*` (single asterisk)
    
- `**` (double asterisk)

---
## 2. `*args` (Variable-Length Positional Arguments)

### Basic Idea

`*args` collects **extra positional arguments** into a **tuple**.
```
def show_numbers(*args):
    print(args)
```
Call:
```
show_numbers(1, 2, 3, 4)
```
Output:
```
(1, 2, 3, 4)
```
✔ `args` is a **tuple**

#### Example: Sum Any Number of Values
```
def total(*numbers):
    s = 0
    for n in numbers:
        s += n
    return s
    
print(total(1, 2))
print(total(1, 2, 3, 4, 5))

Output:
3
15
```
### Mixing Normal Parameters and `*args`
```
def greet(name, *messages):
    print("Hello", name)
    for msg in messages:
        print(msg)
```
Call:
```
greet("Milad", "Welcome", "Good luck")
```
**Output:**
```
Hello Milad
Welcome
Good luck
```
📌 Rule:

- Normal parameters come **before** `*args`

---
## 3. `**kwargs` (Variable-Length Keyword Arguments)

### Basic Idea

`**kwargs` collects **keyword arguments** into a **dictionary**.
```
def show_info(**kwargs):
    print(kwargs)
```
Call:
```
show_info(name="Milad", age=22, course="Python")
```
Output:
```
{'name': 'Milad', 'age': 22, 'course': 'Python'}
```
✔ `kwargs` is a **dictionary**  
✔ Keys are strings
#### Example: Accessing Values
```
def student_info(**data):
    for key, value in data.items():
        print(key, ":", value)
```
### Using Default Values with `kwargs`
```
def profile(**kwargs):
    name = kwargs.get("name", "Guest")
    age = kwargs.get("age", "Unknown")
    print(name, age)
    
profile(name = "Milad", age = 22)

#Output:
Milad 22
```

---
## 4. Using `*args` and `**kwargs` Together

You can use **both in the same function**.
```
def demo(*args, **kwargs):
    print("Args:", args)
    print("Kwargs:", kwargs)
```
Call:
```
demo(1, 2, 3, name="Milad", city="Tehran")
```
**Output:**
```
Args: (1, 2, 3)
Kwargs: {'name': 'Milad', 'city': 'Tehran'}
```
📌 Order rule:
```
def func(normal_args, *args, **kwargs):
    pass
```

---
## 5. Argument Order (VERY IMPORTANT)

When defining a function:
```
1. Normal parameters
2. *args
3. **kwargs
```
When calling a function:
```
1. Positional arguments
2. Keyword arguments
```
❌ Invalid:
```
func(name="Alex", 10)
```
✔ Valid:
```
func(10, name="Alex")
```

---
## 6. Unpacking with `*` and `**`

### Unpacking a List or Tuple (`*`)
```
numbers = [1, 2, 3]
print(*numbers)
```
Equivalent to:
```
print(1, 2, 3)
```
Passing list to function:
```
def add(a, b, c):
    print(a + b + c)

add(*numbers)
```
### Unpacking a Dictionary (`**`)
```
def show(a, b):
    print(a, b)

data = {"a": 1, "b": 2}

show(**data)

#Output:
1 2
```

---
## 7. Real-World Use Cases

### 1. Flexible APIs
```
def log(message, **options):
    if options.get("error"):
        print("ERROR:", message)
```
### 2. Wrappers / Decorators
```
def wrapper(*args, **kwargs):
    func(*args, **kwargs)
```
### 3. Forwarding Arguments
```
def child(*args, **kwargs):
    parent(*args, **kwargs)
```

---
## 8. Common Mistakes

### ❌ Treating `args` as a list (it’s a tuple)
```
args.append(5)  # Error
```
✔ Convert if needed:
```
list(args)
```
### ❌ Forgetting order
```
def f(**kwargs, *args):  # SyntaxError
```
### ❌ Assuming `kwargs` keys are variables
```
show_info(name=Alex)  # Error
```
✔ Must be:
```
show_info(name="Alex")
```

---
## 9. Simple Exam Definition (Memorize This)

> `*args` allows a function to accept any number of positional arguments and stores them as a tuple.

> `**kwargs` allows a function to accept any number of keyword arguments and stores them as a dictionary.

