## What is Time Complexity?

Time complexity is a way to measure how the runtime of an algorithm grows as the input size increases. It's expressed using **Big O notation**, which describes the upper bound of growth.

---
## Big-O Notation (O) Vs. Big-Theta Notation (Θ) Vs. Big-Omega Notation (Ω)
### 1. Big-O Notation (O) – The "Upper Bound" (Worst Case)

- **What it means:** This is the **maximum** time (or space) an algorithm will ever take. It is the "ceiling."
    
- **The Analogy:** If you are driving, Big-O is the **speed limit**. You will not go faster than this (in the worst case).
    
- **Why we use it:** It guarantees your code won't blow up, even with massive input. This is what most people mean when they say "complexity."
### 2. Big-Theta Notation (Θ) – The "Tight Bound" (Exact Average)

- **What it means:** This means the algorithm is **both** O(f(n)) **and** Ω(f(n)) at the same time. The upper and lower bounds match.
    
- **The Analogy:** If Big-O is the speed limit and Omega is the minimum speed, Theta is your **cruise control**. You are driving exactly at that speed most of the time.
    
- **Why we use it:** It gives the most mathematically precise description of an algorithm's growth because it tells you exactly how it behaves for _all_ inputs of size `n`.
### 3. Big-Omega Notation (Ω) – The "Lower Bound" (Best Case)

- **What it means:** This is the **minimum** time an algorithm will ever take. It is the "floor."
    
- **The Analogy:** If Big-O is the speed limit, Big-Omega is the **minimum speed limit** on the highway (you will always go at least this fast).
    
- **Why we use it:** It tells you the best-case scenario. It’s useful for knowing the absolute fastest your algorithm can run, but it’s usually less useful for practical performance because best cases are rare.
---
## Common Time Complexities (from fastest to slowest)
|Notation|Name|Description|Example|
|---|---|---|---|
|**O(1)**|Constant|Time doesn't depend on input size|Accessing array element|
|**O(log n)**|Logarithmic|Time grows slowly as input increases|Binary Search|
|**O(n)**|Linear|Time grows proportionally to input|Simple loop|
|**O(n log n)**|Linearithmic|Common in efficient sorting|Merge Sort, Quick Sort|
|**O(n²)**|Quadratic|Time grows quadratically|Nested loops|
|**O(2ⁿ)**|Exponential|Very slow growth|Recursive Fibonacci|
|**O(n!)**|Factorial|Extremely slow|Permutations|

---
## Python-Specific Considerations

### List Operations Complexity
```
# Access by index: O(1)
arr = [1, 2, 3, 4, 5]
x = arr[3]  # O(1)

# Append: O(1) amortized
arr.append(6)  # Usually O(1), occasionally O(n) when resizing

# Insert/Delete at beginning: O(n)
arr.insert(0, 0)  # Shifts all elements

# Search: O(n)
if 5 in arr:  # Linear search
    print("Found")

# Slice: O(k) where k is slice length
subarray = arr[1:4]  # O(3)
```
### Dictionary/Set Operations
```
# Insert/Lookup/Delete: Average O(1), Worst O(n)
d = {}
d["key"] = "value"  # O(1) average
x = d["key"]        # O(1) average
del d["key"]        # O(1) average

# Set operations similarly efficient
s = {1, 2, 3}
if 2 in s:  # O(1) average
    print("Found")
```

---
## How to Analyze Time Complexity

### 1. Count the operations
```
def sum_array(arr):
    total = 0           # O(1)
    for num in arr:     # O(n)
        total += num    # O(1) per iteration
    return total        # O(1)
# Total: O(1 + n*1 + 1) = O(n)
```
> The interconnected parts of the code that are related to each other and cause errors without that code must be multiplied, and the parts of the code that are separate and isolated must be added to obtain the time complexity.

### 2. Drop constants and lower-order terms
```
def example(n):
    for i in range(n):        # O(n)
        print(i)              # O(1)
    
    for j in range(n):        # O(n)
        for k in range(n):    # O(n)
            print(j, k)       # O(1)
# Total: O(n + n²) = O(n²)
```
### 3. Consider worst case
```
def find_element(arr, target):
    for num in arr:        # O(n) in worst case
        if num == target:  # (target at end or not present)
            return True
    return False
```

---
## Quick Reference Table
|Data Structure|Access|Search|Insert|Delete|
|---|---|---|---|---|
|Array (List)|O(1)|O(n)|O(n)*|O(n)*|
|Stack|O(n)|O(n)|O(1)|O(1)|
|Queue|O(n)|O(n)|O(1)|O(1)|
|Hash Table|N/A|O(1)**|O(1)**|O(1)**|
|Binary Tree|O(n)|O(n)|O(n)|O(n)|
|BST (balanced)|O(log n)|O(log n)|O(log n)|O(log n)|

*At beginning/end: append/pop are O(1) amortized  
**Average case; worst case O(n)
