`git log` is a Git command used to **view the history of commits** in a repository.

It shows information like:

- Commit ID (hash)
    
- Author
    
- Date
    
- Commit message
    

Common examples:

- `git log` → full commit history
    
- `git log --oneline` → compact, one-line summary
    
- `git log --graph` → visual branch history
    
- `git log -p` → shows code changes per commit
    
- `git log --reverse` -> full commit history but reverse
It helps you understand **what changed, when, and by whom**.

## Common and useful `git log` options

### 1. Compact summaries

`git log --oneline`

Shows each commit on a single line (short hash + message).  
Useful when you want a **quick overview** of history.

---

### 2. Visualizing branches

`git log --graph --oneline --all`

Adds an ASCII graph that shows **branching and merging**.  
This is extremely helpful for understanding complex workflows involving multiple branches.

---

### 3. Seeing actual code changes

`git log -p`

Displays the **diff (patch)** introduced by each commit.  
Great for code reviews or investigating when a specific line changed.

---

### 4. Limiting output

`git log -5`

Shows only the **last 5 commits**, keeping output manageable.

You can also limit by date:
```
git log --since="2024-01-01"
git log --until="2024-06-01"
```

---

### 5. Filtering commits

By author:

`git log --author="Alice"`

By commit message:

`git log --grep="fix"`

By file:

`git log -- path/to/file.txt`

This is especially useful to track the history of a **single file**.

---

### 6. Custom formatting

`git log --pretty=format:"%h - %an, %ar : %s"`

Lets you define exactly how commits are displayed (hash, author, relative time, message, etc.), which is useful for reports or scripts.