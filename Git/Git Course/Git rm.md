`git rm` is the command for **removing a file from Git’s tracking**, with control over whether the file is also deleted from your working directory and how that removal is staged.

---

## What `git rm` does

At its core:

`git rm file.txt`

means:

> “Remove this file from the repository **and** from my working directory, and stage that removal.”

After running it:

- the file is deleted from disk
    
- the deletion is already staged
    
- the next commit will remove the file from the repo
    

---

## The three states involved (important)

Git tracks files in three places:

1. **Working tree** (files on disk)
    
2. **Index / staging area**
    
3. **Repository (last commit)**
    

`git rm` updates **both** the working tree _and_ the index in one command.

---

## Common usage patterns

### Remove a file completely
```
git rm notes.txt
git commit -m "Remove obsolete notes"
```
---

### Remove a file but keep it on disk

`git rm --cached config.json`

This:

- stops tracking the file
    
- leaves it in your working directory
    
- is often used for:
    
    - secrets
        
    - generated files
        
    - local-only configs
        

⚠️ Usually paired with `.gitignore`.

---

### Remove a directory

`git rm -r old_logs/`

`-r` is required for directories.

---

## `git rm` vs deleting files manually

### Manual delete
```
rm file.txt
git status
git add file.txt
```

### With `git rm`

`git rm file.txt`

Both end up the same, but:

- `git rm` is faster
    
- less error-prone
    
- immediately stages the deletion
    

---

## Safety checks (why Git sometimes refuses)

Git will stop you if removal would lose work:

`error: the following file has local modifications:`

Why?

- You modified the file
    
- The changes aren’t staged or committed
    
- Deleting would lose them
    

### Override (be careful)

`git rm -f file.txt`

---

## Interaction with commits and history

Important principle:

> **Git never deletes history.**

- Old commits still contain the file
    
- `git rm` only removes it from future commits
    

You can still recover it:

`git checkout <old-commit> -- file.txt`

---

## `git rm` and renames

If you do:
```
git rm old.txt
git add new.txt
```

Git may later detect this as a **rename** if content is similar.

But this is why `git mv` exists—it combines these steps safely.

---

## Common real-world scenarios

### Remove a tracked file that should be ignored
```
git rm --cached .env
echo ".env" >> .gitignore
git commit -m "Stop tracking .env"
```

---

### Clean up generated files

`git rm -r dist/`

Then add `dist/` to `.gitignore`.

---

## Undoing `git rm`

### Before commit

`git restore --staged file.txt git restore file.txt`

### After commit

`git revert <commit>`

---
## One-line summary

`git rm` removes a file from Git tracking, stages the deletion, and optionally deletes it from your working tree.