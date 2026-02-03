In Python, the **`while` loop** is used to **repeat a block of code as long as a condition remains true**.

---
## 1. Basic idea of a `while` loop

The general syntax is:
```
while condition:
    # code to repeat
```
- **`condition`** is a Boolean expression (`True` or `False`)
    
- The loop **keeps running while the condition is `True`**
    
- When the condition becomes `False`, the loop stops

---
## 2. Simple example
```
count = 1

while count <= 5:
    print(count)
    count += 1
```
**Output:**
```
1
2
3
4
5
```
Explanation:

- `count <= 5` is checked before each iteration
    
- `count += 1` is essential to avoid an infinite loop

---
## 3. Infinite loops ⚠️

If the condition never becomes false, the loop runs forever.
```
while True:
    print("This will run forever")
```
This is sometimes **intentional**, for example in:

- Games
    
- Servers
    
- Input validation loops
    

To stop an infinite loop, use `break`.

---
## 4. Using `break` and `continue`

### `break` – exit the loop immediately
```
while True:
    user_input = input("Enter 'q' to quit: ")
    if user_input == 'q':
        break

```
### `continue` – skip the rest of the loop body
```
count = 0

while count < 5:
    count += 1
    if count == 3:
        continue
    print(count)
```
Skips printing `3`.

---
## 5. `while` with `else`

Just like `for`, `while` can have an `else` block.
```
count = 1

while count <= 3:
    print(count)
    count += 1
else:
    print("Loop ended normally")
```
`else` runs **only if the loop was not stopped by `break`**

---
## 6. Input validation (very common use case)
```
age = -1

while age < 0:
    age = int(input("Enter a valid age: "))
```
This keeps asking until the user enters a valid value.

| `for` loop                              | `while` loop                                |
| --------------------------------------- | ------------------------------------------- |
| Used when number of iterations is known | Used when repetitions depend on a condition |
| Iterates over sequences                 | Controlled by a Boolean condition           |
| Cleaner for lists/ranges                | Better for user input & unknown loops       |

### Example comparison
```
# for loop
for i in range(5):
    print(i)

# while loop
i = 0
while i < 5:
    print(i)
    i += 1
```
Both produce the same output.

---
## 8. Common mistakes ❌

### a) Forgetting to update the condition variable
```
i = 0
while i < 5:
    print(i)
# i never changes → infinite loop
```
### b) Wrong condition
```
while x = 5:   # ❌ assignment instead of comparison
```
Correct version:
```
while x == 5:
```

---
## 9. Nested `while` loops
```
i = 1
while i <= 3:
    j = 1
    while j <= 2:
        print(i, j)
        j += 1
    i += 1
```
Used for:

- Tables
    
- Patterns
    
- Multi-step processes

---
## 10. When should you use a `while` loop?

Use a `while` loop when:

- You **don’t know in advance** how many times the loop will run
    
- The loop depends on **user input**
    
- You need a loop that runs **until a condition changes**
    

Use a `for` loop when:

- You are looping over a list, string, or range
    
- The number of iterations is predictable

---
## 11. Teaching perspective

A good way to explain `while` to students:

> “A `while` loop keeps asking _‘Should I continue?’_ before every repetition.  
> As long as the answer is **yes (True)**, the loop continues.”

