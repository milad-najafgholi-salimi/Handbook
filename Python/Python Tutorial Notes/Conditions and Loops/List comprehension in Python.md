**List comprehension** in Python is a **compact and readable way to create lists** using a single line of code instead of a full loop. It is widely used because it makes code **shorter, clearer, and more “Pythonic.”**

---
## 1. What is list comprehension?

A **list comprehension** is a concise way to create a new list by:

- Iterating over an iterable
    
- Optionally applying a condition
    
- Optionally transforming each element
    

### General syntax
```
[expression for item in iterable if condition]
```
- **`expression`** → what you put into the new list
    
- **`item`** → each element from the iterable
    
- **`condition`** → optional filter

---
## 2. Basic example (without condition)

### Normal `for` loop
```
squares = []
for i in range(1, 6):
    squares.append(i * i)
```
### List comprehension version
```
squares = [i * i for i in range(1, 6)]
```
Result:
```
[1, 4, 9, 16, 25]
```
✔ Same result, less code, easier to read

---
## 3. List comprehension with condition (`if`)

#### Example: get only even numbers
```
evens = [i for i in range(1, 11) if i % 2 == 0]
```
**Result:**
```
[2, 4, 6, 8, 10]
```
Explanation:

- Loop through numbers 1–10
    
- Add only those that satisfy the condition

---
## 4. Transforming data

#### Example: convert strings to uppercase
```
names = ["Milad", "Faraz", "Mehrdad"]

upper_names = [name.upper() for name in names]

print(upper_names)
```
Result:
```
['MILAD', 'FARAZ', 'MEHRDAD']
```

---
## 5. `if–else` in list comprehension

⚠️ Different from filtering `if`

### Syntax
```
[expression_if_true if condition else expression_if_false for item in iterable]
```
#### Example:
```
numbers = [1, 2, 3, 4, 5]

result = ["even" if n % 2 == 0 else "odd" for n in numbers]

print(result)
```
Result:
```
['odd', 'even', 'odd', 'even', 'odd']
```

---
## 6. Nested list comprehensions

Used with matrices or nested loops.

#### Example: create pairs
```
pairs = [(i, j) for i in range(1, 3) for j in range(1, 4)]
```
Equivalent to:
```
pairs = []
for i in range(1, 3):
    for j in range(1, 4):
        pairs.append((i, j))
```

---
## 7. List comprehension with strings

Example: extract vowels
```
word = "education"

vowels = [ch for ch in word if ch in "aeiou"]
```
Result:
```
['e', 'u', 'a', 'i', 'o']
```

---
## 8. When NOT to use list comprehension ❌

Avoid list comprehension when:

- The logic is too complex
    
- Multiple conditions make it hard to read
    
- You need many statements inside the loop
    

Readable code is **better than short code**.

---
## 9. Common mistakes

### ❌ Forgetting square brackets
```
i * i for i in range(5)   # wrong
```
✔ Correct:
```
[i * i for i in range(5)]
```
### ❌ Confusing filter `if` with `if–else`
```
[i if i % 2 == 0 for i in range(5)]   # wrong
```
✔ Correct:
```
[i if i % 2 == 0 else 0 for i in range(5)]
```

---
## 10. Comparison: loop vs list comprehension
| Feature        | `for` loop              | List comprehension     |
| -------------- | ----------------------- | ---------------------- |
| Length         | Longer                  | Short                  |
| Readability    | Clear for complex logic | Clear for simple logic |
| Speed          | Slightly slower         | Slightly faster        |
| Pythonic style | Normal                  | Preferred              |

---
## 11. Teaching tip (math education context)

List comprehension is excellent for:

- Generating sequences
    
- Creating tables
    
- Applying formulas to data
    

Example:
```
y_values = [2*x + 1 for x in range(-3, 4)]
```

---
### Quick summary

- List comprehension creates lists in **one line**
    
- Syntax: `[expression for item in iterable if condition]`
    
- Use it for **simple, readable transformations**