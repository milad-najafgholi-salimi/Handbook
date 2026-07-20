A **linked list** is a linear data structure where elements are stored in nodes, and each node points to the next node in the sequence. Unlike arrays, elements are not stored in contiguous memory locations.

### Key Characteristics:

- **Dynamic Size**: Can grow or shrink at runtime
    
- **Non-contiguous Memory**: Nodes can be anywhere in memory
    
- **Sequential Access**: Must traverse from head to find elements
    
- **Efficient Insertions/Deletions**: O(1) at known positions
    

### Basic Components:

- **Node**: Contains data and reference(s) to next/previous nodes
    
- **Head**: Pointer to the first node
    
- **Tail**: Pointer to the last node (optional)
    
---
## Types of Linked Lists

1. **Singly Linked List**: Each node points to next node
    
2. **Doubly Linked List**: Nodes point to both next and previous
    
3. **Circular Linked List**: Last node points back to first
    

## Implementation in Python

### Node Class (Building Block)
```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None  # Reference to next node
        self.prev = None  # For doubly linked list
```
### 1. Singly Linked List
```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None  # Reference to next node
        self.prev = None  # For doubly linked list

class SinglyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0
    
    def insert_at_beginning(self, data):
        """Insert node at the beginning"""
        new_node = Node(data)
        new_node.next = self.head
        self.head = new_node
        
        if self.tail is None:  # If list was empty
            self.tail = new_node
        
        self.size += 1
    
    def insert_at_end(self, data):
        """Insert node at the end"""
        new_node = Node(data)
        
        if self.head is None:  # If list is empty
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        
        self.size += 1
    
    def insert_at_position(self, data, position):
        """Insert node at specific position (0-based)"""
        if position < 0 or position > self.size:
            raise IndexError("Position out of range")
        
        if position == 0:
            self.insert_at_beginning(data)
            return
        
        if position == self.size:
            self.insert_at_end(data)
            return
        
        new_node = Node(data)
        current = self.head
        
        # Traverse to node before insertion point
        for _ in range(position - 1):
            current = current.next
        
        new_node.next = current.next
        current.next = new_node
        self.size += 1
    
    def delete_from_beginning(self):
        """Delete first node"""
        if self.head is None:
            return None
        
        data = self.head.data
        self.head = self.head.next
        
        if self.head is None:  # List became empty
            self.tail = None
        
        self.size -= 1
        return data
    
    def delete_from_end(self):
        """Delete last node"""
        if self.head is None:
            return None
        
        data = self.tail.data
        
        if self.head == self.tail:  # Only one node
            self.head = None
            self.tail = None
        else:
            current = self.head
            while current.next != self.tail:
                current = current.next
            current.next = None
            self.tail = current
        
        self.size -= 1
        return data
    
    def delete_by_value(self, value):
        """Delete first occurrence of value"""
        if self.head is None:
            return False
        
        if self.head.data == value:
            self.delete_from_beginning()
            return True
        
        current = self.head
        while current.next and current.next.data != value:
            current = current.next
        
        if current.next:
            if current.next == self.tail:
                self.tail = current
            current.next = current.next.next
            self.size -= 1
            return True
        
        return False
    
    def search(self, value):
        """Search for value, return index if found"""
        current = self.head
        index = 0
        
        while current:
            if current.data == value:
                return index
            current = current.next
            index += 1
        
        return -1
    
    def get(self, index):
        """Get value at index"""
        if index < 0 or index >= self.size:
            raise IndexError("Index out of range")
        
        current = self.head
        for _ in range(index):
            current = current.next
        return current.data
    
    def display(self):
        """Display the linked list"""
        elements = []
        current = self.head
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" -> ".join(elements) + " -> None")
        print(f"Size: {self.size}, Head: {self.head.data if self.head else None}, Tail: {self.tail.data if self.tail else None}")

# Example Usage
sll = SinglyLinkedList()
sll.insert_at_end(10)
sll.insert_at_end(20)
sll.insert_at_beginning(5)
sll.insert_at_position(15, 2)
sll.display()  # 5 -> 10 -> 15 -> 20 -> None
print(f"Deleted: {sll.delete_from_beginning()}")  # 5
print(f"Search 15: {sll.search(15)}")  # 1
```
### 2. Doubly Linked List
```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None  # Reference to next node
        self.prev = None  # For doubly linked list

class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0
    
    def insert_at_beginning(self, data):
        """Insert node at beginning"""
        new_node = Node(data)
        
        if self.head is None:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.next = self.head
            self.head.prev = new_node
            self.head = new_node
        
        self.size += 1
    
    def insert_at_end(self, data):
        """Insert node at end"""
        new_node = Node(data)
        
        if self.tail is None:
            self.head = new_node
            self.tail = new_node
        else:
            new_node.prev = self.tail
            self.tail.next = new_node
            self.tail = new_node
        
        self.size += 1
    
    def delete_from_beginning(self):
        """Delete first node"""
        if self.head is None:
            return None
        
        data = self.head.data
        
        if self.head == self.tail:
            self.head = None
            self.tail = None
        else:
            self.head = self.head.next
            self.head.prev = None
        
        self.size -= 1
        return data
    
    def delete_from_end(self):
        """Delete last node"""
        if self.tail is None:
            return None
        
        data = self.tail.data
        
        if self.head == self.tail:
            self.head = None
            self.tail = None
        else:
            self.tail = self.tail.prev
            self.tail.next = None
        
        self.size -= 1
        return data
    
    def display_forward(self):
        """Display from head to tail"""
        elements = []
        current = self.head
        while current:
            elements.append(str(current.data))
            current = current.next
        print(" -> ".join(elements) + " -> None")
    
    def display_backward(self):
        """Display from tail to head"""
        elements = []
        current = self.tail
        while current:
            elements.append(str(current.data))
            current = current.prev
        print("None <- " + " <- ".join(elements))

# Example
dll = DoublyLinkedList()
dll.insert_at_end(1)
dll.insert_at_end(2)
dll.insert_at_end(3)
dll.insert_at_beginning(0)
dll.display_forward()   # 0 -> 1 -> 2 -> 3 -> None
dll.display_backward()  # None <- 3 <- 2 <- 1 <- 0
```
### 3. Circular Linked List
```
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None  # Reference to next node
        self.prev = None  # For doubly linked list

class CircularLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None
        self.size = 0
    
    def insert_at_end(self, data):
        """Insert node at end"""
        new_node = Node(data)
        
        if self.head is None:
            self.head = new_node
            self.tail = new_node
            new_node.next = self.head  # Point to itself
        else:
            new_node.next = self.head
            self.tail.next = new_node
            self.tail = new_node
        
        self.size += 1
    
    def delete_by_value(self, value):
        """Delete node with given value"""
        if self.head is None:
            return False
        
        current = self.head
        prev = self.tail
        
        # Search for the node
        while True:
            if current.data == value:
                if current == self.head:
                    self.head = self.head.next
                    self.tail.next = self.head
                else:
                    prev.next = current.next
                    if current == self.tail:
                        self.tail = prev
                
                self.size -= 1
                return True
            
            prev = current
            current = current.next
            
            if current == self.head:  # Completed full circle
                break
        
        return False
    
    def display(self):
        """Display circular linked list"""
        if self.head is None:
            print("Empty list")
            return
        
        elements = []
        current = self.head
        while True:
            elements.append(str(current.data))
            current = current.next
            if current == self.head:
                break
        
        print(" -> ".join(elements) + f" -> (back to {self.head.data})")

# Example
cll = CircularLinkedList()
cll.insert_at_end(10)
cll.insert_at_end(20)
cll.insert_at_end(30)
cll.display()  # 10 -> 20 -> 30 -> (back to 10)
```

---
## Common Linked List Problems

### 1. Reverse a Linked List
```
def reverse_linked_list(head):
    """Reverse singly linked list iteratively"""
    prev = None
    current = head
    
    while current:
        next_temp = current.next
        current.next = prev
        prev = current
        current = next_temp
    
    return prev

# Recursive version
def reverse_recursive(head):
    if head is None or head.next is None:
        return head
    
    new_head = reverse_recursive(head.next)
    head.next.next = head
    head.next = None
    
    return new_head
```
### 2. Detect Cycle (Floyd's Cycle Detection)
```
def has_cycle(head):
    """Detect if linked list has a cycle"""
    if head is None:
        return False
    
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            return True
    
    return False

def find_cycle_start(head):
    """Find the start node of the cycle"""
    if head is None:
        return None
    
    # Detect cycle
    slow = fast = head
    has_cycle = False
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
        
        if slow == fast:
            has_cycle = True
            break
    
    if not has_cycle:
        return None
    
    # Find cycle start
    slow = head
    while slow != fast:
        slow = slow.next
        fast = fast.next
    
    return slow
```
### 3. Find Middle of Linked List
```
def find_middle(head):
    """Find middle node using slow/fast pointers"""
    if head is None:
        return None
    
    slow = head
    fast = head
    
    while fast and fast.next:
        slow = slow.next
        fast = fast.next.next
    
    return slow
```
### 4. Merge Two Sorted Lists
```
def merge_sorted_lists(l1, l2):
    """Merge two sorted linked lists"""
    dummy = Node(0)
    current = dummy
    
    while l1 and l2:
        if l1.data <= l2.data:
            current.next = l1
            l1 = l1.next
        else:
            current.next = l2
            l2 = l2.next
        current = current.next
    
    # Attach remaining nodes
    if l1:
        current.next = l1
    if l2:
        current.next = l2
    
    return dummy.next
```
### 5. Remove Nth Node from End
```
def remove_nth_from_end(head, n):
    """Remove nth node from end"""
    dummy = Node(0)
    dummy.next = head
    
    first = dummy
    second = dummy
    
    # Move first pointer n+1 steps ahead
    for i in range(n + 1):
        first = first.next
    
    # Move both pointers until first reaches end
    while first:
        first = first.next
        second = second.next
    
    # Remove nth node
    second.next = second.next.next
    
    return dummy.next
```

---
## Time Complexity Comparison

|Operation|Singly Linked|Doubly Linked|Array|
|---|---|---|---|
|Access by Index|O(n)|O(n)|O(1)|
|Insert at Beginning|O(1)|O(1)|O(n)|
|Insert at End|O(1)*|O(1)|O(1)**|
|Insert in Middle|O(n)|O(n)|O(n)|
|Delete at Beginning|O(1)|O(1)|O(n)|
|Delete at End|O(n)|O(1)|O(1)|
|Search|O(n)|O(n)|O(n)|

* With tail pointer  
** If capacity not exceeded

---
## Space Complexity

- **Singly Linked List**: O(n) for n nodes
    
- **Doubly Linked List**: O(n) + extra space for prev pointers
    
- **Each Node**: O(1) extra space for pointers
    
---
## Real-World Applications

1. **Music Player Playlist**: Next/previous navigation
    
2. **Browser History**: Back/forward navigation
    
3. **Image Viewer**: Previous/next image
    
4. **Undo/Redo Functionality**: Stack implementation
    
5. **Hash Table Collision Resolution**: Chaining
    
6. **Memory Management**: Free list in operating systems
    
---
## Advantages and Disadvantages

### Advantages:

- **Dynamic size**: No need to pre-allocate
    
- **Efficient insertions/deletions**: O(1) at known positions
    
- **Memory efficient**: Only allocate needed memory
    
- **Easy to reorganize**: Can rearrange nodes by changing pointers
    

### Disadvantages:

- **No random access**: Must traverse to find elements
    
- **Extra memory**: Need to store pointers
    
- **Not cache-friendly**: Nodes may be scattered in memory
    
- **Complex implementation**: More complex than arrays
    
---
## When to Use Linked Lists

✅ **Use Linked List when:**

- You need frequent insertions/deletions at arbitrary positions
    
- Size is unknown and may change frequently
    
- You don't need random access
    
- Memory is fragmented (can't allocate large contiguous blocks)
    

❌ **Avoid Linked List when:**

- You need frequent random access by index
    
- Memory is very limited (pointer overhead)
    
- You have cache-sensitive applications
    
- Implementation simplicity is important
    
---
## Advanced: LRU Cache Using Doubly Linked List
```
class LRUCache:
    """Least Recently Used (LRU) Cache implementation"""
    def __init__(self, capacity):
        self.capacity = capacity
        self.cache = {}  # Key -> node mapping
        self.head = Node(0, 0)  # Dummy head
        self.tail = Node(0, 0)  # Dummy tail
        self.head.next = self.tail
        self.tail.prev = self.head
    
    def _remove(self, node):
        """Remove node from linked list"""
        prev = node.prev
        next = node.next
        prev.next = next
        next.prev = prev
    
    def _add(self, node):
        """Add node right after head"""
        node.prev = self.head
        node.next = self.head.next
        self.head.next.prev = node
        self.head.next = node
    
    def get(self, key):
        """Get value by key"""
        if key in self.cache:
            node = self.cache[key]
            self._remove(node)
            self._add(node)
            return node.value
        return -1
    
    def put(self, key, value):
        """Put key-value pair"""
        if key in self.cache:
            self._remove(self.cache[key])
        
        node = Node(key, value)
        self._add(node)
        self.cache[key] = node
        
        if len(self.cache) > self.capacity:
            lru = self.tail.prev
            self._remove(lru)
            del self.cache[lru.key]

# Example
lru = LRUCache(2)
lru.put(1, 1)
lru.put(2, 2)
print(lru.get(1))    # 1
lru.put(3, 3)        # Evicts key 2
print(lru.get(2))    # -1 (not found)
```
Linked lists are fundamental data structures that provide flexibility in memory management and efficient insertions/deletions, making them essential in many algorithms and system designs!