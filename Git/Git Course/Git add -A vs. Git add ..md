|Command|What it stages|
|---|---|
|`git add -A`|**All changes everywhere** (new, modified, deleted files across the whole repo)|
|`git add .`|New + modified files **in the current directory and below** (deletions are the tricky part)|

---

## The real differences (there are two)

### 1. **Deletions**

This is the biggest historical gotcha.

### `git add -A`

✔️ Stages **file deletions**

Example:
```
rm old.txt
git add -A
```

→ `old.txt` will be removed in the next commit.

---

### `git add .`

- **Older Git versions (< 2.0)**: ❌ does **not** stage deletions
    
- **Newer Git versions**: ✅ usually _does_ stage deletions
    

Because of this inconsistency, many teams prefer `git add -A` for safety and clarity.

---

### 2. **Scope (where it applies)**

### `git add -A`

- Applies to the **entire repository**
    
- Ignores your current directory
    

No matter where you are:
```
cd subdir/
git add -A
```

→ stages everything, even changes outside `subdir`.

---

### `git add .`

- Applies **only to the current directory and its subdirectories**
    

Example:
```
cd src/
git add .
```

→ stages changes in `src/` only  
→ changes in `tests/` or root files are ignored

This can be intentional or accidental.

---

## Recommended rule of thumb

- ✅ Use **`git add -A`** when:
    
    - You want a complete snapshot
        
    - You’re finishing a task
        
    - You don’t want surprises
        
- ✅ Use **`git add .`** when:
    
    - You intentionally want to commit **only a subdirectory**
        
    - You know exactly what’s in scope
        

---

## Best practice (what many experienced devs do)
```
git add -A
git status
```

Always inspect before committing.

---

## One-liner to remember

> **`git add -A` = everything, everywhere**  
> **`git add .` = here and below**