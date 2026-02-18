The Radix Sort algorithm sorts an array by individual digits, starting with the least significant digit (the rightmost one).

The radix (or base) is the number of unique digits in a number system. In the decimal system we normally use, there are 10 different digits from 0 till 9.

Radix Sort uses the radix so that decimal values are put into 10 different buckets (or containers) corresponding to the digit that is in focus, then put back into the array before moving on to the next digit.

Radix Sort is a non comparative algorithm that only works with non negative integers.

---
**How it works:**

1. Start with the least significant digit (rightmost digit).
2. Sort the values based on the digit in focus by first putting the values in the correct bucket based on the digit in focus, and then put them back into array in the correct order.
3. Move to the next digit, and sort again, like in the step above, until there are no digits left.
---
## Stable Sorting

Radix Sort must sort the elements in a stable way for the result to be sorted correctly.

A stable sorting algorithm is an algorithm that keeps the order of elements with the same value before and after the sorting. Let's say we have two elements "K" and "L", where "K" comes before "L", and they both have value "3". A sorting algorithm is considered stable if element "K" still comes before "L" after the array is sorted.

It makes little sense to talk about stable sorting algorithms for the previous algorithms we have looked at individually, because the result would be same if they are stable or not. But it is important for Radix Sort that the sorting is done in a stable way because the elements are sorted by just one digit at a time.

So after sorting the elements on the least significant digit and moving to the next digit, it is important to not destroy the sorting work that has already been done on the previous digit position, and that is why we need to take care that Radix Sort does the sorting on each digit position in a stable way.

---
```
mylist = [170, 45, 75, 90, 802, 24, 2, 66]
print("Original array:", mylist)
radixArray = [[], [], [], [], [], [], [], [], [], []]
maxVal = max(mylist)
exp = 1

while maxVal // exp > 0:

  while len(mylist) > 0:
    val = mylist.pop()
    radixIndex = (val // exp) % 10
    radixArray[radixIndex].append(val)

  for bucket in radixArray:
    while len(bucket) > 0:
      val = bucket.pop()
      mylist.append(val)

  exp *= 10

print(mylist)

#Output:
Original array: [170, 45, 75, 90, 802, 24, 2, 66]  
[2, 24, 45, 66, 75, 90, 170, 802]
```

---
## Radix Sort Using Other Sorting Algorithms
Radix Sort can actually be implemented together with any other sorting algorithm as long as it is stable. This means that when it comes down to sorting on a specific digit, any stable sorting algorithm will work, such as counting sort or bubble sort.

```
def bubbleSort(arr):
  n = len(arr)
  for i in range(n):
    for j in range(0, n - i - 1):
      if arr[j] > arr[j + 1]:
        arr[j], arr[j + 1] = arr[j + 1], arr[j]

def radixSortWithBubbleSort(arr):
  max_val = max(arr)
  exp = 1

  while max_val // exp > 0:
    radixList = [[],[],[],[],[],[],[],[],[],[]]

    for num in arr:
      radixIndex = (num // exp) % 10
      radixList[radixIndex].append(num)

    for bucket in radixList:
      bubbleSort(bucket)

    i = 0
    for bucket in radixList:
      for num in bucket:
        arr[i] = num
        i += 1

    exp *= 10

mylist = [170, 45, 75, 90, 802, 24, 2, 66]

radixSortWithBubbleSort(mylist)

print(mylist)

#Output:
[2, 24, 45, 66, 75, 90, 170, 802]
```

---
## Radix Sort Time Complexity

The time complexity for Radix Sort is: $O(n⋅k)$

This means that Radix Sort depends both on the values that need to be sorted `n`, and the number of digits in the highest value `k`.

A best case scenario for Radix Sort is if there are lots of values to sort, but the values have few digits. For example if there are more than a million values to sort, and the highest value is 999, with just three digits. In such a case the time complexity $O(n⋅k)$ can be simplified to just $O(n)$.

A worst case scenario for Radix Sort would be if there are as many digits in the highest value as there are values to sort. This is perhaps not a common scenario, but the time complexity would be $O(n^2)$ in this case.

The most average or common case is perhaps if the number of digits `k` is something like $k(n)=logn$. If so, Radix Sort gets time complexity $O(n⋅logn)$. An example of such a case would be if there are 1_000_000 values to sort, and the values have 6 digits.