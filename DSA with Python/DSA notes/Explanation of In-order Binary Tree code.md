**Attention please that you can use this explanation to understand two other codes (pre-order and post-order binary tree)!**

### My Question:
Consider the following code:
```
class TreeNode:
    def __init__(self, data):
        self.data = data
        self.left = None
        self.right = None

def inOrderTraversal(node):
    if node is None:
        return
    inOrderTraversal(node.left)
    print(node.data, end=", ")
    inOrderTraversal(node.right)

root = TreeNode('R')
nodeA = TreeNode('A')
nodeB = TreeNode('B')
nodeC = TreeNode('C')
nodeD = TreeNode('D')
nodeE = TreeNode('E')
nodeF = TreeNode('F')
nodeG = TreeNode('G')

root.left = nodeA
root.right = nodeB

nodeA.left = nodeC
nodeA.right = nodeD

nodeB.left = nodeE
nodeB.right = nodeF

nodeF.left = nodeG

# Traverse
inOrderTraversal(root)

# Output:
# C, A, D, R, E, B, G, F,
```
In the following part of the code:
```
inOrderTraversal(node.left)
print(node.data, end=", ")
inOrderTraversal(node.right)
```
Are all three lines read and executed by the interpreter first, then stored somewhere, and finally their results returned in the order they appear in the program?

### Answer:
No, that is **not** how recursion works.
When the interpreter reaches these three lines:
```
inOrderTraversal(node.left)
print(node.data, end=", ")
inOrderTraversal(node.right)
```
it **does not execute all three lines first** and then store or return their results later. Instead, execution **stops at the first recursive call** until that call has completely finished.

Let's walk through the process step by step.
#### Step 1: Start at the Root

The traversal begins with:
```
inOrderTraversal(root)
```
where `root` is the node `R`.
Inside the function, we have:
```
node = R

inOrderTraversal(node.left)   # Visit A
print(node.data)
inOrderTraversal(node.right)
```
The interpreter reaches:
```
inOrderTraversal(node.left)
```
and immediately calls the function again for node `A`.
Notice that **the next two lines have not been executed yet**.
#### Step 2: Traverse Node A

Now the function is executing for node `A`:
```
node = A

inOrderTraversal(C)
print(A)
inOrderTraversal(D)
```
Again, the interpreter executes the first line:
```
inOrderTraversal(C)
```
and pauses the execution of `A` until the traversal of `C` is complete.
#### Step 3: Traverse Node C

Now the function is executing for node `C`:
```
node = C

inOrderTraversal(None)
print(C)
inOrderTraversal(None)
```
The first call is:
```
inOrderTraversal(None)
```
Since the function begins with:
```
if node is None:
    return
```
it returns immediately.
The interpreter then continues with:
```
print(C)
```
So the first value printed is:
```
C
```
Next,
```
inOrderTraversal(None)
```
is executed and returns immediately.
The traversal of node `C` is now complete.

#### Returning to Node A
Once the recursive call for `C` finishes, execution returns to the suspended function for `A`.
The interpreter continues with:
```
print(A)
```
and then executes:
```
inOrderTraversal(D)
```
#### Returning to the Root
After the entire left subtree (`A`, `C`, and `D`) has been processed, execution returns to the original call for `R`.
Only now does the interpreter execute:
```
print(R)
```
followed by:
```
inOrderTraversal(B)
```
### Are the three lines executed together?
No.
The execution flow is actually:
```
Execute the first line.
        ↓
If it is a recursive call,
pause the current function.
        ↓
Completely finish the recursive call.
        ↓
Return to the current function.
        ↓
Execute the second line.
        ↓
Execute the third line.
```
### Is anything stored?
Yes—but **not the printed output**.
What is stored is the **execution state** of each function call on the **Call Stack**.
For example, while processing node `C`, the call stack looks conceptually like this:
```
Top
---------
C
A
R
---------
```
Each stack frame stores information such as:

- The current value of `node`
- The local variables
- The exact point where execution should resume after the recursive call finishes

When the traversal of `C` finishes, its stack frame is removed:
```
Top
---------
A
R
---------
```
The interpreter now knows to continue executing `A` **immediately after** the recursive call to `C`, which means the next statement is:
```
print(node.data)
```
### The Actual Execution Order
The traversal proceeds like this:
```
R:
    Go to A

A:
    Go to C

C:
    Go to None
    Print C
    Go to None
    Finish C

A:
    Print A
    Go to D

D:
    Go to None
    Print D
    Go to None
    Finish D

A:
    Finish A

R:
    Print R
    Go to B
...
```
