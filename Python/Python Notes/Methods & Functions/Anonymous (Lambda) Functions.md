Anonymous functions in Python are called **lambda functions**. They are **small, one-line functions** without a name, used for **short, simple operations**.

---
## 1. What Is a Lambda Function?

A **lambda function** is:

- An **anonymous** (nameless) function
    
- Defined using the keyword `lambda`
    
- Written in **one line**
    
- Used for **simple logic**
    
### Syntax
```
lambda arguments: expression
```
Example:
```
square = lambda x: x * x
print(square(5))

#Output:
25
```
✔ No `def`  
✔ No function name  
✔ Expression result is returned automatically

---
## 2. Lambda vs Normal Function

### Normal Function
```
def add(a, b):
    return a + b
```
### Lambda Function
```
add = lambda a, b: a + b
```

| Feature        | Normal Function | Lambda        |
| -------------- | --------------- | ------------- |
| Name           | Required        | Not required  |
| Lines          | Multiple        | Single        |
| Statements     | Allowed         | ❌ Not allowed |
| Return keyword | Required        | ❌ Not used    |

---
## 3. Key Rules of Lambda Functions

1. **Only one expression**
    
2. **No statements** (no `if`, `for`, `while`, `try`, etc. *as blocks*)
    
3. Expression is **returned automatically**
    
4. Can have **multiple arguments**
    
5. Best for **short-lived use**
    

✔ Valid:
```
lambda x: x + 1
```
❌ Invalid:
```
lambda x:
    x + 1   # SyntaxError
```

---
## 4. Lambda with Multiple Arguments
```
multiply = lambda a, b, c: a * b * c
print(multiply(2, 3, 4))
```

---
## 5. Lambda with Conditional Expression

You **can** use a ternary expression:
```
max_num = lambda a, b: a if a > b else b
print(max_num(5, 3))
```
📌 This is an **expression**, not a statement.

---
## 6. Lambda with Built-in Functions (Very Important)

### `map()` – apply function to each element
```
nums = [1, 2, 3, 4]
squares = list(map(lambda x: x * x, nums))

print(squares)

#Output:
[1, 4, 9, 16]
```
### `filter()` – select elements
```
nums = [1, 2, 3, 4, 5]
evens = list(filter(lambda x: x % 2 == 0, nums))

print(evens)

#Output:
[2, 4]
```
### `reduce()` – combine elements
```
from functools import reduce

nums = [1, 2, 3, 4]
total = reduce(lambda a, b: a + b, nums)

print(total)

#Output:
10
```

---
## 7. Lambda in Sorting

Very common real-world use:
```
students = [("Milad", 22), ("Faraz", 18), ("Mehrdad", 22)]

students.sort(key=lambda x: x[1])

print(students)

#Output:
[('Faraz', 18), ('Milad', 22), ('Mehrdad', 22)]
```
Sorts by age.

---
## 8. Lambda with `*args`
```
add_all = lambda *args: sum(args)
print(add_all(1, 2, 3, 4))

#Output:
10
```

---
## 9. When Should You Use Lambda?

✔ Use lambda when:

- Function is **simple**
    
- Used **once**
    
- Improves readability
    

❌ Avoid lambda when:

- Logic is complex
    
- Needs multiple steps
    
- Needs documentation or reuse

---
## 10. Common Mistakes

❌ Trying to use multiple statements:
```
lambda x: print(x); x + 1
```
❌ Using lambda for complex logic (bad practice)

✔ Use `def` instead.

---
## 11. Exam-Friendly Definition

> A lambda function is an anonymous, one-line function defined using the `lambda` keyword that can take any number of arguments but only one expression.