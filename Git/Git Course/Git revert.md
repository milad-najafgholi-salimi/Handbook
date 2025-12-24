`git revert` is a **safe way to undo a commit** in Git **without rewriting history**.

Instead of deleting or changing old commits, it **creates a new commit** that reverses the changes made by a previous one.

---

## Key Idea (Very Important)

- **`git revert` does NOT remove history**
    
- **It adds a new commit that undoes another commit**
    
- This makes it **safe for shared branches** (like `main` or `develop`)
    

This is why teams prefer `git revert` over `git reset` when working collaboratively.

---

## Basic Example

Imagine this commit history:

`A — B — C — D`

If commit **C** introduced a bug and you run:

`git revert C`

Git creates a new commit:

`A — B — C — D — E`

Where **E** = “undo everything that C did”.

👉 The original commit **C still exists**, but its effects are canceled.

---

## Reverting a Specific Commit

You don’t need to be on that commit.

`git revert <commit-hash>`

Example:

`git revert a1b2c3d`

This safely undoes just that commit.

---

## What If You Want to Revert Multiple Commits?

### Option 1: Revert a range (newer → older)

`git revert HEAD~3..HEAD`

This reverts the last **3 commits**, one by one.

### Option 2: Revert without auto-committing

Useful if you want to edit or squash the result.

`git revert -n <commit-hash>`

(`-n` means _no commit yet_)

---

#### Common Confusion: `git revert` vs `git reset`

|Command|Rewrites History?|Safe for Shared Branches?|Use Case|
|---|---|---|---|
|`git revert`|❌ No|✅ Yes|Undo a commit publicly|
|`git reset`|✅ Yes|❌ No|Local cleanup, rewrite history|

If others may have pulled your code → **use `git revert`**.

---
## Bonus: Reverting a Merge Commit

Merge commits need a special flag:

`git revert -m 1 <merge-commit-hash>`

`-m 1` tells Git which parent branch to keep.