`git log -p` is a way to **read commit history _together with the exact code changes_** that each commit introduced. It’s especially useful when you want to understand _why_ something changed, not just _when_ or _by whom_.

---
## What `git log -p` does

- `git log` shows the commit history.
    
- The `-p` flag stands for **patch**.
    

So:

`git log -p`

means:

> “Show me each commit **and the diff (patch)** that commit applied.”

Instead of just seeing commit messages, you see the **line-by-line code changes** for every commit, in reverse chronological order.

---

## What the output looks like

A typical section looks like this:
```
commit 3a1f2c9e9d7f...
Author: Alex Smith <alex@example.com>
Date:   Mon Dec 18 14:32:01 2025

    Fix off-by-one error in loop

diff --git a/calc.py b/calc.py
index 4e3d2c1..a9b8f72 100644
--- a/calc.py
+++ b/calc.py
@@ -10,7 +10,7 @@ def sum_numbers(nums):
     total = 0
-    for i in range(len(nums) - 1):
+    for i in range(len(nums)):
         total += nums[i]
     return total
```

### How to read this

#### Commit metadata

- **commit**: SHA hash (unique ID)
    
- **Author / Date**: Who made the change and when
    
- **Message**: Why the change was made (ideally)
    

#### Diff section

- `---` → old version of the file
    
- `+++` → new version
    
- Lines starting with:
    
    - `-` → removed
        
    - `+` → added
        
    - no symbol → unchanged context
        

This lets you reconstruct _exactly_ what the commit did.

---

## Why `git log -p` is useful

### 1. Understanding history deeply

Instead of guessing from commit messages, you see:

- what logic changed
    
- what lines were added or removed
    
- how a bug was fixed
    

### 2. Debugging regressions

If something broke:

`git log -p path/to/file`

You can scroll through changes and find **the commit that introduced the bug**.

### 3. Code reviews after the fact

It’s like replaying a pull request:

- commit message explains intent
    
- patch shows implementation
    

---

## Common and powerful variations

### Limit number of commits

`git log -p -2`

Show only the last 2 commits (with patches).

---

### Focus on a specific file

`git log -p src/main.js`

Extremely useful for answering:

> “How did this file evolve over time?”

---

### Show function-level context (recommended)

`git log -p -U10`

- `-U10` shows 10 lines of context around changes
    
- Makes diffs much easier to understand
    

---

### Combine with `--stat`

`git log -p --stat`

You get:

- a summary of files changed
    
- followed by full diffs
    

---

### Search for a specific change

`git log -p -S "myVariable"`

Shows commits where the _number of occurrences_ of `myVariable` changed.  
This is incredibly powerful for archaeology.

---

## Paging and navigation tips

`git log -p` uses a pager (usually `less`).

Inside it:

- `Space` → next page
    
- `b` → back
    
- `/text` → search forward
    
- `q` → quit
    

If output feels overwhelming:

`git log -p | less`

(or configure pager options globally)

---

## When _not_ to use `git log -p`

- **Very large repositories** → output can be massive
    
- **Binary files** → diffs are useless
    
- **High-level overview needed** → use `git log --oneline --graph`
    

In those cases, `-p` is too much detail.