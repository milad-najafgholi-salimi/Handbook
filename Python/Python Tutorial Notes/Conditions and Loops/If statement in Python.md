## Basic Structure of an `if` Statement

The **`if` statement** lets you run a block of code **only if a condition is true**.

### Syntax:
```
if condition:
    # code to execute if the condition is True
```
Example:`
```
age = 18
if age >= 18:
    print("You are an adult!")
```
- **`condition`**: This is the expression that is evaluated. If it is **True**, the indented code block executes.
    
- **Indentation**: The code inside the `if` block must be indented (typically with four spaces or a tab).

---
## `if-else` Statement

If you want to **do something when the condition is true**, and **something else when it’s false**, use an `else` block.

### Syntax:
```
if condition:
    # code to execute if True
else:
    # code to execute if False
```
Example:
```
age = 16
if age >= 18:
    print("You are an adult!")
else:
    print("You are a minor!")
```
Output:
```
You are a minor!
```

---
## `elif` (else if) Statement

If you have **multiple conditions** to check, use `elif` (short for **else if**) to check additional conditions after the initial `if`.

### Syntax:
```
if condition1:
    # code to execute if condition1 is True
elif condition2:
    # code to execute if condition1 is False and condition2 is True
else:
    # code to execute if all conditions are False
```
Example:
```
age = 20
if age < 13:
    print("You are a child.")
elif age < 18:
    print("You are a teenager.")
else:
    print("You are an adult.")
```
Output:
```
You are an adult.
```

---
## Nested `if` Statements

You can also have **`if` statements inside other `if` statements**. This is called **nesting**.

### Syntax:
```
if condition1:
    if condition2:
        # code to execute if both conditions are True
    else:
        # code if condition2 is False
```
Example:
```
age = 20
has_ticket = True

if age >= 18:
    if has_ticket:
        print("You can watch the movie.")
    else:
        print("You need a ticket to watch the movie.")
else:
    print("You are too young to watch the movie.")
```
Output:
```
You can watch the movie.
```

---
## Boolean Expressions in Conditions

Conditions in an `if` statement are often **Boolean expressions** that evaluate to `True` or `False`. Here are some ways to write complex conditions using logical operators.

### a. **Using `and` (logical AND)**

The condition will be true if **both parts** are true.
```
age = 20
has_ticket = True

if age >= 18 and has_ticket:
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```
Output:
```
You can watch the movie.
```
### b. **Using `or` (logical OR)**

The condition will be true if **at least one part** is true.
```
age = 16
has_ticket = False

if age >= 18 or has_ticket:
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```
Output:
```
You cannot watch the movie.
```

### c. **Using `not` (logical NOT)**

The condition will be **reversed** (True becomes False, and False becomes True).
```
is_raining = False

if not is_raining:
    print("It's a nice day!")
else:
    print("Bring an umbrella!")
```
Output:
```
It's a nice day!
```

---
## Combining Multiple Conditions

You can combine conditions with **`and`, `or`, and `not`** to make more complex expressions.

### Example:
```
age = 25
has_ticket = False
is_vip = True

if (age >= 18 and has_ticket) or is_vip:
    print("You can watch the movie.")
else:
    print("You cannot watch the movie.")
```
Output:
```
You can watch the movie.
```

---
## Ternary Conditional (Shortened `if`-`else`)

For simple conditional assignments, you can use a **ternary conditional** (a shorthand `if`-`else`).

### Syntax:
```
value_if_true if condition else value_if_false
```
Example:
```
age = 20
message = "You can vote." if age >= 18 else "You cannot vote."
print(message)
```
Output:
```
You can vote.
```

---
## One-liner `if`-`else` Example

You can also use the **ternary conditional** in one-liners within your code.

### Example:
```
x = 10
print("Positive") if x > 0 else print("Negative or Zero")
```
Output:
```
Positive
```

---
## Checking Multiple Conditions in a Single `if` Block

You can also have **multiple conditions** to check in a single `if` statement using logical operators like `and`, `or`.

### Example:
```
age = 21
has_ticket = True

if age >= 18 and has_ticket:
    print("You can enter the club!")
else:
    print("Sorry, you cannot enter.")
```
Output:
```
You can enter the club!
```

---
## One-liner Exam Definition

> **`if` statements in Python allow conditional execution of code. They check if a condition evaluates to `True`, and if so, execute the associated block of code. They can be extended with `elif` and `else` for handling multiple conditions.**

---
## Common Mistakes Students Make

- **Forgetting to indent code blocks**: Python relies on indentation to define which lines belong to the `if`, `elif`, or `else` blocks. Always indent the code inside.
    
- **Using `=` instead of `==`**: Remember, **`=`** is for assignment, and **`==`** is for comparison.
    
    - `if x = 10:` is wrong. It should be `if x == 10:`.
        
- **Misunderstanding the difference between `if-else` and `elif`**: `elif` is for **multiple conditions**, while `else` is for the **fallback case**.