## What `git pull` is (in one sentence)

**`git pull` updates your local branch with changes from a remote repository.**

---
## What actually happens when you run `git pull`

This is the key idea most people miss:

> **`git pull` = `git fetch` + `git merge`**  
> (or sometimes `git fetch` + `git rebase`)

So when you run:
```
git pull
```
Git does **two things**:

### 1) `git fetch`

- Downloads new commits from the remote
    
- Does **not** change your code yet
    

### 2) `git merge` (default behavior)

- Merges those remote commits into your current branch
    
- Your files may change
    
- Conflicts may happen here

---
## The most common form
```
git pull origin main
```
Means:

- Pull from the remote named `origin`
    
- From the branch `main`
    
- Merge it into your current local branch
    

If your branch has an upstream set, you can just do:
```
git pull
```

---
## Why conflicts happen during `git pull`

Conflicts occur when:

- You changed a file locally
    
- Someone else changed the **same part** of the file remotely
    
- Git can’t safely decide which version to keep
    

When this happens:

1. Git stops
    
2. Marks the conflict in the file
    
3. Asks **you** to resolve it manually
    
4. You then commit the fix
    

This is totally normal—especially in team projects.

---
## Using rebase instead of merge

Some teams prefer this:
```
git pull --rebase
```
What this does:

- Downloads remote commits
    
- Replays your local commits **on top of them**
    
- Keeps history cleaner (no extra merge commits)
    

Visual difference:

- **Merge** → branchy history
    
- **Rebase** → straight line

⚠️ Important rule:

> Never rebase commits that you’ve already pushed and others are using.