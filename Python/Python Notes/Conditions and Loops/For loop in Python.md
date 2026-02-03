In Python, the **`for` loop** is used to **iterate over a sequence** (or any iterable) and execute a block of code once for each item.

---
## 1. Basic idea of a `for` loop

The general syntax is:
```
for variable in iterable:
    # code to execute for each item
```
- **`variable`**: takes the value of each item in the sequence, one at a time
    
- **`iterable`**: something you can loop over (list, string, tuple, dictionary, range, etc.)
#### Example:
```
for number in [1, 2, 3, 4]:
    print(number)
```
**Output:**
```
1
2
3
4
```
Here:

- Python goes through the list item by item
    
- Each time, `number` holds the current value

---
## 2. `for` loop with `range()`

`range()` is very commonly used with `for` loops.
```
for i in range(5):
    print(i)
```
**Output:**
```
0
1
2
3
4
```
Key points:

- `range(5)` generates numbers from `0` to `4`
    
- The upper limit is **not included**

### Variations of `range()`
```
range(start, stop)
range(start, stop, step)
```
#### Example:
```
for i in range(1, 10, 2):
    print(i)
```
**Output:**
```
1
3
5
7
9
```

---
## 3. Looping over different data types

### a) Strings
```
for char in "Python":
    print(char)
```
- Each iteration gives one character.

**Output:**
```
P
y
t
h
o
n
```

### b) Tuples
```
for item in (10, 20, 30):
    print(item)
```
- Tuples work just like lists in loops.

**Output:**
```
10
20
30
```

### c) Dictionaries

There are several ways to loop through dictionaries:
```
student = {"name": "Milad", "age": 22, "grade": "A"}
```
**Keys only (default):**
```
for key in student:
    print(key)
```
_Output:_
```
name
age
grade
```
**Values:**
```
for value in student.values():
    print(value)
```
_Output:_
```
Milad
22
A
```
**Key–value pairs:**
```
for key, value in student.items():
    print(key, value)
```
_Output:_
```
name Milad
age 22
grade A
```

---
## 4. Using `for` with `if` (filtering)

You can add conditions inside a loop:
```
for number in range(1, 11):
    if number % 2 == 0:
        print(number)
```
This prints only even numbers.
_Output:_
```
2
4
6
8
10
```

---
## 5. `break` and `continue`

### `break` – stop the loop completely
```
for i in range(10):
    if i == 5:
        break
    print(i)
```
Stops when `i` becomes 5.

_Output:_
```
0
1
2
3
4
```
>**Point:** in the *nested for loops*, if _break_ used in inner loop, the inner loop will be stops and the outer *for loop* will continue until the end.

---
### `continue` – skip the current iteration
```
for i in range(5):
    if i == 2:
        continue
    print(i)
```
Skips printing `2`.

_Output:_
```
0
1
3
4
```

---
## 6. `else` with a `for` loop

Python has a unique feature: **`for-else`**.
```
for i in range(5):
    print(i)
else:
    print("Loop finished normally")
```
The `else` block:

- Runs **only if the loop is not stopped by `break`**
    

This is often used in searching problems.

---
## 7. Nested `for` loops

A loop inside another loop:
```
for i in range(3):
    for j in range(2):
        print(i, j)
```
Useful for:

- Matrices
    
- Tables
    
- Patterns

_Output:_
```
0 0
0 1
1 0
1 1
2 0
2 1
```

---
## 8. Common Pythonic patterns

### Using `enumerate()` (index + value)
```
colors = ["red", "green", "blue"]

for index, color in enumerate(colors):
    print(index, color)
```
_Output:_
```
0 red
1 green
2 blue
```
### Using `zip()` (looping over multiple sequences)
```
names = ["Milad", "Faraz", "Mehrdad"]
scores = [85, 90, 78]

for name, score in zip(names, scores):
    print(name, score)
```
_Output:_
```
Milad 85
Faraz 90
Mehrdad 78
```

---
## 9. Why Python `for` loops are special

- Python’s `for` loop **does not count** like in C/Java
    
- It **iterates over objects**, not numbers
    
- Cleaner and less error-prone