The **AVL** Tree is a type of Binary Search Tree named after two Soviet inventors Georgy **A**delson-**V**elsky and Evgenii **L**andis who invented the AVL Tree in 1962.

AVL trees are self-balancing, which means that the tree height is kept to a minimum so that a very fast runtime is guaranteed for searching, inserting and deleting nodes, with time complexity O(logn).

---
The only difference between a **regular Binary Search Tree** and an **AVL Tree** is that AVL Trees do rotation operations in addition, to keep the tree balance.

A Binary Search Tree is in balance when the difference in height between left and right subtrees is less than 2.

---
## The Balance Factor

A node's balance factor is the difference in subtree heights.

The subtree heights are stored at each node for all nodes in an AVL Tree, and the balance factor is calculated based on its subtree heights to check if the tree has become out of balance.

The height of a subtree is the number of edges between the root node of the subtree and the leaf node farthest down in that subtree.

---
The **Balance Factor** (BF) for a node (X) is the difference in height between its right and left subtrees.

BF(X)=height(rightSubtree(X))−height(leftSubtree(X))

Balance factor values

- 0: The node is in balance.
- more than 0: The node is "right heavy".
- less than 0: The node is "left heavy".

If the balance factor is less than -1, or more than 1, for one or more nodes in the tree, the tree is considered not in balance, and a rotation operation is needed to restore balance.

---
## The Four "out-of-balance" Cases

When the balance factor of just one node is less than -1, or more than 1, the tree is regarded as out of balance, and a rotation is needed to restore balance.

There are four different ways an AVL Tree can be out of balance, and each of these cases require a different rotation operation.

|Case|Description|Rotation to Restore Balance|
|---|---|---|
|Left-Left (LL)|The unbalanced node and its left child node are both left-heavy.|A single right rotation.|
|Right-Right (RR)|The unbalanced node and its right child node are both right-heavy.|A single left rotation.|
|Left-Right (LR)|The unbalanced node is left heavy, and its left child node is right heavy.|First do a left rotation on the left child node, then do a right rotation on the unbalanced node.|
|Right-Left (RL)|The unbalanced node is right heavy, and its right child node is left heavy.|First do a right rotation on the right child node, then do a left rotation on the unbalanced node.|

---
## The Left-Left (LL) Case

The node where the unbalance is discovered is left heavy, and the node's left child node is also left heavy.

When this LL case happens, a single right rotation on the unbalanced node is enough to restore balance.

---
## The Right-Right (RR) Case

A Right-Right case happens when a node is unbalanced and right heavy, and the right child node is also right heavy.

A single left rotation at the unbalanced node is enough to restore balance in the RR case.

---
## The Left-Right (LR) Case

The Left-Right case is when the unbalanced node is left heavy, but its left child node is right heavy.

In this LR case, a left rotation is first done on the left child node, and then a right rotation is done on the original unbalanced node.

---
## The Right-Left (RL) Case

The Right-Left case is when the unbalanced node is right heavy, and its right child node is left heavy.

In this case we first do a right rotation on the unbalanced node's right child, and then we do a left rotation on the unbalanced node itself.

---
## Retracing in AVL Trees

After inserting or deleting a node in an AVL tree, the tree may become unbalanced. To find out if the tree is unbalanced, we need to update the heights and recalculate the balance factors of all ancestor nodes.

This process, known as retracing, is handled through recursion. As the recursive calls propagate back to the root after an insertion or deletion, each ancestor node's height is updated and the balance factor is recalculated. If any ancestor node is found to have a balance factor outside the range of -1 to 1, a rotation is performed at that node to restore the tree's balance.

---
## AVL Tree Implementation in Python

This code is based on the BST implementation for inserting nodes.

There is only one new attribute for each node in the AVL tree compared to the BST, and that is the height, but there are many new functions and extra code lines needed for the AVL Tree implementation because of how the AVL Tree rebalances itself.

```
class TreeNode:
  def __init__(self, data):
    self.data = data
    self.left = None
    self.right = None
    self.height = 1

def getHeight(node):
  if not node:
    return 0
  return node.height

def getBalance(node):
  if not node:
    return 0
  return getHeight(node.left) - getHeight(node.right)

def rightRotate(y):
  print('Rotate right on node',y.data)
  x = y.left
  T2 = x.right
  x.right = y
  y.left = T2
  y.height = 1 + max(getHeight(y.left), getHeight(y.right))
  x.height = 1 + max(getHeight(x.left), getHeight(x.right))
  return x

def leftRotate(x):
  print('Rotate left on node',x.data)
  y = x.right
  T2 = y.left
  y.left = x
  x.right = T2
  x.height = 1 + max(getHeight(x.left), getHeight(x.right))
  y.height = 1 + max(getHeight(y.left), getHeight(y.right))
  return y

def insert(node, data):
  if not node:
    return TreeNode(data)

  if data < node.data:
    node.left = insert(node.left, data)
  elif data > node.data:
    node.right = insert(node.right, data)

  # Update the balance factor and balance the tree
  node.height = 1 + max(getHeight(node.left), getHeight(node.right))
  balance = getBalance(node)

  # Balancing the tree
  # Left Left
  if balance > 1 and getBalance(node.left) >= 0:
    return rightRotate(node)

  # Left Right
  if balance > 1 and getBalance(node.left) < 0:
    node.left = leftRotate(node.left)
    return rightRotate(node)

  # Right Right
  if balance < -1 and getBalance(node.right) <= 0:
    return leftRotate(node)

  # Right Left
  if balance < -1 and getBalance(node.right) > 0:
    node.right = rightRotate(node.right)
    return leftRotate(node)

  return node

def inOrderTraversal(node):
  if node is None:
    return
  inOrderTraversal(node.left)
  print(node.data, end=", ")
  inOrderTraversal(node.right)

# Inserting nodes
root = None
letters = ['C', 'B', 'E', 'A', 'D', 'H', 'G', 'F']
for letter in letters:
  root = insert(root, letter)

inOrderTraversal(root)

#Output:
Rotate right on node H  
A, B, C, D, E, F, G, H,
```

---
## AVL Delete Node Implementation

When deleting a node that is not a leaf node, the AVL Tree requires the `minValueNode()` function to find a node's next node in the in-order traversal. This is the same as when deleting a node in a Binary Search Tree.

To delete a node in an AVL Tree, the same code to restore balance is needed as for the code to insert a node.
```
class TreeNode:
  def __init__(self, data):
    self.data = data
    self.left = None
    self.right = None
    self.height = 1

def getHeight(node):
  if not node:
    return 0
  return node.height

def getBalance(node):
  if not node:
    return 0
  return getHeight(node.left) - getHeight(node.right)

def rightRotate(y):
  x = y.left
  T2 = x.right
  x.right = y
  y.left = T2
  y.height = 1 + max(getHeight(y.left), getHeight(y.right))
  x.height = 1 + max(getHeight(x.left), getHeight(x.right))
  return x

def leftRotate(x):
  y = x.right
  T2 = y.left
  y.left = x
  x.right = T2
  x.height = 1 + max(getHeight(x.left), getHeight(x.right))
  y.height = 1 + max(getHeight(y.left), getHeight(y.right))
  return y

def insert(node, data):
  if not node:
    return TreeNode(data)

  if data < node.data:
    node.left = insert(node.left, data)
  elif data > node.data:
    node.right = insert(node.right, data)

  # Update the balance factor and balance the tree
  node.height = 1 + max(getHeight(node.left), getHeight(node.right))
  balance = getBalance(node)

  # Balancing the tree
  # Left Left
  if balance > 1 and getBalance(node.left) >= 0:
    return rightRotate(node)

  # Left Right
  if balance > 1 and getBalance(node.left) < 0:
    node.left = leftRotate(node.left)
    return rightRotate(node)

  # Right Right
  if balance < -1 and getBalance(node.right) <= 0:
    return leftRotate(node)

  # Right Left
  if balance < -1 and getBalance(node.right) > 0:
    node.right = rightRotate(node.right)
    return leftRotate(node)

  return node

def inOrderTraversal(node):
  if node is None:
    return
  inOrderTraversal(node.left)
  print(node.data, end=", ")
  inOrderTraversal(node.right)
    
def minValueNode(node):
  current = node
  while current.left is not None:
    current = current.left
  return current

def minValueNode(node):
  current = node
  while current.left is not None:
    current = current.left
  return current

def delete(node, data):
  if not node:
    return node

  if data < node.data:
    node.left = delete(node.left, data)
  elif data > node.data:
    node.right = delete(node.right, data)
  else:
    if node.left is None:
      temp = node.right
      node = None
      return temp
    elif node.right is None:
      temp = node.left
      node = None
      return temp

    temp = minValueNode(node.right)
    node.data = temp.data
    node.right = delete(node.right, temp.data)

  if node is None:
    return node

  # Update the balance factor and balance the tree
  node.height = 1 + max(getHeight(node.left), getHeight(node.right))
  balance = getBalance(node)

  # Balancing the tree
  # Left Left
  if balance > 1 and getBalance(node.left) >= 0:
    return rightRotate(node)

  # Left Right
  if balance > 1 and getBalance(node.left) < 0:
    node.left = leftRotate(node.left)
    return rightRotate(node)

  # Right Right
  if balance < -1 and getBalance(node.right) <= 0:
    return leftRotate(node)

  # Right Left
  if balance < -1 and getBalance(node.right) > 0:
    node.right = rightRotate(node.right)
    return leftRotate(node)

  return node

# Inserting the letters
root = None
letters = ['C', 'B', 'E', 'A', 'D', 'H', 'G', 'F']
for letter in letters:
  root = insert(root, letter)

inOrderTraversal(root)
print('\nDeleting A')
root = delete(root,'A')
inOrderTraversal(root)

#Output:
A, B, C, D, E, F, G, H,  
Deleting A  
B, C, D, E, F, G, H,
```

---
## Time Complexity for AVL Trees

- The **BST** is not self-balancing. This means that a BST can be very unbalanced, almost like a long chain, where the height is nearly the same as the number of nodes. This makes operations like searching, deleting and inserting nodes slow, with time complexity `O(h)=O(n)`.
- The **AVL Tree** however is self-balancing. That means that the height of the tree is kept to a minimum so that operations like searching, deleting and inserting nodes are much faster, with time complexity `O(h)=O(logn)`.

---
## O(logn) Explained

The fact that the time complexity is `O(h)=O(logn)` for search, insert, and delete on an AVL Tree with height h and nodes n can be explained like this:

Imagine a perfect Binary Tree where all nodes have two child nodes except on the lowest level.

The number of nodes on each level in such an AVL Tree are:

$$1,2,4,8,16,32,..$$

Which is the same as:

$$2^0, 2^1, 2^2, 2^3, 2^4, 2^5, ...$$

To get the number of nodes `n` in a perfect Binary Tree with height `h=3`, we can add the number of nodes on each level together:

$$n_3=2^0+2^1+2^2+2^3=15$$

Which is actually the same as:

$$n_3=2^4−1=15$$

And this is actually the case for larger trees as well! If we want to get the number of nodes `n` in a tree with height `h=5` for example, we find the number of nodes like this:

$$n_5=2^6−1=63$$

So in general, the relationship between the height `h` of a perfect Binary Tree and the number of nodes in it `n`, can be expressed like this:

$$n_h=2^{h+1}−1$$
> **Note:** The formula above can also be found by calculating the sum of the geometric series 20+21+22+23+...+2n

We know that the time complexity for searching, deleting, or inserting a node in an AVL tree is `O(h)`, but we want to argue that the time complexity is actually `O(log(n))`, so we need to find the height `h` described by the number of nodes `n`:

$$n=2^{h+1}−1$$
$$n+1=2^{h+1}$$
$$log_2(n+1)=log_2(2^{h+1})$$
$$h=log_2(n+1)−1$$
$$O(h)=O(logn)$$
For a Binary Tree with a lot of nodes (big n), the "+1" and "-1" terms are not important when we consider time complexity.

The math above shows that the time complexity for search, delete, and insert operations on an AVL Tree `O(h)`, can actually be expressed as `O(logn)`, which is fast, a lot faster than the time complexity for BSTs which is `O(n)`.
