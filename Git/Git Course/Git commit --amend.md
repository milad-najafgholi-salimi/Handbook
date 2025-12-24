`git commit --amend` is a Git command used to **modify the most recent commit**. It’s commonly used to fix small mistakes—like forgetting to add a file, correcting a commit message, or adjusting content—_without creating a new commit_.

---
## What `git commit --amend` Does

When you run:

`git commit --amend`

Git **replaces your last commit** with a new one that includes:

- The previous commit’s changes
    
- Plus any **new staged changes**
    
- Optionally, a **new commit message**
    

The commit history still shows **one commit**, but its **hash changes**.

---

## Common Use Cases

### 1. Fixing the Last Commit Message

If you made a typo or want to reword it:

`git commit --amend`

Your editor opens so you can edit the message.

To skip the editor and reuse the same message:

`git commit --amend --no-edit`

---

### 2. Adding Forgotten Files to the Last Commit

If you forgot to include a file:
```
git add missing_file.txt
git commit --amend
```

Now the file is part of the previous commit instead of creating a new one.

---

### 3. Modifying Previously Committed Code

You can edit files, stage them again, and amend:
```
# make changes
git add .
git commit --amend
```

This replaces the old commit with an updated version.

---

## Important Warning: Rewriting History

⚠️ **Do NOT amend commits that have already been pushed to a shared branch** (like `main` or `develop`) unless you _know exactly what you're doing_.

Why?

- `--amend` changes the commit hash
    
- This causes conflicts for others who pulled the old version
    
- Requires force-pushing (`git push --force`), which can overwrite others’ work
    

**Safe rule:**

> Only amend commits that exist **locally** and haven’t been shared.

---

## How It Differs From Making a New Commit

|Action|Result|
|---|---|
|`git commit`|Creates a new commit|
|`git commit --amend`|Rewrites the previous commit|
|`git rebase -i`|Edits multiple past commits|

---
## When NOT to Use `--amend`

- When the commit is already pushed and shared
    
- When you want a clear historical record of changes
    
- When modifying older (not most recent) commits → use `git rebase -i`