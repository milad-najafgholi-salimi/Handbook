A **queue** is a linear data structure that follows the **FIFO (First In, First Out)** principle.

### Key Characteristics:

- **FIFO Order**: The first element added is the first one removed
    
- **Two Main Operations**: Enqueue (add) and Dequeue (remove)
    
- **Two Ends**: Front (for removal) and Rear (for addition)
    

### Basic Operations:

- **enqueue(item)**: Add an element to the rear
    
- **dequeue()**: Remove and return the front element
    
- **front()/peek()**: View the front element without removing it
    
- **is_empty()**: Check if queue is empty
    
- **size()**: Get number of elements
    
---
## Implementations in Python

### Method 1: Using List (Array) - Class way and simple way

#### Simple way:
```
queue = []

# Enqueue
queue.append('A')
queue.append('B')
queue.append('C')
print("Queue: ", queue)

# Peek
frontElement = queue[0]
print("Peek: ", frontElement)

# Dequeue
poppedElement = queue.pop(0)
print("Dequeue: ", poppedElement)

print("Queue after Dequeue: ", queue)

# isEmpty
isEmpty = not bool(queue)
print("isEmpty: ", isEmpty)

# Size
print("Size: ", len(queue))

# Output:
Queue: ['A', 'B', 'C']  
Peek: A  
Dequeue: A  
Queue after Dequeue: ['B', 'C']  
isEmpty: False  
Size: 2
```

#### Class way - Better functionality:
```
class Queue:
  def __init__(self):
    self.queue = []
    
  def enqueue(self, element):
    self.queue.append(element)

  def dequeue(self):
    if self.isEmpty():
      return "Queue is empty"
    return self.queue.pop(0)

  def peek(self):
    if self.isEmpty():
      return "Queue is empty"
    return self.queue[0]

  def isEmpty(self):
    return len(self.queue) == 0

  def size(self):
    return len(self.queue)

# Create a queue
myQueue = Queue()

myQueue.enqueue('A')
myQueue.enqueue('B')
myQueue.enqueue('C')

print("Queue: ", myQueue.queue)
print("Peek: ", myQueue.peek())
print("Dequeue: ", myQueue.dequeue())
print("Queue after Dequeue: ", myQueue.queue)
print("isEmpty: ", myQueue.isEmpty())
print("Size: ", myQueue.size())

# Output:
Queue: ['A', 'B', 'C']  
Peek: A  
Dequeue: A  
Queue after Dequeue: ['B', 'C']  
isEmpty: False  
Size: 2
```

**Note:** While using a list is simple, removing elements from the beginning (dequeue operation) requires shifting all remaining elements, making it less efficient for large queues.

## Queue Implementation using Linked Lists
A linked list consists of nodes with some sort of data, and a pointer to the next node.

A big benefit with using linked lists is that nodes are stored wherever there is free space in memory, the nodes do not have to be stored contiguously right after each other like elements are stored in arrays. Another nice thing with linked lists is that when adding or removing nodes, the rest of the nodes in the list do not have to be shifted.

#### Creating a Queue using a Linked List:
```
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

class Queue:
  def __init__(self):
    self.front = None
    self.rear = None
    self.length = 0

  def enqueue(self, element):
    new_node = Node(element)
    if self.rear is None:
      self.front = self.rear = new_node
      self.length += 1
      return
    self.rear.next = new_node
    self.rear = new_node
    self.length += 1

  def dequeue(self):
    if self.isEmpty():
      return "Queue is empty"
    temp = self.front
    self.front = temp.next
    self.length -= 1
    if self.front is None:
      self.rear = None
    return temp.data

  def peek(self):
    if self.isEmpty():
      return "Queue is empty"
    return self.front.data

  def isEmpty(self):
    return self.length == 0

  def size(self):
    return self.length

  def printQueue(self):
    temp = self.front
    while temp:
      print(temp.data, end=" -> ")
      temp = temp.next
    print()

# Create a queue
myQueue = Queue()

myQueue.enqueue('A')
myQueue.enqueue('B')
myQueue.enqueue('C')

print("Queue: ", end="")
myQueue.printQueue()
print("Peek: ", myQueue.peek())
print("Dequeue: ", myQueue.dequeue())
print("Queue after Dequeue: ", end="")
myQueue.printQueue()
print("isEmpty: ", myQueue.isEmpty())
print("Size: ", myQueue.size())

# Output:
Queue: A -> B -> C ->  
Peek: A  
Dequeue: A  
Queue after Dequeue: B -> C ->  
isEmpty: False  
Size: 2
```

Reasons for using linked lists to implement queues:

- **Dynamic size:** The queue can grow and shrink dynamically, unlike with arrays.
- **No shifting:** The front element of the queue can be removed (enqueue) without having to shift other elements in the memory.

Reasons for **not** using linked lists to implement queues:

- **Extra memory:** Each queue element must contain the address to the next element (the next linked list node).
- **Readability:** The code might be harder to read and write for some because it is longer and more complex.
### Method 2: Using collections.deque (Recommended)
```
from collections import deque

class QueueDeque:
    def __init__(self):
        self.items = deque()
    
    def enqueue(self, item):
        """Add item to rear - O(1)"""
        self.items.append(item)
    
    def dequeue(self):
        """Remove and return front - O(1)"""
        if not self.is_empty():
            return self.items.popleft()
        return None
    
    def front(self):
        if not self.is_empty():
            return self.items[0]
        return None
    
    def is_empty(self):
        return len(self.items) == 0
    
    def size(self):
        return len(self.items)
    
    def display(self):
        print(f"Front -> {list(self.items)} <- Rear")

# Efficient implementation
queue = QueueDeque()
queue.enqueue(5)
queue.enqueue(15)
queue.enqueue(25)
print(queue.dequeue())  # 5
```
### Method 3: Circular Queue (Fixed Size)
```
class CircularQueue:
    def __init__(self, capacity):
        self.capacity = capacity
        self.queue = [None] * capacity
        self.front = 0
        self.rear = 0
        self.size = 0
    
    def enqueue(self, item):
        if self.is_full():
            print("Queue is full!")
            return False
        
        self.queue[self.rear] = item
        self.rear = (self.rear + 1) % self.capacity
        self.size += 1
        return True
    
    def dequeue(self):
        if self.is_empty():
            return None
        
        item = self.queue[self.front]
        self.queue[self.front] = None
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        return item
    
    def is_empty(self):
        return self.size == 0
    
    def is_full(self):
        return self.size == self.capacity
    
    def display(self):
        print(f"Queue: {self.queue}")

# Example
cq = CircularQueue(5)
cq.enqueue(1)
cq.enqueue(2)
cq.enqueue(3)
cq.display()  # Queue: [1, 2, 3, None, None]
print(cq.dequeue())  # 1
```

---
## Common Queue Problems & Solutions

### 1. Generate Binary Numbers from 1 to N
```
from collections import deque

def generate_binary_numbers(n):
    """Generate binary numbers from 1 to n using queue"""
    result = []
    queue = deque()
    queue.append("1")
    
    for i in range(n):
        binary = queue.popleft()
        result.append(binary)
        
        queue.append(binary + "0")
        queue.append(binary + "1")
    
    return result

print(generate_binary_numbers(5))  # ['1', '10', '11', '100', '101']
```
### 2. Implement Stack Using Queues
```
from collections import deque

class StackUsingQueues:
    def __init__(self):
        self.q1 = deque()
        self.q2 = deque()
    
    def push(self, item):
        """Push item to stack"""
        self.q2.append(item)
        
        # Move all elements from q1 to q2
        while self.q1:
            self.q2.append(self.q1.popleft())
        
        # Swap queues
        self.q1, self.q2 = self.q2, self.q1
    
    def pop(self):
        if self.q1:
            return self.q1.popleft()
        return None
    
    def top(self):
        if self.q1:
            return self.q1[0]
        return None
    
    def is_empty(self):
        return len(self.q1) == 0

# Example
stack = StackUsingQueues()
stack.push(1)
stack.push(2)
stack.push(3)
print(stack.pop())  # 3
```
### 3. First Non-Repeating Character in Stream
```
from collections import deque, Counter

def first_non_repeating(stream):
    """Find first non-repeating character in stream"""
    queue = deque()
    char_count = Counter()
    result = []
    
    for char in stream:
        char_count[char] += 1
        queue.append(char)
        
        # Remove repeating characters from front
        while queue and char_count[queue[0]] > 1:
            queue.popleft()
        
        result.append(queue[0] if queue else '#')
    
    return result

stream = "aabcbd"
print(first_non_repeating(stream))  # ['a', '#', 'b', 'b', 'c', '#']
```
### 4. Reverse First K Elements of Queue
```
from collections import deque

def reverse_first_k(queue, k):
    """Reverse first k elements of queue"""
    if queue.is_empty() or k > queue.size() or k <= 0:
        return queue
    
    stack = []
    
    # Dequeue first k elements and push to stack
    for i in range(k):
        stack.append(queue.dequeue())
    
    # Pop from stack and enqueue back
    while stack:
        queue.enqueue(stack.pop())
    
    # Move remaining elements to maintain order
    for i in range(queue.size() - k):
        queue.enqueue(queue.dequeue())
    
    return queue

# Example
q = QueueDeque()
for i in range(1, 6):
    q.enqueue(i)
reverse_first_k(q, 3)
q.display()  # Front -> [3, 2, 1, 4, 5] <- Rear
```

---
## Time Complexity

|Operation|List|deque|Circular Queue|
|---|---|---|---|
|enqueue()|O(1)|O(1)|O(1)|
|dequeue()|O(n)|O(1)|O(1)|
|front()|O(1)|O(1)|O(1)|
|is_empty()|O(1)|O(1)|O(1)|

## Types of Queues

1. **Simple Queue**: Basic FIFO queue
    
2. **Circular Queue**: Last position connects to first
    
3. **Priority Queue**: Elements have priorities
    
4. **Double-Ended Queue (Deque)**: Insert/remove from both ends
    

### Priority Queue Example
```
import heapq

class PriorityQueue:
    def __init__(self):
        self.heap = []
        self.count = 0
    
    def enqueue(self, item, priority):
        """Add item with given priority"""
        heapq.heappush(self.heap, (priority, self.count, item))
        self.count += 1
    
    def dequeue(self):
        """Remove and return highest priority item"""
        if self.heap:
            return heapq.heappop(self.heap)[2]
        return None
    
    def is_empty(self):
        return len(self.heap) == 0

# Example
pq = PriorityQueue()
pq.enqueue("Task 1", 3)
pq.enqueue("Task 2", 1)
pq.enqueue("Task 3", 2)
print(pq.dequeue())  # Task 2 (highest priority)
```
