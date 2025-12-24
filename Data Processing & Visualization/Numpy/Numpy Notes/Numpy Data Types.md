## Data Types in NumPy

NumPy has some extra data types, and refer to data types with one character, like `i` for integers, `u` for unsigned integers etc.

Below is a list of all data types in NumPy and the characters used to represent them.
- `i` - integer
- `b` - boolean
- `u` - unsigned integer
- `f` - float
- `c` - complex float
- `m` - timedelta
- `M` - datetime
- `O` - object
- `S` - string
- `U` - unicode string
- `V` - fixed chunk of memory for other type ( void )

---
## Checking the Data Type of an Array

The NumPy array object has a property called `dtype` that returns the data type of the array:

Example:
```
import numpy as np  
  
arr = np.array([1, 2, 3, 4])  
print(arr.dtype)

#Output:
int64
```
Example:
```
import numpy as np  
  
arr = np.array(['apple', 'banana', 'cherry'])  
  
print(arr.dtype)

#Output:
<U6
```

