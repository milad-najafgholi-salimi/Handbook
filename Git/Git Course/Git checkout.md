`git checkout` is a **Git command used to switch what you’re working on**—most commonly **branches**, but also **specific commits or files**.

---

> **`git checkout <file>` restores the file in your _working directory_ from the _index (staging area)_.**

---

## The 3 places a file can live in Git

Before the command makes sense, keep this model in mind:

`Commit (HEAD)  ←→  Staging Area (Index)  ←→  Working Directory`

- **HEAD**: last committed version
    
- **Index (staging area)**: what will go into the next commit
    
- **Working directory**: your actual files on disk
    

---

## What `git checkout <file>` REALLY does

`git checkout file.txt`

This means:

> “Replace `file.txt` in my **working directory** with the version from the **staging area (index)**.”

### Important consequences

- ✅ Working directory changes are discarded
    
- ❌ Staging area is **unchanged**
    
- ❌ Commit history is untouched
    

---

## Example: staged vs unstaged changes

### Step 1: Modify and stage a file
```
echo "v1" > file.txt
git add file.txt
```

Now:

- HEAD: old version
    
- Index: `v1`
    
- Working directory: `v1`
    

---

### Step 2: Modify again (but don’t stage)

`echo "v2" > file.txt`

Now:

- HEAD: old
    
- Index: `v1`
    
- Working directory: `v2`
    

---

### Step 3: Run checkout

`git checkout file.txt`

Result:

- Working directory → reset to `v1`
    
- Index → stays `v1`
    
- HEAD → unchanged
    

So **it “restores” the working directory _from_ the staging area**, not _to_ it.

---

## What if you want to restore the staging area?

This is where the confusion usually comes from.

### ❌ `git checkout` cannot restore _to_ the index

Instead, you want:

### Reset the staging area (but keep working directory)

`git reset file.txt`

This means:

> “Unstage this file, but keep my working changes.”

---

### Reset both index and working directory

`git reset --hard file.txt`

(or)

`git checkout HEAD -- file.txt`

This replaces:

- Index ← HEAD
    
- Working directory ← HEAD
    

⚠️ This **destroys all local changes**.

---

## Modern, clearer equivalents (recommended)

### Restore working directory from index

`git restore file.txt`

Same behavior as:

`git checkout -- file.txt`

---

### Restore working directory from HEAD

`git restore --source=HEAD file.txt`

---

### Restore staging area from HEAD (unstage)

`git restore --staged file.txt`

This is the clean, explicit replacement for:

`git reset file.txt`

---

## Summary table

|Goal|Command|
|---|---|
|Discard unstaged changes|`git checkout -- file`|
|Discard unstaged changes (modern)|`git restore file`|
|Unstage a file|`git reset file`|
|Unstage (modern)|`git restore --staged file`|
|Reset both index & working tree|`git reset --hard`|

---

## One-sentence rule to remember

> **`git checkout <file>` copies _from the index to the working directory_.  
> It never copies _into_ the index.**

---
## Extra
### 1. Switching branches (most common use)

This is what most people mean when they talk about `git checkout`.

`git checkout main`

What happens:

- Your **HEAD** moves to the `main` branch
    
- Your working directory updates to match the latest commit on `main`
    
- Any tracked files change to reflect that branch’s state
    

Create and switch to a new branch in one step:

`git checkout -b feature/login`

Equivalent to:
```
git branch feature/login
git checkout feature/login
```

---

## 2. Checking out a specific commit (detached HEAD)

You can also use `git checkout` to move to a specific commit **without being on a branch**:

`git checkout a1b2c3d`

This puts you in a **detached HEAD state**:

- You’re no longer on a branch
    
- You can inspect code, run tests, or debug
    
- New commits won’t belong to any branch unless you create one
    

If you decide to keep work done here:

`git checkout -b hotfix-from-old-commit`

---

## 3. Restoring files from another commit or branch

`git checkout` can replace files in your working directory with versions from elsewhere.

Restore a file from the last commit:

`git checkout -- config.yml`

Restore a file from another branch:

`git checkout develop -- src/app.js`

Important:

- This **overwrites the file** in your working directory
    
- The change is not committed automatically
    

---

## 4. Why `git checkout` is considered confusing

Historically, `git checkout` did **three different things**:

1. Switch branches
    
2. Move to a commit (detached HEAD)
    
3. Restore files
    

Because of this, Git introduced **clearer commands**.

---

## 5. Modern replacements (recommended)

### `git switch` → for branches
```
git switch main
git switch -c feature/login
```

Clear intent: _“I am switching branches.”_

---

### `git restore` → for files

```
git restore config.yml
git restore --source=develop src/app.js
```

Clear intent: _“I am restoring files.”_

---

### Summary mapping

|Old command|New command|
|---|---|
|`git checkout branch`|`git switch branch`|
|`git checkout -b new`|`git switch -c new`|
|`git checkout -- file`|`git restore file`|

> `git checkout` still works and is not deprecated, but many teams prefer the newer commands for clarity.

---
### Bonus
if you ran something like:
```
git checkout <commit-hash>
```
In this case, `HEAD` points to **one specific commit**, not a branch — so `git log HEAD` shows only history up to _that commit_.

Check:
```
git status
```
If you see:
```
HEAD detached at a3f1c2d
```
To see all commits in that repo history:
```
git switch <branch-name>
```

### Also:
You can go to another branch by using:
```
git checkout <branch>
```