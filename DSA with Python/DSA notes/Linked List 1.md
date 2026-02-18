A **Linked List** is, as the word implies, a list where the nodes are linked together. Each node contains data and a pointer. The way they are linked together is that each node points to where in the memory the next node is placed.

---
## Linked Lists

A linked list consists of nodes with some sort of data, and a pointer, or link, to the next node.

---
## Types of Linked Lists

There are three basic forms of linked lists:

1. Singly linked lists
2. Doubly linked lists
3. Circular linked lists

---

A **singly linked list** is the simplest kind of linked lists. It takes up less space in memory because each node has only one address to the next node.

A **doubly linked list** has nodes with addresses to both the previous and the next node and therefore takes up more memory. But doubly linked lists are good if you want to be able to move both up and down in the list.

A **circular linked list** is like a singly or doubly linked list with the first node, the "head", and the last node, the "tail", connected.

In singly or doubly linked lists, we can find the start and end of a list by just checking if the links are null. But for circular linked lists, more complex code is needed to explicitly check for start and end nodes in certain applications.

Circular linked lists are good for lists you need to cycle through continuously.

> **Note:** What kind of linked list you need depends on the problem you are trying to solve.

---
## Linked List Operations

Basic things we can do with linked lists are:

1. Traversal
2. Remove a node
3. Insert a node
4. Sort

---
## Traversal of a Linked List

Traversing a linked list means to go through the linked list by following the links from one node to the next.

Traversal of linked lists is typically done to search for a specific node, and read or modify the node's content, remove the node, or insert a node right before or after that node.

To traverse a singly linked list, we start with the first node in the list, the head node, and follow that node's next link, and the next node's next link and so on, until the next address is null.

```
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

def traverseAndPrint(head):
  currentNode = head
  while currentNode:
    print(currentNode.data, end=" -> ")
    currentNode = currentNode.next
  print("null")

node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

traverseAndPrint(node1)

#Output:
7 -> 11 -> 3 -> 2 -> 9 -> null
```

---
## Find The Lowest Value in a Linked List
To find the lowest value we need to traverse the list like in the previous code. But in addition to traversing the list, we must also update the current lowest value when we find a node with a lower value.
```
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

def findLowestValue(head):
  minValue = head.data
  currentNode = head.next
  while currentNode:
    if currentNode.data < minValue:
      minValue = currentNode.data
    currentNode = currentNode.next
  return minValue

node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

print("The lowest value in the linked list is:", findLowestValue(node1))

#Output:
The lowest value in the linked list is: 2
```

---
## Delete a Node in a Linked List
If you want to delete a node in a linked list, it is important to connect the nodes on each side of the node before deleting it, so that the linked list is not broken.

So before deleting the node, we need to get the next pointer from the previous node, and connect the previous node to the new next node before deleting the node in between.

Also, it is a good idea to first connect next pointer to the node after the node we want to delete, before we delete it. This is to avoid a 'dangling' pointer, a pointer that points to nothing, even if it is just for a brief moment.
```
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

def traverseAndPrint(head):
  currentNode = head
  while currentNode:
    print(currentNode.data, end=" -> ")
    currentNode = currentNode.next
  print("null")

def deleteSpecificNode(head, nodeToDelete):
  if head == nodeToDelete:
    return head.next

  currentNode = head
  while currentNode.next and currentNode.next != nodeToDelete:
    currentNode = currentNode.next

  if currentNode.next is None:
    return head

  currentNode.next = currentNode.next.next

  return head

node1 = Node(7)
node2 = Node(11)
node3 = Node(3)
node4 = Node(2)
node5 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4
node4.next = node5

print("Before deletion:")
traverseAndPrint(node1)

# Delete node4
node1 = deleteSpecificNode(node1, node4)

print("\nAfter deletion:")
traverseAndPrint(node1)

#Output:
Before deletion:  
7 -> 11 -> 3 -> 2 -> 9 -> null  
  
After deletion:  
7 -> 11 -> 3 -> 9 -> null
```

---
## Insert a Node in a Linked List
Inserting a node into a linked list is very similar to deleting a node, because in both cases we need to take care of the next pointers to make sure we do not break the linked list.

To insert a node in a linked list we first need to create the node, and then at the position where we insert it, we need to adjust the pointers so that the previous node points to the new node, and the new node points to the correct next node.

1. New node is created
2. Node 1 is linked to new node
3. New node is linked to next node

```
class Node:
  def __init__(self, data):
    self.data = data
    self.next = None

def traverseAndPrint(head):
  currentNode = head
  while currentNode:
    print(currentNode.data, end=" -> ")
    currentNode = currentNode.next
  print("null")

def insertNodeAtPosition(head, newNode, position):
  if position == 1:
    newNode.next = head
    return newNode

  currentNode = head
  for _ in range(position - 2):
    if currentNode is None:
      break
    currentNode = currentNode.next

  newNode.next = currentNode.next
  currentNode.next = newNode
  return head

node1 = Node(7)
node2 = Node(3)
node3 = Node(2)
node4 = Node(9)

node1.next = node2
node2.next = node3
node3.next = node4

print("Original list:")
traverseAndPrint(node1)

# Insert a new node with value 97 at position 2
newNode = Node(97)
node1 = insertNodeAtPosition(node1, newNode, 2)

print("\nAfter insertion:")
traverseAndPrint(node1)

#Output:
Original list:  
7 -> 3 -> 2 -> 9 -> null  
  
After insertion:  
7 -> 97 -> 3 -> 2 -> 9 -> null
```