In Python, **`break`** and **`continue`** are **loop control statements**. They change the normal flow of a loop (`for` or `while`).

---
## 1. `break` statement

### What `break` does

- **Immediately exits the loop**
    
- The loop stops completely
    
- Execution continues with the code **after** the loop
#### Example with `for`
```
for i in range(1, 6):
    if i == 3:
        break
    print(i)
```
**Output:**
```
1
2
```
Explanation:

- When `i == 3`, `break` is executed
    
- The loop ends instantly
    
- `3`, `4`, and `5` are never processed
#### Example with `while`
```
count = 1

while count <= 5:
    if count == 4:
        break
    print(count)
    count += 1
```
Stops the loop when `count` reaches 4.

---
### Typical uses of `break`

- Stop searching when an item is found
    
- Exit infinite loops
    
- End a loop early when a condition is met
    

Example (searching):
```
numbers = [4, 7, 9, 2, 5]

for n in numbers:
    if n == 9:
        print("Found!")
        break
    else:
	    print("Not found!")
```

---
## 2. `continue` statement

### What `continue` does

- **Skips the rest of the current iteration**
    
- Goes directly to the **next loop cycle**
    
- The loop itself continues running
#### Example with `for`
```
for i in range(1, 6):
    if i == 3:
        continue
    print(i)
```
**Output:**
```
1
2
4
5
```
Explanation:

- When `i == 3`, Python skips `print(i)`
    
- The loop continues with the next value
#### Example with `while`
```
count = 0

while count < 5:
    count += 1
    if count == 2:
        continue
    print(count)
```
Important:

- The counter is updated **before** `continue`
    
- Otherwise, you risk an infinite loop

---
## 3. `break` vs `continue` (comparison)

| Feature                      | `break` | `continue` |
| ---------------------------- | ------- | ---------- |
| Stops the loop completely    | ✅ Yes   | ❌ No       |
| Skips current iteration only | ❌ No    | ✅ Yes      |
| Used to exit early           | ✅ Yes   | ❌ No       |
| Loop continues after use     | ❌ No    | ✅ Yes      |

---
## 4. `break` and `continue` with `else`

Both affect `else` in loops:
```
for i in range(5):
    if i == 3:
        break
else:
    print("Finished normally")
```
- `else` **does NOT run** because `break` was used
    

But with `continue`:
```
for i in range(5):
    if i == 3:
        continue
    print(i)
else:
    print("Finished normally")
```
- `else` **DOES run**

**Output:**
```
0
1
2
4
Finished normally
```

---
## 5. Common mistakes ❌

### a) Forgetting to update variables with `continue`
```
i = 0
while i < 5:
    if i == 2:
        continue   # ❌ infinite loop
    i += 1
```
Correct version:
```
i = 0
while i < 5:
    i += 1
    if i == 2:
        continue
```
### b) Overusing `break`

Sometimes students use `break` when an `if` is enough.  
Good practice: use `break` **only when you truly want to stop the loop**.

---
## 6. How to explain this in an exam or classroom

Simple analogy:

- **`break`** → _“Stop the loop and leave the room.”_
    
- **`continue`** → _“Skip this step and move to the next round.”_

---
## 7. Quick summary

- Use **`break`** when you want to **exit a loop early**
    
- Use **`continue`** when you want to **skip part of a loop iteration**
    
- Both work in `for` and `while` loops
    
- Be careful with `while` loops to avoid infinite loops