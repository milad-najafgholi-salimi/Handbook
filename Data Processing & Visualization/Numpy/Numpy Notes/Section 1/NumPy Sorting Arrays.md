## Sorting Arrays

Sorting means putting elements in an _ordered sequence_.

_Ordered sequence_ is any sequence that has an order corresponding to elements, like numeric or alphabetical, ascending or descending.

The NumPy ndarray object has a function called `sort()`, that will sort a specified array.
### Example
- Sort the array:
```
import numpy as np

arr = np.array([3, 2, 0, 1])

print(np.sort(arr))

#Output:
[0 1 2 3]
```
>**Note:** This method returns a copy of the array, leaving the original array unchanged.

You can also sort arrays of strings, or any other data type:

### Example
- Sort the array alphabetically:
```
import numpy as np

arr = np.array(['banana', 'cherry', 'apple'])

print(np.sort(arr))

#Output:
['apple' 'banana' 'cherry']
```

### Example
- Sort a boolean array:
```
import numpy as np

arr = np.array([True, False, True])

print(np.sort(arr))

#Output:
[False True True]
```

---
## Sorting a 2-D Array

If you use the sort() method on a 2-D array, both arrays will be sorted:

### Example
- Sort a 2-D array:
```
import numpy as np

arr = np.array([[3, 2, 4], [5, 0, 1]])

print(np.sort(arr))

#Output:
[[2 3 4]
 [0 1 5]]
```

---
## Sorting Algorithms

NumPy supports following algorithms:

- Quicksort
- Heapsort
- Mergesort
- Stable

We can specify the algorithm by using the `kind` parameter:

### Example
- Sort with different algorithms:
```
import numpy as np  
  
arr = np.array([[3, 2, 4], [5, 0, 1]])  
  
print(np.sort(arr, kind='quicksort')) # default  
print(np.sort(arr, kind='heapsort'))  
print(np.sort(arr, kind='mergesort'))  
print(np.sort(arr, kind='stable'))

#Output:
[[2 3 4]
 [0 1 5]]
[[2 3 4]
 [0 1 5]]
[[2 3 4]
 [0 1 5]]
[[2 3 4]
 [0 1 5]]
```


