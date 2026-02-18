Linear search (or sequential search) is the simplest search algorithm. It checks each element one by one.

---
**How it works:**

1. Go through the array value by value from the start.
2. Compare each value to check if it is equal to the value we are looking for.
3. If the value is found, return the index of that value.
4. If the end of the array is reached and the value is not found, return -1 to indicate that the value was not found.

---
## Implement Linear Search in Python

In Python, the fastest way check if a value exists in a list is to use the `in` operator.
```
mylist = [3, 7, 2, 9, 5, 1, 8, 4, 6]

if 4 in mylist:
  print("Found!")
else:
  print("Not found!")

#Output:
Found!
```

---
```
def linearSearch(arr, targetVal):
  for i in range(len(arr)):
    if arr[i] == targetVal:
      return i
  return -1

mylist = [3, 7, 2, 9, 5, 1, 8, 4, 6]
x = 4

result = linearSearch(mylist, x)

if result != -1:
  print("Found at index", result)
else:
  print("Not found")
  
#Output:
Found at index 7
```

---
## Linear Search Time Complexity

If Linear Search runs and finds the target value as the first array value in an array with `n` values, only one compare is needed.

But if Linear Search runs through the whole array of n values, without finding the target value, `n` compares are needed.

This means that time complexity for Linear Search is: `O(n)`
