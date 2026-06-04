The `itertools` module is a powerful part of Python's standard library that provides fast, memory-efficient tools for working with iterators. It's inspired by constructs from functional programming languages like Haskell and APL.

---
## Why Use itertools?

- **Memory efficient** - processes items one at a time
    
- **Fast** - implemented in C
    
- **Composable** - functions can be combined
    
- **Clean code** - expressive and readable
    
---
## Installation and Import

No installation needed - it's in the standard library:
```
import itertools
# or import specific functions
from itertools import count, cycle, repeat
```

---
## 1. Infinite Iterators

### `count(start=0, step=1)`

Generates consecutive numbers indefinitely.
```
from itertools import count

for i in count(5, 2):
    if i > 15:
        break
    print(i, end=' ')  # Output: 5 7 9 11 13 15

# Practical use: enumerate with custom start
for idx, value in zip(count(1), ['a', 'b', 'c']):
    print(f"{idx}: {value}")
```
### `cycle(iterable)`

Cycles through an iterable indefinitely.
```
from itertools import cycle

colors = cycle(['red', 'green', 'blue'])
for i, color in zip(range(7), colors):
    print(f"{i}: {color}")
# Output: 0: red, 1: green, 2: blue, 3: red, 4: green, 5: blue, 6: red
```
### `repeat(object[, times])`

Repeats an object indefinitely or a specified number of times.
```
from itertools import repeat

list(repeat(10, 3))  # Output: [10, 10, 10]

# Useful for creating constant streams
squares = list(map(pow, range(5), repeat(2)))  # [0, 1, 4, 9, 16]
```

---
## 2. Finite Iterators

### `accumulate(iterable[, func])`

Returns accumulated sums or results of binary function.
```
from itertools import accumulate
import operator

list(accumulate([1, 2, 3, 4]))  # Output: [1, 3, 6, 10]
list(accumulate([1, 2, 3, 4], operator.mul))  # Output: [1, 2, 6, 24]
list(accumulate([5, 3, 8, 1], max))  # Output: [5, 5, 8, 8]
```
### `chain(*iterables)`

Chains multiple iterables together.
```
from itertools import chain

list(chain([1, 2], [3, 4], [5, 6]))  # Output: [1, 2, 3, 4, 5, 6]
list(chain.from_iterable([[1, 2], [3, 4], [5, 6]]))  # Same as above

# Flatten nested lists
nested = [[1, 2], [3, 4], [5, 6]]
flattened = list(chain.from_iterable(nested))
```
### `compress(data, selectors)`

Filters data based on selector values.
```
from itertools import compress

data = ['a', 'b', 'c', 'd', 'e']
selectors = [1, 0, 1, 0, 1]
list(compress(data, selectors))  # Output: ['a', 'c', 'e']
```
### `dropwhile(predicate, iterable)`

Drops elements while predicate is true, then returns rest.
```
from itertools import dropwhile

list(dropwhile(lambda x: x < 5, [1, 4, 6, 4, 1]))  # Output: [6, 4, 1]
# Stops dropping after first element where predicate is false
```
### `takewhile(predicate, iterable)`

Takes elements while predicate is true, stops when false.
```
from itertools import takewhile

list(takewhile(lambda x: x < 5, [1, 4, 6, 4, 1]))  # Output: [1, 4]
```
### `filterfalse(predicate, iterable)`

Returns elements where predicate is false.
```
from itertools import filterfalse

list(filterfalse(lambda x: x % 2, range(10)))  # Even numbers: [0, 2, 4, 6, 8]
```
### `groupby(iterable, key=None)`

Groups consecutive elements with the same key.
```
from itertools import groupby

# Sort before grouping (important!)
data = [('a', 1), ('b', 2), ('a', 3), ('b', 4)]
data.sort(key=lambda x: x[0])

for key, group in groupby(data, key=lambda x: x[0]):
    print(key, list(group))
# Output:
# a [('a', 1), ('a', 3)]
# b [('b', 2), ('b', 4)]
```
### `islice(iterable, stop)` or `islice(iterable, start, stop[, step])`

Slices an iterator.
```
from itertools import islice

# Like list slicing but for iterators
list(islice(range(10), 5))        # [0, 1, 2, 3, 4]
list(islice(range(10), 2, 8))      # [2, 3, 4, 5, 6, 7]
list(islice(range(10), 2, 8, 2))   # [2, 4, 6]
```
### `starmap(function, iterable)`

Maps function using arguments from iterable.
```
from itertools import starmap

list(starmap(pow, [(2, 3), (3, 2), (10, 3)]))  # [8, 9, 1000]

# vs regular map
list(map(pow, [2, 3, 10], [3, 2, 3]))  # Same result
```
### `tee(iterable, n=2)`

Returns n independent iterators from a single iterable.
```
from itertools import tee

iter1, iter2 = tee([1, 2, 3, 4], 2)
list(iter1)  # [1, 2, 3, 4]
list(iter2)  # [1, 2, 3, 4] (independent)
```
### `zip_longest(*iterables, fillvalue=None)`

Like zip but fills missing values.
```
from itertools import zip_longest

list(zip_longest('AB', 'xyz', fillvalue='-'))  # [('A', 'x'), ('B', 'y'), ('-', 'z')]
```

---
## 3. Combinatoric Iterators

### `product(*iterables, repeat=1)`

Cartesian product of input iterables.
```
from itertools import product

list(product('AB', [1, 2]))  # [('A', 1), ('A', 2), ('B', 1), ('B', 2)]

# With repeat
list(product([0, 1], repeat=2))  # [(0,0), (0,1), (1,0), (1,1)]

# Equivalent to nested loops
for p in product('AB', repeat=3):
    print(''.join(p), end=' ')  # AAA AAB ABA ABB BAA BAB BBA BBB
```
### `permutations(iterable, r=None)`

All possible orderings (length r).
```
from itertools import permutations

list(permutations('ABC', 2))  # [('A','B'), ('A','C'), ('B','A'), ('B','C'), ('C','A'), ('C','B')]
list(permutations(range(3)))  # 3! = 6 permutations
```
### `combinations(iterable, r)`

All combinations (order doesn't matter).
```
from itertools import combinations

list(combinations('ABC', 2))  # [('A','B'), ('A','C'), ('B','C')]
# Notice: ('B','A') not included - order doesn't matter
```
### `combinations_with_replacement(iterable, r)`

Combinations where elements can be repeated.
```
from itertools import combinations_with_replacement

list(combinations_with_replacement('ABC', 2))  # [('A','A'), ('A','B'), ('A','C'), ('B','B'), ('B','C'), ('C','C')]
```

---
## Practical Examples

### Example 1: Rolling Window
```
from itertools import islice, tee

def sliding_window(iterable, n):
    """Generate sliding windows of size n over iterable"""
    iterables = tee(iterable, n)
    for i, it in enumerate(iterables):
        for _ in range(i):
            next(it, None)
    return zip(*iterables)

list(sliding_window(range(5), 3))  # [(0,1,2), (1,2,3), (2,3,4)]
```
### Example 2: Pagination
```
from itertools import islice

def paginate(iterable, page_size):
    """Split iterable into pages of fixed size"""
    it = iter(iterable)
    while True:
        page = list(islice(it, page_size))
        if not page:
            break
        yield page

list(paginate(range(10), 3))  # [[0,1,2], [3,4,5], [6,7,8], [9]]
```
### Example 3: Data Analysis
```
from itertools import groupby, filterfalse

# Process log entries
logs = [
    {'level': 'INFO', 'msg': 'Started'},
    {'level': 'ERROR', 'msg': 'Failed'},
    {'level': 'INFO', 'msg': 'Processing'},
    {'level': 'WARN', 'msg': 'Low memory'},
    {'level': 'ERROR', 'msg': 'Timeout'}
]

# Group by log level
logs.sort(key=lambda x: x['level'])
for level, group in groupby(logs, key=lambda x: x['level']):
    print(f"{level}: {len(list(group))} entries")

# Filter out INFO logs
non_info = filterfalse(lambda x: x['level'] == 'INFO', logs)
```

---
## Performance Tips

1. **itertools functions return iterators**, not lists - use `list()` when you need actual lists
    
2. **Chain operations** for complex pipelines
    
3. **Use `tee()` carefully** - it stores values in memory
    
4. **Remember to sort before `groupby()`** - it groups consecutive elements only
    

## Summary Table
|Category|Function|Description|
|---|---|---|
|**Infinite**|`count()`|Count from start with step|
||`cycle()`|Cycle through iterable|
||`repeat()`|Repeat object|
|**Finite**|`accumulate()`|Running totals|
||`chain()`|Chain iterables|
||`compress()`|Filter with selectors|
||`dropwhile()`|Drop while condition true|
||`filterfalse()`|Filter false values|
||`groupby()`|Group consecutive items|
||`islice()`|Slice iterator|
||`starmap()`|Map with unpacked args|
||`takewhile()`|Take while condition true|
||`tee()`|Create multiple iterators|
||`zip_longest()`|Zip with fill values|
|**Combinatoric**|`product()`|Cartesian product|
||`permutations()`|All orderings|
||`combinations()`|All combinations|
||`combinations_with_replacement()`|Combinations with repeats|
