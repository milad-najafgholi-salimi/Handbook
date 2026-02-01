A **tuple** is a **collection** of elements, like a list, but unlike lists, **tuples are immutable**. This means once you create a tuple, **you cannot change its elements**.

You can think of it like a **read-only list** or an **immutable sequence**.

### Syntax:

Tuples are created by placing elements inside **parentheses** `( )`, separated by commas.

Example:
```
my_tuple = (1, 2, 3)
```

---
## Key Properties of Tuples

- **Ordered**: The order of elements is preserved.
    
- **Immutable**: Once created, **cannot be changed** (no adding, removing, or changing elements).
    
- **Indexable**: You can access elements using their **index**.
    
- **Heterogeneous**: You can store **different data types** in a tuple.
    
- **Can be nested**: Tuples can contain other tuples or collections.

---
## Creating Tuples

### a. Basic tuple
```
t = (1, 2, 3)
```
### b. Single-element tuple (Note the comma!)
```
single_element = (10,)   # This is a tuple with one element
```
Without the comma, it’s just a regular value:
```
not_a_tuple = (10)       # This is just the integer 10
```
### c. Empty tuple
```
empty_tuple = ()         # Empty tuple
```

---
## Accessing Tuple Elements (Indexing)

Like lists, you can **access individual elements** in a tuple using **indexing** (starting from 0).
```
t = (10, 20, 30)

print(t[0])    # 10
print(t[1])    # 20
print(t[2])    # 30
```
### Negative Indexing:

You can also index from the **end** of the tuple:
```
print(t[-1])   # 30
print(t[-2])   # 20
```

---
## 5. Slicing Tuples

Just like with lists, **slicing** allows you to get a **subtuple**.

Syntax: `tuple[start:stop:step]`
```
t = (0, 1, 2, 3, 4, 5)

# Get elements from index 1 to 3 (not including 3)
print(t[1:3])   # (1, 2)

# Get every second element
print(t[::2])   # (0, 2, 4)
```

---
## 6. Modifying Tuples

### a. You **cannot change elements** once a tuple is created.

For example:
```
t = (10, 20, 30)

# This will raise an error:
# t[1] = 99      # TypeError: 'tuple' object does not support                        item assignment
```
### b. But you **can create a new tuple** from parts of an old one.
```
t = (10, 20, 30)
new_t = t + (40, 50)   # Concatenation, creating a new tuple
print(new_t)            # (10, 20, 30, 40, 50)
```

---
## Tuple Methods

Tuples have very **few methods** because they are immutable, but they still have some useful ones:
```
t = (1, 2, 3, 1, 4)

print(t.count(1))    # 2 (counts how many times 1 appears)
print(t.index(4))    # 4 (returns the index of the first                                    ############## occurrence of 4)
```

---
### **When to use a tuple over a list**:

- If your data should not change after creation (i.e., read-only data).
    
- Tuples are generally **faster** than lists for iteration or access.
    
- When you want to **use the tuple as a dictionary key** (since tuples are hashable, while lists are not).

---
## Tuple Packing and Unpacking

### a. Packing:

You can group values into a tuple without explicitly using parentheses.
```
t = 10, 20, 30   # This is a tuple (10, 20, 30)
```
### b. Unpacking:

You can extract values from a tuple into variables.
```
t = (10, 20, 30)

x, y, z = t    # Unpacking
print(x)       # 10
print(y)       # 20
print(z)       # 30
```
If the number of variables doesn’t match the number of elements, Python will raise a `ValueError`.
```
# This will raise an error
a, b = (10, 20, 30)  # ValueError: too many values to unpack
```

---
## Nested Tuples

Tuples can also contain other tuples, or even other complex data structures.
```
nested_tuple = ((1, 2), (3, 4), (5, 6))

# Accessing nested elements
print(nested_tuple[0])      # (1, 2)
print(nested_tuple[0][1])   # 2
```

---
## Immutability & Practical Use Cases

### **Why immutability matters:**

- Tuples **cannot be changed** after they’re created, making them a good choice for **constant data**.
    
- They can be used as keys in dictionaries, while lists cannot, because only **immutable types** are hashable.

Example use case:
```
coordinates = (10, 20)   # Fixed, unchangeable
locations = {coordinates: "Home"}   # This works because tuples are hashable
```

---
## One-liner Exam Definition

> **A tuple is an ordered, immutable collection of elements, accessed via indexing and used for storing fixed, unchangeable data.**

---
## Common Mistakes with Tuples

- **Trying to modify a tuple** (because they are immutable):
```
t = (1, 2, 3)
t[0] = 100   # Error: TypeError: 'tuple' object does not support item assignment
```
**Confusing tuple and list syntax**:  
Remember that **a single value tuple** needs a trailing comma:
```
t = (10,)  # Correct single-item tuple
```
