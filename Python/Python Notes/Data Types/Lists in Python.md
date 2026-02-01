A **list** is a built-in Python data structure used to store **multiple values in a single variable**.

Formally, a list is:

- **Ordered** → elements have a fixed position
    
- **Mutable** → elements can be changed
    
- **Indexed** → elements are accessed by index
    
- **Heterogeneous** → can store different data types
    

Example:
```
my_list = [10, 20, 30]
another_list = ["apple", 3.5, True]
```
---

## Creating lists

### a. Using square brackets `[]`
```
numbers = [1, 2, 3, 4]
empty = []
```
b. Using the `list()` constructor
```
chars = list("python")     # ['p', 'y', 't', 'h', 'o', 'n']
nums = list(range(5))      # [0, 1, 2, 3, 4]
```

---
## Accessing elements (indexing)

Indexes start at **0**.
```
letters = ['a', 'b', 'c', 'd']

letters[0]    # 'a'
letters[2]    # 'c'
```
Negative indexing
```
letters[-1]   # 'd'
letters[-2]   # 'c'
```

---
## Slicing lists

Slicing allows you to extract **sub-lists**.

Syntax:
```
list[start : stop : step]
```
Examples:
```
nums = [0, 1, 2, 3, 4, 5]

nums[1:4]     # [1, 2, 3]
nums[:3]      # [0, 1, 2]
nums[::2]     # [0, 2, 4]
nums[::-1]    # reversed list
```
🔑 **Important:** Slicing returns a **new list**, not a reference.

---
## Lists are mutable (key concept)

You can change a list after creating it.
```
values = [1, 2, 3]
values[1] = 99
# [1, 99, 3]
```

---
## Adding elements to a list
```
nums = [1, 2, 3]

nums.append(4)        # adds to the end
nums.insert(1, 10)    # inserts at index 1
nums.extend([5, 6])   # adds multiple elements
```

---
## Removing elements
```
nums.remove(10)   # removes first occurrence of 10
nums.pop()        # removes last element
nums.pop(1)       # removes element at index 1
del nums[0]       # deletes element at index 0
```

---
## Common list methods (exam favorites)
```
nums = [3, 1, 4, 1, 5]

nums.sort()           # sorts in place
sorted(nums)          # returns new sorted list

nums.reverse()        # reverses list
nums.count(1)         # number of occurrences of 1
nums.index(4)         # index of first 4
nums.clear()          # empties the list
```

---
## Iterating over lists
#### Simple loop
```
for x in nums:
    print(x)
```
#### With index
```
for i, x in enumerate(nums):
    print(i, x)
```
## What is `enumerate`?

`enumerate()` is a **built-in Python function** that lets you loop over a sequence **while keeping track of both**:

- the **index** (position)
    
- the **value** (element)
    

In simple words:

> **`enumerate` gives you (index, value) pairs while looping.**

## Why do we need `enumerate`?

### Without `enumerate` (older / clumsier way)
```
nums = [10, 20, 30]

for i in range(len(nums)):
    print(i, nums[i])
```
Problems:

- Harder to read
    
- More error-prone
    
- Less “Pythonic”

## 3. What exactly does `enumerate(nums)` return?

It returns an **iterator of tuples**:
```
(0, nums[0]), (1, nums[1]), (2, nums[2]), ...
```
Example:
```
list(enumerate(['a', 'b', 'c']))
```
Output:
```
[(0, 'a'), (1, 'b'), (2, 'c')]
```
So when you write:
```
for i, x in enumerate(nums):
```
Python is doing **tuple unpacking**:
```
i, x = (index, value)
```


---
## List comprehensions (very important)
A compact way to create lists.

### Basic form:
```
[expression for item in iterable]
```
Example:
```
squares = [x**2 for x in range(6)]
```
With condition:
```
evens = [x for x in range(10) if x % 2 == 0]
```

---
## Nested lists
Lists can contain other lists.
```
matrix = [
    [1, 2],
    [3, 4],
    [5, 6]
]

matrix[2][1]   # 6
```

---
## Copying lists (common mistake)
Assignment copies the reference
```
a = [1, 2, 3]
b = a

b.append(4)
# a is now [1, 2, 3, 4]
```
Proper copy
```
b = a.copy()
# or
b = a[:]
```

---
## When should you use lists?

Use lists when:

- You need **ordered data**
    
- You want to **modify elements**
    
- You need **index-based access**
    
- The size of data may change

