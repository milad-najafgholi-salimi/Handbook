The Selection Sort algorithm finds the lowest value in an array and moves it to the front of the array.

The algorithm looks through the array again and again, moving the next lowest values to the front, until the array is sorted.

---
**How it works:**

1. Go through the array to find the lowest value.
2. Move the lowest value to the front of the unsorted part of the array.
3. Go through the array again as many times as there are values in the array.

---
```
mylist = [64, 34, 25, 5, 22, 11, 90, 12]

n = len(mylist)
for i in range(n-1):
  min_index = i
  for j in range(i+1, n):
     if mylist[j] < mylist[min_index]:
       min_index = j
  min_value = mylist.pop(min_index)
  mylist.insert(i, min_value)

print(mylist)

#Output:
[5, 11, 12, 22, 25, 34, 64, 90]
```

---
## Selection Sort Shifting Problem
The Selection Sort algorithm can be improved a little bit more.

In the code above, the lowest value element is removed, and then inserted in front of the array.

Each time the next lowest value array element is removed, all following elements must be shifted one place down to make up for the removal.

These shifting operation takes a lot of time, and we are not even done yet! After the lowest value (5) is found and removed, it is inserted at the start of the array, causing all following values to shift one position up to make space for the new value, like the image below shows.

>**Note:** You will not see these shifting operations happening in the code if you are using a high level programming language such as Python or Java, but the shifting operations are still happening in the background. Such shifting operations require extra time for the computer to do, which can be a problem.

---
## Solution: Swap Values!

Instead of all the shifting, swap the lowest value (5) with the first value (64).

We can swap values because the lowest value ends up in the correct position, and it does not matter where we put the other value we are swapping with, because it is not sorted yet.

---
## Selection Sort Improvement
```
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)
for i in range(n):
  min_index = i
  for j in range(i+1, n):
     if mylist[j] < mylist[min_index]:
       min_index = j
  mylist[i], mylist[min_index] = mylist[min_index], mylist[i]

print(mylist)

#Output:
[5, 11, 12, 22, 25, 34, 64, 90]
```

---
## Selection Sort Time Complexity
Selection Sort sorts an array of `n` values.

On average, about $\frac{n}{2}$ elements are compared to find the lowest value in each loop.

And Selection Sort must run the loop to find the lowest value approximately `n` times.

We get time complexity: $O(\frac{n}{2}⋅n)$=$O(n^2)$
