**Squashing commits means combining multiple commits into one single commit.**
So instead of this messy history:
```
feat: add login
fix typo
oops fix tests
another fix
final fix I swear
```
You end up with:
```
feat: add login
```
Same code. **Much cleaner history.**

---
## Why squash commits?

### 1. Clean, readable history 

Git history is not a diary — it’s a **story for future humans**.

Squashing removes:

- “fix typo”
    
- “debug”
    
- “WIP”
    
- “try again”
    

and keeps **intentional commits**.

---
### 2. Perfect before a PR (pull request)

Very common workflow:

- While coding → many small, messy commits
    
- Before merging → **squash into 1–3 meaningful commits**
    

Most teams _expect_ this.

---
## How squashing actually works

There is **no `git squash` command**.

Squash is done via **interactive rebase**.

---
## The classic squash workflow

Say you want to squash the last 4 commits:
```
git rebase -i HEAD~4
```
You’ll see something like:
```
pick a1b2c3 Add login form
pick d4e5f6 Fix typo
pick g7h8i9 Fix tests
pick j1k2l3 Update styles
```
Change it to:
```
pick a1b2c3 Add login form
squash d4e5f6 Fix typo
squash g7h8i9 Fix tests
squash j1k2l3 Update styles
```
(or shorter:)
```
pick a1b2c3 Add login form
s d4e5f6 Fix typo
s g7h8i9 Fix tests
s j1k2l3 Update styles
```
Save and close.

---
## What happens next?

Git will:

1. Combine all commits into one
    
2. Open an editor
    
3. Ask you to write **one final commit message**
    

You might write:
```
feat: add login form

- login UI
- validation
- tests
- styles
```
Boom. Clean history.

---
## Squash vs Fixup (pro move)

Instead of `squash`, you can use `fixup`:
```
pick a1b2c3 Add login form
fixup d4e5f6 Fix typo
fixup g7h8i9 Fix tests
```
Difference:

- `squash` → asks you to edit commit message
    
- `fixup` → **auto-discards** the extra messages
    

### Even better:
```
git commit --fixup <commit-hash>
git rebase -i --autosquash
```
🔥 This is _chef-level Git_.

---
## Squash vs Merge Squash

Two different things people confuse:

### 1. Interactive squash (what we talked about)

- Rewrites history
    
- Local
    
- Uses rebase
    

### 2. “Squash and merge” (GitHub/GitLab)

- Platform feature
    
- Squashes _at merge time_
    
- Your local history stays messy
    
- Repo history stays clean
    

Both are valid. Different use cases.

---
## Important rule (again, but crucial)

> **Never squash commits that are already shared with others**, unless everyone agrees.

Squash = history rewrite  
History rewrite + shared branch = pain 