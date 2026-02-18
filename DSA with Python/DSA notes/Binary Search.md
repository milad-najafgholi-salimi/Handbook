The Binary Search algorithm searches through a **sorted** array and returns the index of the value it searches for.

---
Binary Search is much faster than Linear Search, but requires a sorted array to work.

The Binary Search algorithm works by checking the value in the center of the array. If the target value is lower, the next value to check is in the center of the left half of the array. This way of searching means that the search area is always half of the previous search area, and this is why the Binary Search algorithm is so fast.

This process of halving the search area happens until the target value is found, or until the search area of the array is empty.

---
**How it works:**

1. Check the value in the center of the array.
2. If the target value is lower, search the left half of the array. If the target value is higher, search the right half.
3. Continue step 1 and 2 for the new reduced part of the array until the target value is found or until the search area is empty.
4. If the value is found, return the target value index. If the target value is not found, return -1.

---
```
def binarySearch(arr, targetVal):
  left = 0
  right = len(arr) - 1

  while left <= right:
    mid = (left + right) // 2

    if arr[mid] == targetVal:
      return mid

    if arr[mid] < targetVal:
      left = mid + 1
    else:
      right = mid - 1

  return -1

mylist = [1, 3, 5, 7, 9, 11, 13, 15, 17, 19]
x = 11

result = binarySearch(mylist, x)

if result != -1:
  print("Found at index", result)
else:
  print("Not found")

#Output:
Found at index 5
```

---
## Binary Search Time Complexity

Each time Binary Search checks a new value to see if it is the target value, the search area is halved.

This means that even in the worst case scenario where Binary Search cannot find the target value, it still only needs $log_2n$ comparisons to look through a sorted array of n values.

Time complexity for Binary Search is: O($log_2n$)

>**Note:** When writing time complexity using Big O notation we could also just have written O(logn), but O($log_2n$) reminds us that the array search area is halved for every new comparison, which is the basic concept of Binary Search, so we will just keep the base 2 indication in this case.

