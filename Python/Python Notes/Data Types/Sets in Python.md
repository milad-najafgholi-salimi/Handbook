A **set** is an **unordered** collection of **unique elements**.

- **Unordered**: You can’t rely on the order of items in a set. When you print a set, the order of the elements may not be the same as when you created it.
    
- **Unique elements**: A set automatically **removes duplicates**. Only one instance of each element is stored.
    
- **Mutable**: You can add and remove elements, but you cannot change an element once it’s in the set (because they are unordered).
    

### Example:
```
my_set = {1, 2, 3, 4}
```

---
## Key Properties of Sets

- **Unordered**: No index, no order.
    
- **Mutable**: Can add/remove elements.
    
- **Unique**: No duplicates allowed.
    
- **No indexing or slicing**: Since sets are unordered, you can’t access elements via indexing.
    
- **Contains hashable (immutable) elements**: Sets cannot contain mutable objects like lists or other sets.

---
## Creating a Set

### a. Using curly braces `{ }`
```
my_set = {1, 2, 3, 4}
```
### b. Using the `set()` constructor
```
my_set = set([1, 2, 3, 4])   # Creates a set from a list
```
### c. Empty set (important note)
```
empty_set = set()   # An empty set, not {}
```
**Note**: `{}` creates an empty dictionary, not a set.

---
## Basic Set Operations

### a. Adding elements (`add()`)
```
my_set = {1, 2, 3}
my_set.add(4)       # Add 4 to the set
print(my_set)       # {1, 2, 3, 4}
```
### b. Removing elements (remove() or discard())
```
my_set.remove(2)    # Removes 2, raises KeyError if not found
my_set.discard(5)   # Removes 5 if it exists, does nothing if not found
print(my_set)       # {1, 3, 4}
```
### c. Popping elements (pop())
```
removed_element = my_set.pop()  # Removes and returns an arbitrary element (since the set is unordered)
print(removed_element)          # Randomly removed element
print(my_set)
```
### d. Clearing all elements (`clear()`)
```
my_set.clear()    # Empties the set
print(my_set)     # set()
```

---
## Set Operations (Mathematical Set Operations)
### a. Union (| or union())

The union of two sets combines all unique elements from both sets.
```
set1 = {1, 2, 3}
set2 = {3, 4, 5}

union_set = set1 | set2      # {1, 2, 3, 4, 5}
# or
union_set = set1.union(set2) # {1, 2, 3, 4, 5}
```
### b. Intersection (`&` or `intersection()`)

The intersection of two sets gives the **common elements** between them.
```
set1 = {1, 2, 3}
set2 = {3, 4, 5}

intersection_set = set1 & set2      # {3}
# or
intersection_set = set1.intersection(set2)  # {3}
```
### c. Difference (`-` or `difference()`)

The difference gives the elements that are in the first set but not in the second.
```
set1 = {1, 2, 3}
set2 = {3, 4, 5}

difference_set = set1 - set2      # {1, 2}
# or
difference_set = set1.difference(set2)  # {1, 2}
```
### d. Symmetric Difference (`^` or `symmetric_difference()`)

The symmetric difference gives the elements that are in **either of the sets**, but not in **both**.
```
set1 = {1, 2, 3}
set2 = {3, 4, 5}

symmetric_difference_set = set1 ^ set2      # {1, 2, 4, 5}
# or
symmetric_difference_set = set1.symmetric_difference(set2)  # {1, 2, 4, 5}
```

---
## 6. Set Membership Test
You can check if an element is in a set using the `in` keyword:
```
my_set = {1, 2, 3, 4}

print(3 in my_set)   # True
print(5 in my_set)   # False
```

---
## Set Iteration
You can loop through a set, but remember that since sets are unordered, the order of the elements may not be the same each time.
```
my_set = {1, 2, 3, 4}

for element in my_set:
    print(element)
```

---
## Set Comprehensions

Just like list comprehensions, Python supports **set comprehensions** to create sets based on existing sequences or conditions.
```
# Create a set of squares of numbers from 1 to 5
squares = {x**2 for x in range(1, 6)}
print(squares)    # {1, 4, 9, 16, 25}
```

---
## One-Liner Exam Definition

> **A set is an unordered, mutable collection of unique elements, used for operations like union, intersection, and difference.**

---
## Common Mistakes with Sets

- **Trying to access elements by index**:
```
my_set = {1, 2, 3}
print(my_set[0])  # ERROR! Sets are unordered and cannot be indexed
```
**Confusing set syntax**:
```
{} creates an empty dictionary, not a set.
```
**Trying to add mutable elements**:  
Sets can’t contain mutable (unhashable) types, like lists or other sets:
```
my_set = {1, [2, 3]}  # ERROR! Lists cannot be elements of a set
```

---
## Real-World Use Cases for Sets

- **Removing duplicates**: A set automatically removes duplicates.
```
nums = [1, 2, 3, 1, 2, 4]
unique_nums = set(nums)  # {1, 2, 3, 4}
```
- **Membership tests**: Sets are ideal for fast membership testing (using `in`).
    
- **Mathematical set operations**: Sets are naturally suited for operations like union, intersection, and difference, making them useful in problems involving **sets** of data.