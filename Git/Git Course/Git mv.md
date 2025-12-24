`git mv` is Git’s **rename-and-move command**. It moves (or renames) a file **and stages the change in one step**, while preserving history _as much as Git can_.

---

## What `git mv` does

`git mv old_path new_path`

This is equivalent to running **three commands**:
```
mv old_path new_path
git rm old_path
git add new_path
```

But:

- it’s atomic (one operation)
    
- it’s safer
    
- it immediately stages the result
    

---

## Basic examples

### Rename a file

`git mv app.js main.js`

### Move a file into a directory

`git mv utils.js src/utils.js`

### Move and rename

`git mv index.html public/home.html`

After any of these:

`git status`

will show the rename already staged.

---

## Does Git _really_ track renames?

Important concept:

> **Git does not store renames explicitly.**

Git stores:

- file contents (blobs)
    
- commit snapshots
    

Renames are **detected heuristically** later by comparing content similarity.

### So what does `git mv` actually help with?

- Ensures the delete + add happen together
    
- Makes rename detection **more reliable**
    
- Keeps your index (staging area) consistent
    

---

## History and blame

Even if you use plain `mv` instead of `git mv`:
```
mv file.py new_file.py
git add -A
```

Git can still detect the rename **if content similarity is high**.

But tools work better with `git mv`:

### Follow history across a rename

`git log --follow new_file.py`

### Blame across renames

`git blame --follow new_file.py`

---
## Overwriting targets

`git mv -f old.js new.js`

- `-f` = force
    
- overwrites `new.js` if it exists
    

Use carefully.

---

## Undoing a `git mv`

Before commit:
```
git restore --staged new_path
git restore new_path
```

Or:

`git reset HEAD old_path new_path`

After commit:

`git revert <commit>`

---

## `git mv` vs `git add -p`

Important interaction:

- `git mv` stages the rename
    
- content changes inside the file still appear as hunks
    
- you can still refine them with:
    

`git add -p`

---
## One-line summary

`git mv` moves or renames a file **and stages the change cleanly**, helping Git and humans understand that it’s a rename, not a delete-and-recreate.