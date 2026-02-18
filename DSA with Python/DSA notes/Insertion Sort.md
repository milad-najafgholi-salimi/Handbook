The Insertion Sort algorithm uses one part of the array to hold the sorted values, and the other part of the array to hold values that are not sorted yet.

The algorithm takes one value at a time from the unsorted part of the array and puts it into the right place in the sorted part of the array, until the array is sorted.

---
**How it works:**

1. Take the first value from the unsorted part of the array.
2. Move the value into the correct place in the sorted part of the array.
3. Go through the unsorted part of the array again as many times as there are values.
---
```
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)
for i in range(1,n):
  insert_index = i
  current_value = mylist.pop(i)
  for j in range(i-1, -1, -1):
    if mylist[j] > current_value:
      insert_index = j
  mylist.insert(insert_index, current_value)

print(mylist)

#Output:
[5, 11, 12, 22, 25, 34, 64, 90]
```

---
## Insertion Sort Improvement

Insertion Sort can be improved a little bit more.

The way the code above first removes a value and then inserts it somewhere else is intuitive. It is how you would do Insertion Sort physically with a hand of cards for example. If low value cards are sorted to the left, you pick up a new unsorted card, and insert it in the correct place between the other already sorted cards.

The problem with this way of programming it is that when removing a value from the array, all elements above must be shifted one index place down.

And when inserting the removed value into the array again, there are also many shift operations that must be done: all following elements must shift one position up to make place for the inserted value.

These shifting operations can take a lot of time, especially for an array with many elements.

>**Hidden memory shifts:** You will not see these shifting operations happening in the code if you are using a high-level programming language such as Python or JavaScript, but the shifting operations are still happening in the background. Such shifting operations require extra time for the computer to do, which can be a problem.

---
## Improved Solution

We can avoid most of these shift operations by only shifting the values necessary:

```
mylist = [64, 34, 25, 12, 22, 11, 90, 5]

n = len(mylist)
for i in range(1,n):
  insert_index = i
  current_value = mylist[i]
  for j in range(i-1, -1, -1):
     if mylist[j] > current_value:
       mylist[j+1] = mylist[j]
       insert_index = j
     else:
       break
  mylist[insert_index] = current_value

print(mylist)

#Output:
[5, 11, 12, 22, 25, 34, 64, 90]
```
What is also done in the code above is to break out of the inner loop. That is because there is no need to continue comparing values when we have already found the correct place for the current value.

---
## Insertion Sort Time Complexity

_Insertion Sort_ sorts an array of `n` values.

On average, each value must be compared to about $\frac{n}{2}$ other values to find the correct place to insert it.

_Insertion Sort_ must run the loop to insert a value in its correct place approximately `n` times.

We get time complexity for Insertion Sort: $O(\frac{n}{2}⋅n)=O(n^2)$

For Insertion Sort, there is a big difference between best, average and worst case scenarios.

