A Hash Table is a data structure designed to be fast to work with.

The reason Hash Tables are sometimes preferred instead of arrays or linked lists is because searching for, adding, and deleting data can be done really quickly, even for large amounts of data.

In a **Linked list**, finding a person "Milad" takes time because we would have to go from one node to the next, checking each node, until the node with "Milad" is found.

And finding "Milad" in an **array/list** could be fast if we knew the index, but when we only know the name "Milad", we need to compare each element and that takes time.

With a Hash Table however, finding "Milad" is done really fast because there is a way to go directly to where "Milad" is stored, using something called a hash function.

---
## Building A Hash Table from Scratch

To get the idea of what a Hash Table is, let's try to build one from scratch, to store unique first names inside it.

We will build the Hash Table in 5 steps:

1. Create an empty list (it can also be a dictionary or a set).
2. Create a hash function.
3. Inserting an element using a hash function.
4. Looking up an element using a hash function.
5. Handling collisions.

### Step 1: Create an Empty List

To keep it simple, let's create a list with 10 empty elements.
```
my_list = [None, None, None, None, None, None, None, None, None, None]
```
Each of these elements is called a **bucket** in a Hash Table.
### Step 2: Create a Hash Function

We want to store a name directly into its right place in the array, and this is where the **hash function** comes in.

A hash function can be made in many ways, it is up to the creator of the Hash Table. A common way is to find a way to convert the value into a number that equals one of the Hash Table's index numbers, in this case a number from 0 to 9.

In our example we will use the Unicode number of each character, summarize them and do a modulo 10 operation to get index numbers 0-9.
```
def hash_function(value):
  sum_of_chars = 0
  for char in value:
    sum_of_chars += ord(char)

  return sum_of_chars % 10

print("'Milad' has hash code:", hash_function('Milad'))

#Output:
'Milad' has hash code: 7
```
The number returned by the hash function is called the **hash code**.

>**Unicode number:** Everything in our computers are stored as numbers, and the Unicode code number is a unique number that exist for every character. For example, the character `A` has Unicode number `65`.

>**Modulo:** A modulo operation divides a number with another number, and gives us the resulting remainder. So for example, `7 % 3` will give us the remainder `1`. 
In Python and most programming languages, the modolo operator is written as `%`.

### Step 3: Inserting an Element

According to our hash function, "Milad" should be stored at index 7.

Lets create a function that add items to our hash table:
```
my_list = [None, None, None, None, None, None, None, None, None, None]

def hash_function(value):
  sum_of_chars = 0
  for char in value:
    sum_of_chars += ord(char)

  return sum_of_chars % 10

def add(name):
  index = hash_function(name)
  my_list[index] = name


add("Milad")
add("Faraz")
add("Mehrdad")
add("Matin")

print(my_list)

#Output:
['Faraz', None, None, 'Mehrdad', None, 'Matin', None, 'Milad', None, None]
```
### Step 4: Looking up a name

To find "Milad" in the Hash Table, we give the name "Milad" to our hash function. The hash function returns `7`, meaning that "Milad" is stored at index 7.
```
my_list = [None, None, None, None, None, None, None, None, None, None]

def hash_function(value):
  sum_of_chars = 0
  for char in value:
    sum_of_chars += ord(char)

  return sum_of_chars % 10

def add(name):
  index = hash_function(name)
  my_list[index] = name

def contains(name):
  index = hash_function(name)
  return my_list[index] == name

add("Milad")
add("Faraz")
add("Mehrdad")
add("Matin")

print("'Milad' is in the Hash Table:", contains('Milad'))

#Output:
'Milad' is in the Hash Table: True
```
Because we do not have to check element by element to find out if "Milad" is in there, we can just use the hash function to go straight to the right element!
### Step 5: Handling collisions

Let's also add "Nika" to our Hash Table.

We give "Nika" to our hash function, which returns `7`, meaning "Nika" should be stored at index 7.

Trying to store "Nika" in index 7, creates what is called a **collision**, because "Milad" is already stored at index 7.

To fix the collision, we can make room for more elements in the same bucket. Solving the collision problem in this way is called **chaining**, and means giving room for more elements in the same bucket.

Start by creating a new list with the same size as the original list, but with empty buckets:
```
my_list = [
  [],
  [],
  [],
  [],
  [],
  [],
  [],
  [],
  [],
  []
]

def hash_function(value):
  sum_of_chars = 0
  for char in value:
    sum_of_chars += ord(char)

  return sum_of_chars % 10

def add(name):
  index = hash_function(name)
  my_list[index].append(name)

def contains(name):
  index = hash_function(name)
  return my_list[index] == name

add("Milad")
add("Faraz")
add("Mehrdad")
add("Matin")
add("Nika")

print(my_list)

#Output:
[['Faraz'], [], [], ['Mehrdad'], [], ['Matin'], [], ['Milad', 'Nika'], [], []]
```
Searching for "Nika" now takes a little bit longer time, because we also find "Milad" in the same bucket, but still much faster than searching the entire Hash Table.

---
## Uses of Hash Tables

Hash Tables are great for:

- Checking if something is in a collection (like finding a book in a library).
- Storing unique items and quickly finding them (like storing phone numbers).
- Connecting values to keys (like linking names to phone numbers).

The most important reason why Hash Tables are great for these things is that Hash Tables are very fast compared Arrays and Linked Lists, especially for large sets. Arrays and Linked Lists have time complexity `O(n)` for search and delete, while Hash Tables have just `O(1)` on average.

---

## Hash Tables Summarized

Hash Table elements are stored in storage containers called **buckets**.

A **hash function** takes the key of an element to generate a **hash code**.

The hash code says what bucket the element belongs to, so now we can go directly to that Hash Table element: to modify it, or to delete it, or just to check if it exists.

A **collision** happens when two Hash Table elements have the same hash code, because that means they belong to the same **bucket**.

Collision can be solved by **Chaining** by using lists to allow more than one element in the same bucket.