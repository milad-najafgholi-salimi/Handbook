The Counting Sort algorithm sorts an array by counting the number of times each value occurs.

Counting Sort does not compare values like the previous sorting algorithms we have looked at, and only works on non negative integers.

**One more thing:** We need to find out what the highest value in the array is, so that the counting array can be created with the correct size. For example, if the highest value is 5, the counting array must be 6 elements in total, to be able count all possible non negative integers 0, 1, 2, 3, 4 and 5.

---
**How it works:**

1. Create a new array for counting how many there are of the different values.
2. Go through the array that needs to be sorted.
3. For each value, count it by increasing the counting array at the corresponding index.
4. After counting the values, go through the counting array to create the sorted array.
5. For each count in the counting array, create the correct number of elements, with values that correspond to the counting array index.

---
## Conditions for Counting Sort

These are the reasons why Counting Sort is said to only work for a limited range of non-negative integer values:

- **Integer values:** Counting Sort relies on counting occurrences of distinct values, so they must be integers. With integers, each value fits with an index (for non negative values), and there is a limited number of different values, so that the number of possible different values k is not too big compared to the number of values n.
- **Non negative values:** Counting Sort is usually implemented by creating an array for counting. When the algorithm goes through the values to be sorted, value x is counted by increasing the counting array value at index x. If we tried sorting negative values, we would get in trouble with sorting value -3, because index -3 would be outside the counting array.
- **Limited range of values:** If the number of possible different values to be sorted k is larger than the number of values to be sorted n, the counting array we need for sorting will be larger than the original array we have that needs sorting, and the algorithm becomes ineffective.

---
```
def countingSort(arr):
  max_val = max(arr)
  count = [0] * (max_val + 1)

  while len(arr) > 0:
    num = arr.pop(0)
    count[num] += 1

  for i in range(len(count)):
    while count[i] > 0:
      arr.append(i)
      count[i] -= 1

  return arr

mylist = [4, 2, 2, 6, 3, 3, 1, 6, 5, 2, 3]
mysortedlist = countingSort(mylist)
print(mysortedlist)

#Output:
[1, 2, 2, 2, 3, 3, 3, 4, 5, 6, 6]
```

---
## Counting Sort Time Complexity

How fast the Counting Sort algorithm runs depends on both the range of possible values `k` and the number of values `n`.

In general, time complexity for Counting Sort is $O(n+k)$.

In a best case scenario, the range of possible different values `k` is very small compared to the number of values `n` and Counting Sort has time complexity $O(n)$.

But in a worst case scenario, the range of possible different values `k` is very big compared to the number of values `n` and Counting Sort can have time complexity $O(n^2)$ or even worse.

As you can see, it is important to consider the range of values compared to the number of values to be sorted before choosing Counting Sort as your algorithm. Also, as mentioned at the top of the page, keep in mind that Counting Sort only works for non negative integer values.

As mentioned previously: if the numbers to be sorted varies a lot in value (large k), and there are few numbers to sort (small n), the Counting Sort algorithm is not effective.
