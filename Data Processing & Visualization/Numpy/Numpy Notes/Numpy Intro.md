- NumPy is a Python library.
- NumPy is used for working with arrays.
- NumPy is short for "Numerical Python".

---
## Why Use NumPy?

In Python we have lists that serve the purpose of arrays, but they are slow to process.

NumPy aims to provide an array object that is up to 50x faster than traditional Python lists.

The array object in NumPy is called `ndarray`, it provides a lot of supporting functions that make working with `ndarray` very easy.

Arrays are very frequently used in data science, where speed and resources are very important.

---
## Why is NumPy Faster Than Lists?

NumPy arrays are stored at one continuous place in memory unlike lists, so processes can access and manipulate them very efficiently.

This behavior is called locality of reference in computer science.

This is the main reason why NumPy is faster than lists. Also it is optimized to work with latest CPU architectures.

---
## Import NumPy

Once NumPy is installed, import it in your applications by adding the `import` keyword. Now NumPy is imported and ready to use:
```
import numpy

arr = numpy.array([1, 2, 3, 4, 5])
print(arr)    #Output: [1 2 3 4 5]
```

---
## NumPy alias

NumPy is usually imported under the `np` alias.
>**alias:** In Python alias are an alternate name for referring to the same thing.

Create an alias with the `as` keyword while importing:
```
import numpy as np

arr = np.array([1, 2, 3, 4, 5])
print(arr)
```

---
## Checking NumPy Version
Use:
```
import numpy as np  
  
print(np.__version__)
```
