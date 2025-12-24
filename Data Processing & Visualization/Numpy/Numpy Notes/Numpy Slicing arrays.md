Slicing in python means taking elements from one given index to another given index.

We pass slice instead of index like this: `[_start_:_end_]`.

We can also define the step, like this: `[_start_:_end_:_step_]`.

If we don't pass start its considered 0

If we don't pass end its considered length of array in that dimension

If we don't pass step its considered 1.

Example:
```
import numpy as np  
  
arr = np.array([1, 2, 3, 4, 5, 6, 7])
print(arr[1:5])

#Output:
[2 3 4 5]
```
**Note:** The result _includes_ the start index, but _excludes_ the end index.

---
## Negative Slicing

Use the minus operator to refer to an index from the end:

Example:
```
import numpy as np  
  
arr = np.array([1, 2, 3, 4, 5, 6, 7])  
print(arr[-3:-1])

#Output:
[5 6]
```

---
## STEP

Use the `step` value to determine the step of the slicing:

Example:
```
import numpy as np  
  
arr = np.array([1, 2, 3, 4, 5, 6, 7])  
print(arr[1:5:2])

#Output:
[2 4]
```
Example:
```
import numpy as np  
  
arr = np.array([1, 2, 3, 4, 5, 6, 7])  
print(arr[::2])

#Output:
[1 3 5 7]
```

---
## Slicing 2-D Arrays
Example:
```
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[1, 1:4])

#Output:
[7 8 9]
```
Example - From both elements, return index 2:
```
import numpy as np  
  
arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[0:2, 2])

#Output:
[3 8]
```
Example - From both elements, slice index 1 to index 4 (not included), this will return a 2-D array:
```
import numpy as np

arr = np.array([[1, 2, 3, 4, 5], [6, 7, 8, 9, 10]])
print(arr[0:2, 1:4])

#Output:
[[2 3 4]
 [7 8 9]]
```
