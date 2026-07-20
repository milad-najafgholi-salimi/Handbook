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

### Method 1: Using List (Most Common) - Class way & Simple way:
#### Simple way:
```
stack = []

# Push
stack.append('A')
stack.append('B')
stack.append('C')
print("Stack: ", stack)

# Peek
topElement = stack[-1]
print("Peek: ", topElement)

# Pop
poppedElement = stack.pop()
print("Pop: ", poppedElement)

# Stack after Pop
print("Stack after Pop: ", stack)

# isEmpty
isEmpty = not bool(stack)
print("isEmpty: ", isEmpty)

# Size
print("Size: ",len(stack))

# Output:
Stack: ['A', 'B', 'C']  
Peek: C  
Pop: C  
Stack after Pop: ['A', 'B']  
isEmpty: False  
Size: 2
```
#### Class way - Better functionality:

```
class Stack:
  def __init__(self):
    self.stack = []

  def push(self, element):
    self.stack.append(element)

  def pop(self):
    if self.isEmpty():
      return "Stack is empty"
    return self.stack.pop()

  def peek(self):
    if self.isEmpty():
      return "Stack is empty"
    return self.stack[-1]

  def isEmpty(self):
    return len(self.stack) == 0

  def size(self):
    return len(self.stack)

# Create a stack
myStack = Stack()

myStack.push('A')
myStack.push('B')
myStack.push('C')

print("Stack: ", myStack.stack)
print("Pop: ", myStack.pop())
print("Stack after Pop: ", myStack.stack)
print("Peek: ", myStack.peek())
print("isEmpty: ", myStack.isEmpty())
print("Size: ", myStack.size())

# Outpu:
Stack: ['A', 'B', 'C']  
Pop: C  
Stack after Pop: ['A', 'B']  
Peek: B  
isEmpty: False  
Size: 2
```

Reasons to implement stacks using lists/arrays:

- **Memory Efficient:** Array elements do not hold the next elements address like linked list nodes do.
- **Easier to implement and understand:** Using arrays to implement stacks require less code than using linked lists, and for this reason it is typically easier to understand as well.

A reason for **not** using arrays to implement stacks:

- **Fixed size:** An array occupies a fixed part of the memory. This means that it could take up more memory than needed, or if the array fills up, it cannot hold more elements.
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

---
## Stack Implementation using Linked Lists
A linked list consists of nodes with some sort of data, and a pointer to the next node.

A big benefit with using linked lists is that nodes are stored wherever there is free space in memory, the nodes do not have to be stored contiguously right after each other like elements are stored in arrays. Another nice thing with linked lists is that when adding or removing nodes, the rest of the nodes in the list do not have to be shifted.

Creating a Stack using a Linked List:
```
class Node:
  def __init__(self, value):
    self.value = value
    self.next = None

class Stack:
  def __init__(self):
    self.head = None
    self.size = 0

  def push(self, value):
    new_node = Node(value)
    if self.head:
      new_node.next = self.head
    self.head = new_node
    self.size += 1

  def pop(self):
    if self.isEmpty():
      return "Stack is empty"
    popped_node = self.head
    self.head = self.head.next
    self.size -= 1
    return popped_node.value

  def peek(self):
    if self.isEmpty():
      return "Stack is empty"
    return self.head.value

  def isEmpty(self):
    return self.size == 0

  def stackSize(self):
    return self.size

  def traverseAndPrint(self):
    currentNode = self.head
    while currentNode:
      print(currentNode.value, end=" -> ")
      currentNode = currentNode.next
    print()

myStack = Stack()
myStack.push('A')
myStack.push('B')
myStack.push('C')

print("LinkedList: ", end="")
myStack.traverseAndPrint()
print("Peek: ", myStack.peek())
print("Pop: ", myStack.pop())
print("LinkedList after Pop: ", end="")
myStack.traverseAndPrint()
print("isEmpty: ", myStack.isEmpty())
print("Size: ", myStack.stackSize())
```
A reason for using linked lists to implement stacks:

- **Dynamic size:** The stack can grow and shrink dynamically, unlike with arrays.

Reasons for **not** using linked lists to implement stacks:

- **Extra memory:** Each stack element must contain the address to the next element (the next linked list node).
- **Readability:** The code might be harder to read and write for some because it is longer and more complex.