**Rebase = move your commits to a new base commit.**

Imagine your branch is a stack of commits sitting on top of some older commit.  
`git rebase` **picks up your commits, one by one, and replays them on top of another branch**.

So instead of:

> “My work branched off _there_”

it becomes:

> “My work branched off _here_”

## Why people use rebase

### 1. Cleaner history 

Rebase avoids messy “merge commits” and gives you a **straight, linear history**.

Compare:

**With merge**
```
main ──●────●────●
         \        \
feature   ●──●──●─●
```
**With rebase**
```
main ──●────●────●────●────●────●
                 feature commits
```
Same code, **much nicer story**.
### 2. Keep your branch up to date

If `main` changed while you were working:
```
git checkout feature
git rebase main
```
Now your commits sit _on top of the latest main_, as if you started today.
## Basic rebase workflow

### Scenario

- You branched off `main`
    
- You made 3 commits on `feature`
    
- `main` got new commits
    
- You want your work on top of the latest `main`
### Commands
```
git checkout feature
git fetch origin
git rebase origin/main
```
Git will:

1. Temporarily remove your commits
    
2. Fast-forward `feature` to `main`
    
3. Replay your commits one by one
---
## What happens if there’s a conflict?

Git pauses and says:

> “Hey, I don’t know how to apply this commit.”

You then:
```
# fix the conflicts in files
git add <fixed-files>
git rebase --continue
```
If things go sideways:
```
git rebase --abort
```
Boom—back to where you started.

---
## Rebase vs Merge (quick comparison)
| Rebase                  | Merge                       |
| ----------------------- | --------------------------- |
| Linear history          | Preserves branching history |
| Rewrites commit history | Does NOT rewrite history    |
| Cleaner logs            | More explicit record        |
| Dangerous if misused    | Safer for shared branches   |

---
## The Golden Rule of Rebase

> **Never rebase commits that you’ve already pushed and other people are using.**

Why?

- Rebase **rewrites commit hashes**
    
- Your teammates’ history explodes
    

**Safe to rebase:**

- Local branches
    
- Personal feature branches
    

**Do NOT rebase:**

- `main`
    
- `develop`
    
- Shared branches
