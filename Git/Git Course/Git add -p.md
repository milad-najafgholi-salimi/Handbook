`git add -p` is one of Git’s most powerful tools for **precise, intentional commits**. It lets you **interactively choose exactly which changes** go into the next commit—down to individual lines or even parts of lines.

---

## What `git add -p` does

`git add -p`

- `-p` stands for **patch**
    
- Git shows your uncommitted changes **one chunk (hunk) at a time**
    
- For each hunk, Git asks what you want to do with it
    

Instead of staging _entire files_, you stage **specific hunks**.

### See [[what is hunk]] here.

---

## Why this matters

Without `-p`:

`git add file.py`

You stage _everything_, even if:

- a bug fix
    
- a refactor
    
- and a formatting tweak  
    are all mixed together.
    

With `git add -p`, you can:

- commit the bug fix alone
    
- keep refactors separate
    
- leave experimental changes unstaged
    

This leads to:

- cleaner commit history
    
- easier reviews
    
- safer rollbacks
    

---

## Basic flow

1. Make changes to files
    
2. Run:
    
    `git add -p`
    
3. Git shows a diff and prompts you:
```
diff --git a/app.js b/app.js
@@ -12,7 +12,8 @@ function login() {
-  authenticate(user);
+  authenticate(user);
+  logLogin(user);
```

Prompt:

`Stage this hunk [y,n,q,a,d,s,e,?]?`

---

## The interactive options (important)

Here’s what each option means:

|Key|Meaning|
|---|---|
|`y`|Stage this hunk|
|`n`|Do not stage this hunk|
|`q`|Quit (keep decisions so far)|
|`a`|Stage this hunk **and all remaining hunks**|
|`d`|Do not stage this hunk **or any remaining hunks**|
|`s`|**Split** the hunk into smaller hunks|
|`e`|**Edit** the hunk manually|
|`?`|Show help|

The real power is in **`s` and `e`**.

---

## Splitting hunks (`s`)

`Stage this hunk [y,n,q,a,d,s,e,?]? s`

Git tries to break a large change into smaller hunks.

Example:

`- fix bug - refactor naming`

After splitting:

- you can stage only the bug fix
    
- and leave the refactor for another commit
    

⚠️ Git can only split along _unchanged lines_. If changes are tightly interwoven, you’ll need `e`.

---

## Editing hunks (`e`) – surgical precision

`Stage this hunk [y,n,q,a,d,s,e,?]? e`

This opens a text editor with something like:

`- console.log("debug"); + console.log("debug"); + validateInput();`

You manually edit:

- remove lines you don’t want staged
    
- keep only the exact lines you want
    

Rules:

- Lines starting with `+` are staged
    
- Lines removed or turned into context won’t be staged
    
- **Do not change context lines**
    

This is the ultimate “commit surgeon” mode.

---

## Common variants and related commands

### Add a specific file interactively

`git add -p src/main.py`

---

### Interactive mode (menu-driven)

`git add -i`

This includes patch mode but also lets you:

- choose files
    
- review staged content
    
- unstage hunks
    

---

### Unstage with patch mode

`git reset -p`

Same interface, but in reverse:

- remove hunks from the staging area
    

---

### Modern equivalent (recommended)

`git add --patch`

Same behavior, clearer spelling.

---

## Typical real-world workflow

1. You work for an hour
    
2. Changes are messy
    
3. Instead of panicking:
    
    `git add -p`
    
4. Stage only:
    
    - one logical change
        
5. Commit
    
6. Repeat for next logical change
    

Result:  
**One idea per commit**, even if you coded many ideas at once.

---

## When _not_ to use `git add -p`

- You changed **one file for one reason**
    
- You’re committing generated files
    
- You’re doing a quick spike or throwaway branch
    

In those cases, full-file staging is fine.