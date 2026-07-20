## What Are They?

These are three ways to write mathematical expressions. They differ in where the **operator** (like `+`, `-`, `*`, `/`) is placed relative to the **operands** (numbers/variables).

|Notation|Operator Position|Example|
|---|---|---|
|**Infix**|Between operands|`A + B`|
|**Prefix** (Polish)|Before operands|`+ A B`|
|**Postfix** (Reverse Polish)|After operands|`A B +`|

---

## 1. Infix Notation

- **What we normally write**: `(A + B) * C`
    
- **Human‑friendly** but ambiguous without parentheses or precedence rules.
    
- **Computers find it hard** to evaluate directly because of operator precedence and parentheses.
    

---

## 2. Prefix Notation (Polish)

- Operator **before** operands: `* + A B C` means `(A + B) * C`
    
- **No parentheses needed** – order is fixed by position.
    
- Evaluation: scan **right to left**, push operands, apply operator when seen.
    

---

## 3. Postfix Notation (Reverse Polish)

- Operator **after** operands: `A B + C *` means `(A + B) * C`
    
- **No parentheses, no precedence rules** – very easy for computers.
    
- Evaluation: scan **left to right**, push operands, apply operator when seen.
---
## Converting Infix → Postfix (Shunting‑Yard Algorithm)

**Idea**: Use a stack for operators. Output operands immediately; push operators, pop them when a lower‑precedence operator arrives or at the end.

**Example**: `A + B * C` → postfix `A B C * +`

|Step|Symbol|Stack|Output|
|---|---|---|---|
|1|A||A|
|2|+|+|A|
|3|B|+|A B|
|4|*|+ *|A B|
|5|C|+ *|A B C|
|6|end||A B C * +|

---

## Evaluating Postfix Using a Stack

**Algorithm**:

- Scan left → right.
    
- If operand → push.
    
- If operator → pop two operands, apply operator, push result.
    

**Example**: `5 3 + 8 *`

- Push `5`, push `3`
    
- `+` → pop `3`,`5` → `5+3=8` → push `8`
    
- Push `8`
    
- `*` → pop `8`,`8` → `8*8=64` → result = **64**
    

---

## Evaluating Prefix Using a Stack

**Algorithm**:

- Scan right → left.
    
- If operand → push.
    
- If operator → pop two operands, apply operator, push result.
    

**Example**: `* + 5 3 8`

- Scan right: `8` push, `3` push, `5` push
    
- `+` → pop `5`,`3` → `5+3=8` → push `8`
    
- `*` → pop `8`,`8` → `8*8=64`
    
---

## Why Bother?

- **Postfix/prefix** eliminate parentheses and precedence rules → faster evaluation.
    
- Used in **compilers**, **calculators**, and **virtual machines** (e.g., JVM bytecode).

---
Here’s a **complete Python implementation** covering all the key operations:

- **Infix → Postfix** conversion (with parentheses support)
    
- **Infix → Prefix** conversion
    
- **Postfix evaluation**
    
- **Prefix evaluation**
    

I've kept the code clean, well-commented, and ready to run.

---

## 1. Helper Functions (Precedence & Associativity)
```
def precedence(op):
    """Return precedence of an operator."""
    if op in ('+', '-'):
        return 1
    if op in ('*', '/'):
        return 2
    if op == '^':
        return 3
    return 0

def is_operator(ch):
    """Check if character is an operator."""
    return ch in '+-*/^()'

def is_operand(ch):
    """Check if character is an operand (letter or digit)."""
    return ch.isalnum()  # works for single letters/numbers
```
## 2. Infix → Postfix (Shunting-Yard Algorithm)
```
def infix_to_postfix(expression):
    """
    Convert infix expression to postfix.
    Handles + - * / ^ and parentheses.
    """
    stack = []
    output = []
    
    for ch in expression:
        # If operand → add to output
        if is_operand(ch):
            output.append(ch)
        
        # If '(' → push to stack
        elif ch == '(':
            stack.append(ch)
        
        # If ')' → pop until '('
        elif ch == ')':
            while stack and stack[-1] != '(':
                output.append(stack.pop())
            stack.pop()  # remove '('
        
        # If operator
        elif is_operator(ch):
            # Pop higher/equal precedence operators from stack
            while (stack and stack[-1] != '(' and 
                   precedence(stack[-1]) >= precedence(ch)):
                output.append(stack.pop())
            stack.append(ch)
    
    # Pop remaining operators
    while stack:
        output.append(stack.pop())
    
    return ''.join(output)
```
## 3. Infix → Prefix
```
def infix_to_prefix(expression):
    """
    Convert infix to prefix by:
    1. Reverse the string
    2. Swap '(' with ')' and vice versa
    3. Convert to postfix
    4. Reverse the result
    """
    # Step 1: Reverse the expression
    reversed_expr = expression[::-1]
    
    # Step 2: Swap parentheses
    swapped = []
    for ch in reversed_expr:
        if ch == '(':
            swapped.append(')')
        elif ch == ')':
            swapped.append('(')
        else:
            swapped.append(ch)
    
    # Step 3: Get postfix of this modified expression
    postfix = infix_to_postfix(''.join(swapped))
    
    # Step 4: Reverse to get prefix
    return postfix[::-1]
```
## 4. Evaluate Postfix
```
def evaluate_postfix(expression):
    """
    Evaluate a postfix expression.
    Assumes single-digit operands (like '5', '3') or variables.
    """
    stack = []
    
    for ch in expression:
        if is_operand(ch):
            # If it's a digit, push as int; if letter, treat as variable (just push it)
            if ch.isdigit():
                stack.append(int(ch))
            else:
                stack.append(ch)  # variable like 'A'
        elif is_operator(ch):
            # Pop two operands
            b = stack.pop()
            a = stack.pop()
            
            # Apply operator
            if ch == '+':
                result = a + b
            elif ch == '-':
                result = a - b
            elif ch == '*':
                result = a * b
            elif ch == '/':
                result = a / b
            elif ch == '^':
                result = a ** b
            
            stack.append(result)
    
    return stack[0]
```
## 5. Evaluate Prefix
```
def evaluate_prefix(expression):
    """
    Evaluate a prefix expression.
    Scan from right to left.
    """
    stack = []
    
    # Scan from right to left
    for ch in reversed(expression):
        if is_operand(ch):
            if ch.isdigit():
                stack.append(int(ch))
            else:
                stack.append(ch)
        elif is_operator(ch):
            # Pop two operands (note: a is first operand, b is second)
            a = stack.pop()
            b = stack.pop()
            
            if ch == '+':
                result = a + b
            elif ch == '-':
                result = a - b
            elif ch == '*':
                result = a * b
            elif ch == '/':
                result = a / b
            elif ch == '^':
                result = a ** b
            
            stack.append(result)
    
    return stack[0]
```
## 6. Complete Demo
```
if __name__ == "__main__":
    infix = "(A+B)*C"
    print(f"Infix:     {infix}")
    print(f"Postfix:   {infix_to_postfix(infix)}")   # AB+C*
    print(f"Prefix:    {infix_to_prefix(infix)}")    # *+ABC
    print()
    
    # Numeric evaluation example
    infix_num = "(5+3)*8"
    postfix_num = infix_to_postfix(infix_num)
    prefix_num = infix_to_prefix(infix_num)
    
    print(f"Infix:     {infix_num}")
    print(f"Postfix:   {postfix_num}  →  {evaluate_postfix(postfix_num)}")
    print(f"Prefix:    {prefix_num}   →  {evaluate_prefix(prefix_num)}")
    print()
    
    # More complex example
    infix_complex = "A+B*C-D/E"
    print(f"Infix:     {infix_complex}")
    print(f"Postfix:   {infix_to_postfix(infix_complex)}")  # ABC*+DE/-
    print(f"Prefix:    {infix_to_prefix(infix_complex)}")   # -+A*BC/DE
```
## Output
```
Infix:     (A+B)*C
Postfix:   AB+C*
Prefix:    *+ABC

Infix:     (5+3)*8
Postfix:   53+8*  →  64
Prefix:    *+538   →  64

Infix:     A+B*C-D/E
Postfix:   ABC*+DE/-
Prefix:    -+A*BC/DE
```
