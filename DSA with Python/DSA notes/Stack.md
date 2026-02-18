A **stack** is a linear data structure that follows the **LIFO (Last In, First Out)** principle.

### Key Characteristics:

- **LIFO Order**: The last element added is the first one removed
    
- **Two Main Operations**: Push (add) and Pop (remove)
    
- **Limited Access**: Can only access the top element
    

### Basic Operations:

- **push(item)**: Add an element to the top
    
- **pop()**: Remove and return the top element
    
- **peek()/top()**: View the top element without removing it
    
- **is_empty()**: Check if stack is empty
    
- **size()**: Get number of elements
    

## Implementation in Python

### Method 1: Using List (Most Common)
```
class Stack:
    def __init__(self):
        self.items = []
    
    def push(self, item):
        """Add item to the top of stack"""
        self.items.append(item)
    
    def pop(self):
        """Remove and return top item"""
        if not self.is_empty():
            return self.items.pop()
        return None
    
    def peek(self):
        """Return top item without removing"""
        if not self.is_empty():
            return self.items[-1]
        return None
    
    def is_empty(self):
        """Check if stack is empty"""
        return len(self.items) == 0
    
    def size(self):
        """Return number of items"""
        return len(self.items)
    
    def display(self):
        """Display stack contents"""
        print(f"Stack: {self.items}")

# Example usage
stack = Stack()
stack.push(10)
stack.push(20)
stack.push(30)
stack.display()  # Stack: [10, 20, 30]
print(f"Popped: {stack.pop()}")  # Popped: 30
print(f"Top: {stack.peek()}")    # Top: 20
print(f"Size: {stack.size()}")    # Size: 2
```
### Method 2: Using collections.deque (More Efficient for Large Stacks)
```
from collections import deque

class StackDeque:
    def __init__(self):
        self.items = deque()
    
    def push(self, item):
        self.items.append(item)
    
    def pop(self):
        if not self.is_empty():
            return self.items.pop()
        return None
    
    def peek(self):
        if not self.is_empty():
            return self.items[-1]
        return None
    
    def is_empty(self):
        return len(self.items) == 0
    
    def size(self):
        return len(self.items)

# Example
stack = StackDeque()
stack.push(5)
stack.push(15)
stack.push(25)
print(stack.pop())  # 25
```

---
## Common Stack Problems & Solutions

### 1. Balanced Parentheses Check
```
def is_balanced(expression):
    """Check if parentheses are balanced"""
    stack = []
    pairs = {')': '(', '}': '{', ']': '['}
    
    for char in expression:
        if char in '({[':
            stack.append(char)
        elif char in ')}]':
            if not stack or stack.pop() != pairs[char]:
                return False
    
    return len(stack) == 0

# Test
print(is_balanced("({[]})"))  # True
print(is_balanced("({[})"))    # False
```
### 2. Reverse String Using Stack
```
def reverse_string(text):
    """Reverse a string using stack"""
    stack = []
    
    # Push all characters
    for char in text:
        stack.append(char)
    
    # Pop all characters
    reversed_text = ''
    while stack:
        reversed_text += stack.pop()
    
    return reversed_text

print(reverse_string("hello"))  # "olleh"
```
### 3. Evaluate Postfix Expression
```
def evaluate_postfix(expression):
    """Evaluate postfix expression"""
    stack = []
    
    for token in expression.split():
        if token.isdigit():
            stack.append(int(token))
        else:
            b = stack.pop()
            a = stack.pop()
            
            if token == '+':
                stack.append(a + b)
            elif token == '-':
                stack.append(a - b)
            elif token == '*':
                stack.append(a * b)
            elif token == '/':
                stack.append(a / b)
    
    return stack.pop()

print(evaluate_postfix("3 4 + 2 *"))  # (3+4)*2 = 14
```

---
## Time Complexity
|Operation|Time Complexity|
|---|---|
|push()|O(1)|
|pop()|O(1)|
|peek()|O(1)|
|is_empty()|O(1)|
|size()|O(1)|

## Real-World Applications

1. **Function Call Stack** - Managing function calls in programming
    
2. **Undo/Redo Operations** - In text editors and applications
    
3. **Browser History** - Back/forward navigation
    
4. **Expression Evaluation** - Converting and evaluating mathematical expressions
    
5. **Backtracking Algorithms** - Maze solving, puzzle games
    
6. **Syntax Parsing** - Checking balanced parentheses in code
    

## When to Use Stacks

✅ **Use Stack when:**

- You need LIFO behavior
    
- Implementing undo/redo functionality
    
- Parsing expressions
    
- Performing depth-first search
    
- Reversing data
    

❌ **Avoid Stack when:**

- You need random access to elements
    
- FIFO behavior is required (use Queue)
    
- You frequently need to access middle elements
    
---
## Advanced Example: Min Stack (Track Minimum Element)
```
class MinStack:
    """Stack that can return minimum element in O(1)"""
    def __init__(self):
        self.stack = []
        self.min_stack = []
    
    def push(self, val):
        self.stack.append(val)
        if not self.min_stack or val <= self.min_stack[-1]:
            self.min_stack.append(val)
    
    def pop(self):
        if self.stack:
            val = self.stack.pop()
            if val == self.min_stack[-1]:
                self.min_stack.pop()
            return val
        return None
    
    def get_min(self):
        if self.min_stack:
            return self.min_stack[-1]
        return None

# Example
min_stack = MinStack()
min_stack.push(5)
min_stack.push(2)
min_stack.push(7)
print(min_stack.get_min())  # 2
```
Stacks are fundamental data structures that appear in many algorithms and real-world applications. Understanding them well is crucial for any programmer!