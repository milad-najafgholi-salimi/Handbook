## What is Time Complexity?

Time complexity is a way to measure how the runtime of an algorithm grows as the input size increases. It's expressed using **Big O notation**, which describes the upper bound of growth.

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
## Visual Examples in Python

### O(1) - Constant Time
```
def get_first_element(arr):
    return arr[0]  # Always takes same time regardless of array size

# Even if arr has 1 or 1 million elements, operation is constant
```
### O(log n) - Logarithmic Time
```
def binary_search(arr, target):
    left, right = 0, len(arr) - 1
    
    while left <= right:  # Each iteration halves the search space
        mid = (left + right) // 2
        if arr[mid] == target:
            return mid
        elif arr[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
    return -1
```
### O(n) - Linear Time
```
def find_max(arr):
    max_val = arr[0]
    for num in arr:  # Loop runs n times
        if num > max_val:
            max_val = num
    return max_val
```
### O(n²) - Quadratic Time
```
def print_pairs(arr):
    for i in range(len(arr)):      # n times
        for j in range(len(arr)):  # n times for each i
            print(arr[i], arr[j])  # Total: n * n operations
```

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
## Common Pitfalls

### Hidden Complexities
```
# Inefficient string concatenation
def build_string_bad(words):
    result = ""
    for word in words:      # O(n) iterations
        result += word      # O(n) each time due to immutability
    return result
# Total: O(n²)

# Efficient approach
def build_string_good(words):
    return "".join(words)   # O(n)
```
### Recursive Complexity
```
# Exponential time - BAD
def fib_bad(n):
    if n <= 1:
        return n
    return fib_bad(n-1) + fib_bad(n-2)  # O(2ⁿ)

# Linear time - GOOD
def fib_good(n):
    if n <= 1:
        return n
    a, b = 0, 1
    for _ in range(2, n + 1):  # O(n)
        a, b = b, a + b
    return b
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

## Tips for Interview Preparation

1. **Always consider input size**: What works for n=10 might fail for n=10^6
    
2. **Look for nested loops**: Usually indicate O(n²) or worse
    
3. **Binary search pattern**: Often indicates O(log n)
    
4. **Divide and conquer**: Often O(n log n)
    
5. **Space-time tradeoff**: Sometimes using more memory can improve time complexity

>**Remember:** Time complexity helps you choose the right algorithm for your specific constraints and input sizes!

