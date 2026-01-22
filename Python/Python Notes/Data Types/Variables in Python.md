## What is a variable in Python? (the real answer)

A **variable is a name (label) bound to an object**.

Not a box.  
Not storage.  
A **label pointing to something in memory**.
```
x = 10
```
This means:

> The name `x` now refers to the integer object `10`.

---
## Variables are not typed — objects are

This is huge:
```
x = 10        # x → int
x = "hello"   # x → str
```
- `x` has no type
    
- the **object** has a type
    

This is why Python is called **dynamically typed**.

---
## Assignment ≠ copying

This is where many bugs come from.
```
a = [1, 2, 3]
b = a
```
Now:

- `a` and `b` point to the **same list**
```
b.append(4)
print(a)  # [1, 2, 3, 4]
```
You didn’t copy the list.  
You copied the **reference**.

---
## How to actually copy

### Shallow copy
```
b = a.copy()
# or
b = a[:]
```
### Deep copy
```
import copy
b = copy.deepcopy(a)
```
Use deep copy only when necessary.

### what is the difference between shallow copy and deep copy?
## The short answer (intuition first)

- **Shallow copy**:  
    Copies the _container_, **not the objects inside it**
    
- **Deep copy**:  
    Copies the _container_ **and everything inside it, recursively**
    

Think:

> Shallow copy = new box, same items  
> Deep copy = new box, new items

## Why this even matters

Because Python variables point to **objects**, and many objects are **mutable**.

If you don’t understand copying, you’ll get bugs that feel _haunted_ 👻

#### Example setup
```
original = [[1, 2], [3, 4]]
```
Memory-wise:
```
original ──► list ──► [list1, list2]
                    ├─► [1, 2]
                    └─► [3, 4]
```
## Shallow copy 

### How to make one
```
copy1 = original.copy()
# or
copy1 = original[:]
# or
import copy
copy1 = copy.copy(original)
```
### What actually happens

- A **new outer list** is created
    
- The **inner lists are shared**
    

Memory picture:
```
copy1 ─────► list ──► same inner lists
original ──► list ──► same inner lists
```
#### Observe the behavior
```
copy1[0].append(99)

print(original)
print(copy1)
```
Output:
```
[[1, 2, 99], [3, 4]]
[[1, 2, 99], [3, 4]]
```
😬 Surprise?

You didn’t modify `original` directly —  
you modified a **shared inner object**.

#### But wait — outer changes don’t affect the original
```
copy1.append([5, 6])

print(original)
print(copy1)
```
Output:
```
[[1, 2], [3, 4]]
[[1, 2], [3, 4], [5, 6]]
```
Why?

- Outer list is different
    
- Inner lists are shared
## Deep copy

### How to make one
```
import copy
copy2 = copy.deepcopy(original)
```
### What actually happens

- New outer list
    
- New inner lists
    
- New objects all the way down
    

Memory picture:
```
copy2 ──► list ──► new list1, new list2
original ─► list ──► old list1, old list2
```
#### Observe the behavior
```
copy2[0].append(99)

print(original)
print(copy2)
```
Output:
```
[[1, 2], [3, 4]]
[[1, 2, 99], [3, 4]]
```
✅ Completely independent  
✅ No shared mutable state
## When shallow copy is enough (very common)

Shallow copy is **fine** when:

- Your structure contains **only immutable objects**
    
- You _want_ shared inner data
    
- You control mutations carefully
    

Example:
```
data = [1, 2, 3]
copy_data = data.copy()
```
No problem — ints are immutable.
## When you MUST use deep copy

Use deep copy when:

- Nested mutable objects
    
- You don’t control all mutations
    
- State isolation is required (configs, snapshots, undo)
    

Examples:

- game state
    
- AI memory snapshots
    
- config templates
    
- concurrent systems
## Performance warning ⚠️

`deepcopy`:

- can be **slow**
    
- can use a lot of memory
    
- copies _everything_
    

Rule of thumb:

> Use the **simplest copy that is safe**

## Custom deep copy (advanced insight)

Not everything can or should be deep-copied automatically.

Python allows control via:
```
__copy__()
__deepcopy__()
```
This matters in serious systems (ORMs, caches, AI agents).

---
Variable rebinding (important!)
```
x = 10
x = x + 1
```
Python does:

1. compute `x + 1`
    
2. create a new object `11`
    
3. rebind `x` to `11`
    

The old `10` is untouched.

---
## Mutability vs variables (connect the dots)

### Immutable objects
```
x = 10
y = x
x += 1

# x → 11
# y → 10
```
Mutable objects
```
x = [1, 2]
y = x
x.append(3)

# both see [1, 2, 3]
```
The variable didn’t change — the **object did**.

---
## Multiple assignment
```
a = b = c = 0
```
⚠️ Dangerous with mutable types:
```
a = b = []
a.append(1)
print(b)  # [1]
```

---
## Tuple unpacking (Python superpower)
```
x, y = 10, 20
```
Swap without temp variable:
```
x, y = y, x
```
Under the hood: tuple packing/unpacking.

---
## Variable scope

### Local scope
```
def f():
    x = 10
```
### Global scope
```
x = 10
```
### Reading is fine

### Writing needs `global`
```
def f():
    global x
    x = 20
```
⚠️ Avoid `global` unless absolutely needed.

---
## Namespaces (what variables really live in)

Variables live in **namespaces**:

- local
    
- global
    
- built-in
```
print(len([1, 2, 3]))
```
`len` comes from the built-in namespace.

---
## Variable lifetime
A variable exists:

- as long as something references the object
    

When references drop to zero → object is garbage collected.
```
x = [1, 2]
del x
```
Object may be freed.

---
## Naming variables (this matters more than you think)

Good:
```
user_count
total_price
is_valid
```
Bad:
```
x1
temp
foo
```
Rules:

- snake_case
    
- meaningful
    
- verbs for functions, nouns for variables

---
## Mental model (remember this forever)

> **Variables are names.  
> Objects hold data.  
> Assignment binds names to objects.**

If you truly get this, Python becomes much simpler.

