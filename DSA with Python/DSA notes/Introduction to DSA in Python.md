**DSA (Data Structures and Algorithms)** in Python refers to the study and implementation of efficient ways to organize, store, and process data using the Python programming language.

---
## What is DSA?

DSA is made up of two main parts:

### 1. Data Structures

Data structures are ways of organizing and storing data so that it can be accessed and modified efficiently.

Common data structures in Python include:

- Lists (Dynamic arrays)
    
- Tuples
    
- Stacks
    
- Queues
    
- Linked Lists
    
- Trees
    
- Graphs
    
- Hash Tables (Dictionaries)
    
- Heaps
    

For example, a Python list can be used as a stack:
```
stack = []
stack.append(10)
stack.append(20)
print(stack.pop())  # Output: 20
```
### 2. Algorithms

Algorithms are step-by-step procedures or instructions used to solve a specific problem.

Common algorithms include:

- Searching
    
- Sorting
    
- Recursion
    
- Dynamic Programming
    
- Greedy Algorithms
    
- Graph Algorithms
---

## How Python Supports DSA Learning

Python allows quick implementation of complex structures. For example:

- Dictionaries → Hash Maps
    
- Lists → Dynamic Arrays
    
- `heapq` → Priority Queues
    
- `collections` → Advanced data structures
    

Example of a queue using deque:
```
from collections import deque

queue = deque()
queue.append(1)
queue.append(2)
print(queue.popleft())  # Output: 1
```
