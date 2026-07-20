In Data Structures and Algorithms (DSA), a **tree** is a **non-linear**, **hierarchical** data structure consisting of nodes connected by edges.

Unlike arrays, linked lists, stacks, or queues (which are linear), trees organize data in a parent-child relationship, making them perfect for representing hierarchical data (like file systems, organizational charts, or HTML DOM).

### 1. Core Terminology

To understand trees, you must know these terms:

- **Node:** The fundamental part of a tree that stores data.
    
- **Root:** The topmost node of the tree. There is exactly one root in a tree.
    
- **Parent:** A node that has branches (edges) pointing to other nodes below it.
    
- **Child:** A node directly connected to another node when moving away from the root.
    
- **Leaf (External Node):** A node that has no children.
    
- **Internal Node:** A node that has at least one child.
    
- **Siblings:** Nodes that share the same parent.
    
- **Depth:** The number of edges from the root to a specific node.
    
- **Height:** The number of edges on the longest path from a specific node to a leaf.
    
- **Subtree:** Any node in the tree, along with all its descendants, forms a smaller tree.

### 2. Types of Trees (Most Important Ones)

There are many types, but these are the ones you will encounter most in DSA:

| Type                         | Description                                                                                                           | Best Used For                                                                                          |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ |
| **Binary Tree**              | Each node has **at most 2 children** (left and right).                                                                | Base for all advanced trees.                                                                           |
| **Binary Search Tree (BST)** | A binary tree where the **left child** is smaller than the parent, and the **right child** is greater.                | Fast searching, insertion, and deletion (O(log⁡n) on average).                                         |
| **AVL Tree**                 | A "self-balancing" BST. The height difference between left and right subtrees (balance factor) is always -1, 0, or 1. | When you need guaranteed O(log⁡n) performance even with sorted data.                                   |
| **Red-Black Tree**           | A self-balancing BST that uses a "color" bit (red/black) to ensure balance.                                           | Used in C++ STL (`map`, `set`) and Java `TreeMap` because they require less rotation than AVL.         |
| **B-Tree / B+ Tree**         | A self-balancing tree where a node can have **more than 2 children** (many children).                                 | Databases and file systems (like NTFS or ext4) for reading/writing large blocks of data from disks.    |
| **Trie (Prefix Tree)**       | A tree used to store strings where each node represents a single character.                                           | Autocomplete, spell checkers, and IP routing.                                                          |
| **Heap**                     | A specialized tree where the parent is either greater (Max-Heap) or smaller (Min-Heap) than its children.             | Priority Queues and Heap Sort. (Note: It is usually implemented as an array, but conceptually a tree). |

### 3. Common Tree Traversals

Since trees aren't linear, you need specific ways to visit all the nodes.

**Depth-First Search (DFS)** - Goes deep before going wide:

- **Pre-order (Root, Left, Right):** Used to copy the tree or get a prefix expression.
    
- **In-order (Left, Root, Right):** Used on BSTs to get nodes in sorted order.
    
- **Post-order (Left, Right, Root):** Used to delete the tree or calculate the size of directories (bottom-up).
    

**Breadth-First Search (BFS)** - Goes wide before going deep:

- **Level-order:** Visits nodes row by row, from top to bottom. Used to find the shortest path in unweighted graphs.

### 4. Why use Trees over other Data Structures?

| Operation  | Array (Sorted) | Linked List      | Binary Search Tree (Balanced) |
| ---------- | -------------- | ---------------- | ----------------------------- |
| **Search** | O(log⁡n)       | O(n)             | O(log⁡n)O                     |
| **Insert** | O(n)           | O(1)(if at head) | O(log⁡n)                      |
| **Delete** | O(n)           | O(n)             | O(log⁡n)                      |

**The takeaway:** Trees give you the **best of both worlds**. You get the fast searching of sorted arrays, _plus_ the fast insertion and deletion of linked lists.

### 5. Real-World Applications

You use trees every day without realizing it:

- **File Explorer:** The folders on your computer are a tree (root is "This PC" or "/").
    
- **HTML DOM:** When a web browser renders a webpage, it creates a "Document Object Model" tree.
    
- **Compilers:** When your code compiles, it is broken down into an **Abstract Syntax Tree (AST)**.
    
- **Networking:** Routers use spanning trees to prevent broadcast storms.
    
- **AI/Game Development:** Decision trees and minimax trees are used to make AI play games like Chess.

### 6. Complexity Cheat Sheet (for a balanced BST)

- **Search:** O(log⁡n)
    
- **Insert:** O(log⁡n)
    
- **Delete:** O(log⁡n)
    
- **Space:** O(n)

### 7. Sample Code (Binary Tree Node in Python)

If you are coding interviews, this is the basic building block you must know:
```
class TreeNode:
    def __init__(self, val):
        self.val = val        # The data
        self.left = None      # Pointer to left child
        self.right = None     # Pointer to right child

# Creating a simple tree:    1
#                          /   \
#                         2     3
root = TreeNode(1)
root.left = TreeNode(2)
root.right = TreeNode(3)
```

###  Final Pro-Tip for Interviews:

When solving DSA problems, **always ask the interviewer if the tree is a Binary Search Tree (BST) or a general Binary Tree**.

- If it's a **BST**, you can use the property of sorted order (In-order traversal or binary search logic).
    
- If it's a **general binary tree**, you usually have to traverse the _entire_ tree (using DFS or BFS) to find the answer.