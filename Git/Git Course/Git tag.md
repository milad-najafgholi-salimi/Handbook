A **Git tag** is a **named pointer to a specific commit**.  
Think of it like a permanent bookmark in your project’s history.

Typical use cases:

- Marking **release versions** (e.g. `v1.0.0`, `v2.1.3`)
    
- Capturing a **stable milestone**
    
- Making it easy to check out an exact point in time later
    

Unlike branches, **tags do not move**. Once created, they always point to the same commit.

---

## Types of Git tags

There are **two kinds** of tags, and this distinction matters.

### 1. Lightweight tags

- Just a name → commit reference
    
- No extra metadata
    

Create one - `git tag <tag-name>`:
```
git tag v1.0.0
```
Good for:

- Quick, local markers
    
- Temporary or personal tags
### 2. Annotated tags (recommended for releases)

- Stored as full Git objects
    
- Include:
    
    - Tagger name & email
        
    - Date
        
    - Message
        
    - Optional GPG signature
        

Create one - `git tag -a <tag-name> -m "message"`:
```
git tag -a v1.0.0 -m "Initial stable release"
```
Good for:

- Official releases
    
- Anything you might share with others
    

**Most teams use annotated tags for versioning**

---
## Listing tags
```
git tag
```
Filter by pattern:
```
git tag -l "v1.*"
```

---
## Viewing tag details
For annotated tags:
```
git show v1.0.0
```
You’ll see:

- Tag metadata
    
- The commit it points to
    
- Commit message & diff

---
## Tagging a specific commit
By default, tags point to `HEAD`, but you can tag any commit - 
`git tag -a <tag-name> <commit-hash> -m "message"`:
```
git tag -a v1.0.1 abc1234 -m "Bugfix release"
```

---
## Checking out a tag
```
git checkout v1.0.0
```
⚠️ This puts you in **detached HEAD** state  
(you can look around, but don’t commit unless you create a branch)

---
## Pushing tags to a remote

Important gotcha: **tags are NOT pushed automatically**.

Push a single tag - `git push <remote-name> <tag-name>`:
```
git push origin v1.0.0
```
Push all tags - `git push <remote-name> --tags`:
```
git push origin --tags
```

---
## Deleting tags

### Delete locally:
- Use `git tag -d <tag-name>`
```
git tag -d v1.0.0
```
- Delete from remote -
`git push <remote-name> --delete <tag-name>`:
```
git push origin --delete v1.0.0
```

---
## Semantic versioning (very common with tags)

You’ll often see tags like:
```
v1.2.3
```
Meaning:

- **1** → major (breaking changes)
    
- **2** → minor (new features)
    
- **3** → patch (bug fixes)
    

Git doesn’t enforce this — it’s just convention, but a powerful one.