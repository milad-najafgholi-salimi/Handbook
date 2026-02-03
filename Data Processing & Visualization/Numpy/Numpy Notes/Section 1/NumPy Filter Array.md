## Filtering Arrays

Getting some elements out of an existing array and creating a new array out of them is called _filtering_.

In NumPy, you filter an array using a _boolean index list_.
>A _boolean index list_ is a list of booleans corresponding to indexes in the array.

If the value at an index is `True` that element is contained in the filtered array, if the value at that index is `False` that element is excluded from the filtered array.
### Example
- Create an array from the elements on index 0 and 2:
```
import numpy as np

arr = np.array([41, 42, 43, 44])

x = arr[[True, False, True, False]]

print(x)

#Output:
[41 43]
```

---
## Creating the Filter Array

In the example above we hard-coded the `True` and `False` values, but the common use is to create a filter array based on conditions.

### Example
- Create a filter array that will return only values higher than 42:
```
import numpy as np

arr = np.array([41, 42, 43, 44])

# Create an empty list
filter_arr = []

# go through each element in arr
for element in arr:
  # if the element is higher than 42, set the value to True, otherwise False:
  if element > 42:
    filter_arr.append(True)
  else:
    filter_arr.append(False)

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)

#Output:
[False, False, True, True]  
[43 44]
```
### Example
- Create a filter array that will return only even elements from the original array:
```
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])

# Create an empty list
filter_arr = []

# go through each element in arr
for element in arr:
  # if the element is completely divisble by 2, set the value to True, otherwise False
  if element % 2 == 0:
    filter_arr.append(True)
  else:
    filter_arr.append(False)

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)

#Output:
[False, True, False, True, False, True, False]  
[2 4 6]
```

---
## Creating Filter Directly From Array
We can directly substitute the array instead of the iterable variable in our condition and it will work just as we expect it to.

### Example
- Create a filter array that will return only values higher than 42:
```
import numpy as np

arr = np.array([41, 42, 43, 44])

filter_arr = arr > 42

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)

#Output:
[False False  True  True]
[43 44]
```
### Example
- Create a filter array that will return only even elements from the original array:
```
import numpy as np

arr = np.array([1, 2, 3, 4, 5, 6, 7])

filter_arr = arr % 2 == 0

newarr = arr[filter_arr]

print(filter_arr)
print(newarr)

#Output:
[False  True False  True False  True False]
[2 4 6]
```