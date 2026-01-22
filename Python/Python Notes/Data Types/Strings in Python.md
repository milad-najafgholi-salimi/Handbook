A **string (`str`)** is:

- a sequence of **Unicode characters**
    
- **immutable**
    
- iterable
    
- indexed
```
s = "hello"
type(s)   # <class 'str'>
```
Python strings are **Unicode by default**, so this is fine:
```
s = "سلام 👋"
```

---
## Creating strings

### Quotes
```
"hello"
'hello'
```
No difference — use what reads best.

### Triple quotes (multi-line)
```
text = """This is
a multi-line
string"""
```
Often used for docstrings.

---
## Strings are immutable (VERY important)
You cannot change a string in place:
```
s = "hello"
s[0] = "H"   # ❌ error
```
Instead, Python creates **new strings**:
```
s = "H" + s[1:]
```
This explains a lot of string behavior.

---
## Indexing and slicing
Indexing:
```
s = "python"
s[0]     # 'p'
s[-1]    # 'n'
```
Slicing:
```
s[1:4]   # 'yth'
s[:3]    # 'pyt'
s[3:]    # 'hon'
```
Slicing **never mutates** — it returns a new string.

---
## Iterating over strings
```
for ch in "abc":
    print(ch)
```
Each character is a **string of length 1**.

---
## String concatenation
```
a = "hello"
b = "world"

a + " " + b
```
⚠️ Inefficient in loops:
```
# bad
s = ""
for i in range(1000):
    s += str(i)
```
Better:
```
parts = []
for i in range(1000):
    parts.append(str(i))

s = "".join(parts)
```

---
## Common string methods (you WILL use these)

### Case conversion
```
s.upper()
s.lower()
s.title()
```
### Checking
```
s.startswith("he")
s.endswith("lo")
s.isdigit()
s.isalpha()
```
### Searching
```
s.find("th")      # index or -1
"th" in s         # True / False
```
### Replacing
```
s.replace("py", "my")
```

---
## Splitting and joining (super important)

### Split
```
text = "one,two,three"
l = text.split(",")
print(l)  #Output: ['one', 'two', 'three']
```
### Join
```
",".join(["one", "two", "three"])
```
**Rule to remember:**

> Split breaks strings → lists  
> Join builds strings ← lists

---
## f-strings (modern Python, MUST know)
```
name = "Milad"
age = 22

f"My name is {name} and I am {age}"
```
You can put expressions inside:
```
f"{age + 1}"
```
Readable, fast, clean.

---
## Escaping characters
```
"She said \"hello\""
```
## Raw strings
```
r"C:\new\test"
```
Very useful for regex and paths.

---
## String comparison
```
"apple" < "banana"   # True
```
Lexicographical (dictionary) order, based on Unicode.
Case matters:
```
"a" < "A"   # False
```

---
## Strings and bytes (important distinction)
```
s = "hello"
b = b"hello"
```
- `str` → text (Unicode)
    
- `bytes` → raw data
    

Encoding:
```
b = s.encode("utf-8")
s = b.decode("utf-8")
```
Very important for files, networks, APIs.

---
## Memory & performance notes

- Strings are immutable → safe to share
    
- Python may intern small strings

---
## Common string mistakes

❌ Trying to mutate strings  
❌ Using `+` in loops  
❌ Forgetting encoding/decoding  
❌ Confusing `bytes` with `str`  
❌ Using `.find()` instead of `in`

---
## Mental model (lock this in)

> **A string is an immutable sequence of characters.  
> Every “change” creates a new string.**

If you get that, everything else makes sense.