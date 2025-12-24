In Git, a **hunk** is a **contiguous block of changes** within a file that Git treats as a single unit when showing or staging diffs.

---

## Formal definition (plain English)

A **hunk** is:

> A group of added, removed, or modified lines that are close enough together in a file that Git shows them as one diff section.

Git doesn’t work line-by-line by default—it works **hunk-by-hunk**.

---

## What a hunk looks like

Here’s a diff showing **one hunk**:
```
@@ -10,7 +10,8 @@ function calculateTotal(items) {
     let total = 0;
-    for (let i = 0; i < items.length - 1; i++) {
+    for (let i = 0; i < items.length; i++) {
         total += items[i];
     }
+    return total;
 }
```

Everything between the `@@ ... @@` lines is **one hunk**.

---

## Breaking down the hunk header

`@@ -10,7 +10,8 @@ function calculateTotal(items) {`

This means:

- `-10,7` → old file: start at line 10, 7 lines affected
    
- `+10,8` → new file: start at line 10, 8 lines affected
    
- `function calculateTotal(items)` → nearby code for context
    

Git uses this information to:

- locate where the change applies
    
- show surrounding lines for readability
    

---

## Why Git groups lines into hunks

Git groups changes into hunks because:

1. **Changes close together are usually related**
    
2. Reviewing chunks is easier than reviewing whole files
    
3. Interactive tools (`git add -p`, `git reset -p`) need manageable units
    

So if you change lines 20–22 and 24–26, Git might show **one hunk**, not two.

---

## Hunks vs lines

|Level|What it is|
|---|---|
|File|Entire file|
|**Hunk**|Block of nearby changes|
|Line|Individual line|

By default:

- Git stages **hunks**
    
- Not individual lines
    
- (unless you manually edit a hunk)
    

---

## How hunks are formed (important intuition)

Git decides hunk boundaries based on:

- **Distance between changes**
    
- **Amount of unchanged context** (default ~3 lines)
    

Example:
```
change
(change)
(change)

<unchanged lines>

change
(change)
```

- Close changes → same hunk
    
- Far apart changes → separate hunks
    

You can influence this with:

`git diff -U10`

(more context → larger hunks)

---

## Why hunks matter in practice

### `git add -p`

- You’re asked: _“Stage this hunk?”_
    
- You’re deciding if **this group of changes belongs in the next commit**
    

### `git reset -p`

- You unstage **a hunk at a time**
    

### Code review

- Reviewers reason in hunks, not files
    

---

## Splitting hunks

When Git shows:

`Stage this hunk [y,n,q,a,d,s,e,?]?`

- `s` → split into smaller hunks
    
- `e` → manually edit lines inside the hunk
    

This is how you get **line-level control**.

---
## One sentence summary

A **hunk** is the smallest **default unit of change** that Git shows, stages, and asks you to reason about.