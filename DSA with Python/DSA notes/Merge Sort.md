The Merge Sort algorithm is a divide-and-conquer algorithm that sorts an array by first breaking it down into smaller arrays, and then building the array back together the correct way so that it is sorted.

**Divide:** The algorithm starts with breaking up the array into smaller and smaller pieces until one such sub-array only consists of one element.

**Conquer:** The algorithm merges the small pieces of the array back together by putting the lowest values first, resulting in a sorted array.

The breaking down and building up of the array to sort the array is done recursively.

---
**How it works:**

1. Divide the unsorted array into two sub-arrays, half the size of the original.
2. Continue to divide the sub-arrays as long as the current piece of the array has more than one element.
3. Merge two sub-arrays together by always putting the lowest value first.
4. Keep merging until there are no sub-arrays left.
---
```
def mergeSort(arr):
  if len(arr) <= 1:
    return arr

  mid = len(arr) // 2
  leftHalf = arr[:mid]
  rightHalf = arr[mid:]

  sortedLeft = mergeSort(leftHalf)
  sortedRight = mergeSort(rightHalf)

  return merge(sortedLeft, sortedRight)

def merge(left, right):
  result = []
  i = j = 0

  while i < len(left) and j < len(right):
    if left[i] < right[j]:
      result.append(left[i])
      i += 1
    else:
      result.append(right[j])
      j += 1

  result.extend(left[i:])
  result.extend(right[j:])

  return result

mylist = [3, 7, 6, -10, 15, 23.5, 55, -13]
mysortedlist = mergeSort(mylist)
print("Sorted array:", mysortedlist)

#Output:
Sorted array: [-13, -10, 3, 6, 7, 15, 23.5, 55]
```

---
## Merge Sort without Recursion

Since Merge Sort is a divide and conquer algorithm, recursion is the most intuitive code to use for implementation. The recursive implementation of Merge Sort is also perhaps easier to understand, and uses less code lines in general.

But Merge Sort can also be implemented without the use of recursion, so that there is no function calling itself.

```
def merge(left, right):
  result = []
  i = j = 0

  while i < len(left) and j < len(right):
    if left[i] < right[j]:
      result.append(left[i])
      i += 1
    else:
      result.append(right[j])
      j += 1

  result.extend(left[i:])
  result.extend(right[j:])

  return result

def mergeSort(arr):
  step = 1 # Starting with sub-arrays of length 1
  length = len(arr)

  while step < length:
    for i in range(0, length, 2 * step):
      left = arr[i:i + step]
      right = arr[i + step:i + 2 * step]

      merged = merge(left, right)

      # Place the merged array back into the original array
      for j, val in enumerate(merged):
        arr[i + j] = val

    step *= 2 # Double the sub-array length for the next iteration

  return arr

mylist = [3, 7, 6, -10, 15, 23.5, 55, -13]
mysortedlist = mergeSort(mylist)
print(mysortedlist)

#Output:
[-13, -10, 3, 6, 7, 15, 23.5, 55]
```

---
## Merge Sort Time Complexity

The time complexity for Merge Sort is: $O(n⋅logn)$

And the time complexity is pretty much the same for different kinds of arrays. The algorithm needs to split the array and merge it back together whether it is already sorted or completely shuffled.

Merge Sort performs almost the same every time because the array is split, and merged using comparison, both if the array is already sorted or not.