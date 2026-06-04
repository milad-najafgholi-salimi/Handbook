`map()` and `filter()` are **important Python built-in functions** used for **processing sequences (like lists, tuples, etc.) in a functional style**. They are often taught together with **lambda functions** and appear frequently in **exams and interviews**.

---
## 1. `map()` Function

### What is `map()`?

`map()` **applies a function to every element** in an iterable and returns a **map object** (iterator).

### Syntax
```
map(function, iterable)
```
### Simple Example
```
numbers = [1, 2, 3, 4]

result = map(lambda x: x * 2, numbers)
print(list(result))

#Output:
[2, 4, 6, 8]
```
📌 `map()` **transforms** data.
### Using a Normal Function
```
def square(x):
    return x * x

print(list(map(square, [1, 2, 3])))

#Output:
[1, 4, 9]
```

### Mapping Multiple Iterables
```
a = [1, 2, 3]
b = [4, 5, 6]

result = map(lambda x, y: x + y, a, b)
print(list(result))

#Output:
[5, 7, 9]
```
📌 Stops at the **shortest iterable**.

---
## 2. `filter()` Function

### What is `filter()`?

`filter()` **selects elements** from an iterable based on a **condition**.

### Syntax
```
filter(function, iterable)
```
The function must return **True or False**.
### Simple Example
```
numbers = [1, 2, 3, 4, 5, 6]

result = filter(lambda x: x % 2 == 0, numbers)
print(list(result))

#Output:
[2, 4, 6]
```
📌 `filter()` **reduces** data.
### Using a Normal Function
```
def is_positive(x):
    return x > 0

print(list(filter(is_positive, [-2, 3, -1, 5])))

#Output:
[3, 5]
```

---
## 3. Key Difference Between `map()` and `filter()`
| Feature         | `map()`            | `filter()`                 |
| --------------- | ------------------ | -------------------------- |
| Purpose         | Transform elements | Select elements            |
| Function return | Any value          | True / False               |
| Output size     | Same as input      | Same or smaller            |
| Data change     | Yes                | No (keeps original values) |

---
## 4. `map()` and `filter()` with Lambda (Very Common)
```
nums = [1, 2, 3, 4, 5]

squares = list(map(lambda x: x * x, nums))
evens = list(filter(lambda x: x % 2 == 0, nums))

print(squares)
print(evens)

#Output:
[1, 4, 9, 16, 25]
[2, 4]
```

---
## 5. Return Type (Important!)

Both return **iterators**, not lists.
```
result = map(lambda x: x + 1, [1, 2, 3])
print(result)   # <map object ...>
```
Convert using:
```
list(result)
```

---
## 6. Using `None` as Function

### `filter(None, iterable)`

Removes **false values** (`0`, `False`, `None`, `""`)
```
values = [0, 1, "", "Python", None, True]

print(list(filter(None, values)))

#Output:
[1, 'Python', True]
```

---
## 7. `map()` vs List Comprehension

### `map()`
```
list(map(lambda x: x * 2, nums))
```
### List Comprehension (More Pythonic)
```
[x * 2 for x in nums]
```
📌 List comprehensions are often **more readable**, but `map()` is still widely used.

---
## 8. `filter()` vs List Comprehension

### `filter()`
```
list(filter(lambda x: x > 0, nums))
```
### list(filter(lambda x: x > 0, nums))
```
[x for x in nums if x > 0]
```

---
## 9. Chaining `map()` and `filter()`
```
nums = [1, 2, 3, 4, 5]

result = map(lambda x: x * x,
             filter(lambda x: x % 2 == 0, nums))

print(list(result))

#Output:
[4, 16]
```
Steps:

1. Filter even numbers
    
2. Square them

---
## 10. Common Mistakes

❌ Forgetting to convert to list:
```
print(map(lambda x: x+1, nums))
```
❌ Using `filter()` with non-boolean return:
```
filter(lambda x: x * 2, nums)  # Wrong
```

---
## 11. Exam-Ready Definitions

> `map()` applies a function to each element of an iterable and returns an iterator of results.

> `filter()` selects elements from an iterable for which the function returns True.

---
## 12. When to Use What?

✔ Use `map()` when:

- You want to **transform** every element
    

✔ Use `filter()` when:

- You want to **select** specific elements
    

✔ Use list comprehension when:

- Readability is more important

---
## 13. Final Summary

- `map()` → transform data
    
- `filter()` → select data
    
- Both return iterators
    
- Often used with lambda functions
    
- Can be replaced by list comprehensions