## Recursion Functions in Python

Recursion is a programming technique where a function calls itself to solve a problem by breaking it down into smaller, similar subproblems.

### Basic Structure
```
def recursive_function(parameters):
    # Base case - stops the recursion
    if base_condition:
        return base_value
    # Recursive case - calls itself with modified parameters
    else:
        return recursive_function(modified_parameters)
```
### Classic Examples

#### 1. Factorial
```
def factorial(n):
    # Base case
    if n <= 1:
        return 1
    # Recursive case
    return n * factorial(n - 1)

print(factorial(5))  # Output: 120
```
#### 2. Fibonacci Sequence
```
def fibonacci(n):
    if n <= 1:
        return n
    return fibonacci(n - 1) + fibonacci(n - 2)

print(fibonacci(10))  # Output: 55
```
#### 3. Sum of List
```
def sum_list(numbers):
    if not numbers:  # Empty list
        return 0
    return numbers[0] + sum_list(numbers[1:])

print(sum_list([1, 2, 3, 4, 5]))  # Output: 15
```
#### 4. Power Function
```
def power(base, exponent):
    if exponent == 0:
        return 1
    return base * power(base, exponent - 1)

print(power(2, 5))  # Output: 32
```
#### 5. Binary Search
```
def binary_search(arr, target, left=0, right=None):
    if right is None:
        right = len(arr) - 1
    
    if left > right:
        return -1
    
    mid = (left + right) // 2
    
    if arr[mid] == target:
        return mid
    elif arr[mid] < target:
        return binary_search(arr, target, mid + 1, right)
    else:
        return binary_search(arr, target, left, mid - 1)

arr = [1, 3, 5, 7, 9, 11, 13]
print(binary_search(arr, 7))  # Output: 3
```
#### 6. Tree Traversal
```
class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def inorder_traversal(node):
    if node is None:
        return []
    return (inorder_traversal(node.left) + 
            [node.value] + 
            inorder_traversal(node.right))

# Example usage
root = TreeNode(4)
root.left = TreeNode(2)
root.right = TreeNode(6)
root.left.left = TreeNode(1)
root.left.right = TreeNode(3)

print(inorder_traversal(root))  # Output: [1, 2, 3, 4, 6]
```
