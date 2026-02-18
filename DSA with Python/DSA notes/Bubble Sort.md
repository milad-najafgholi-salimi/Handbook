Bubble Sort is an algorithm that sorts an array from the lowest value to the highest value.

The word 'Bubble' comes from how this algorithm works, it makes the highest values 'bubble up'.

---
**How it works:**

1. Go through the array, one value at a time.
2. For each value, compare the value with the next value.
3. If the value is higher than the next one, swap the values so that the highest value comes last.
4. Go through the array as many times as there are values in the array.

---
```
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)
for i in range(n-1):
  for j in range(n-i-1):
    if mylist[j] > mylist[j+1]:
      mylist[j], mylist[j+1] = mylist[j+1], mylist[j]

print(mylist)

#Output:
[5, 11, 12, 22, 25, 34, 64, 90]
```

---
## Bubble Sort Improvement

Imagine that the array is almost sorted already, with the lowest numbers at the start, like this for example:   `mylist = [7, 3, 9, 12, 11]`

In this case, the array will be sorted after the first run, but the Bubble Sort algorithm will continue to run, without swapping elements, and that is not necessary.

If the algorithm goes through the array one time without swapping any values, the array must be finished sorted, and we can stop the algorithm, like this:
```
mylist = [7, 3, 9, 12, 11]

n = len(mylist)
for i in range(n-1):
  swapped = False
  for j in range(n-i-1):
    if mylist[j] > mylist[j+1]:
      mylist[j], mylist[j+1] = mylist[j+1], mylist[j]
      swapped = True
  if not swapped:
    break

print(mylist)

#Output:
[3, 7, 9, 11, 12]
```

---
## Bubble Sort Time Complexity

The Bubble Sort algorithm loops through every value in the array, comparing it to the value next to it. So for an array of `n` values, there must be `n` such comparisons in one loop.

And after one loop, the array is looped through again and again `n` times.

This means there are `n⋅n` comparisons done in total, so the time complexity for Bubble Sort is: O($n^2$)

The run time increases really fast when the size of the array is increased.
