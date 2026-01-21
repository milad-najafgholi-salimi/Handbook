## What is `git clone`?

`git clone` creates a **local copy of a remote Git repository**.

But under the hood, it does more than that:

When you run:
```
git clone <repo-url>
```
Git:

1. Downloads **all commits, branches, and tags**
    
2. Sets up a **remote called `origin`**
    
3. Checks out the **default branch** (`main` or `master`)
    
4. Creates a working directory ready to use
    

So it’s not just files — it’s the **entire project history**.

---
## Basic usage
```
git clone https://github.com/user/project.git
```
This creates:
```
project/
├── .git/
├── src/
├── README.md
```
The folder name defaults to the repo name.

---
## Cloning into a specific directory
- Use `git clone <repo-url> <path>`:
```
git clone https://github.com/user/project.git my-folder
```
Now the repo lives in `my-folder/`.

---
## HTTPS vs SSH cloning

### HTTPS
```
git clone https://github.com/user/project.git
```
- Easier setup
    
- Prompts for credentials (or token)
    
- Good for beginners
    

---

### SSH
```
git clone git@github.com:user/project.git
```
- Uses SSH keys
    
- No password prompts
    
- Preferred by most devs once set up
    

If you clone via HTTPS and later want SSH, you can change it:
```
git remote set-url origin git@github.com:user/project.git
```

---
## What gets cloned?

By default:

- ✅ All branches
    
- ✅ All tags
    
- ✅ Full commit history
    
- ❌ No working branches except the default
    

Remote branches are visible as:
```
origin/main
origin/dev
```

---
## Shallow clones (faster, less history)

If you only need recent commits:
```
git clone --depth 1 https://github.com/user/project.git
```
- Downloads only the latest commit
    
- Faster
    
- Less disk space
    
- Some Git commands won’t work fully (e.g. full history)
    

You can deepen it later:
```
git fetch --unshallow
```

---
## Cloning a specific branch
- Use `git clone -b <branch-name> <repo-url>`:
```
git clone -b dev https://github.com/user/project.git
```
This:

- Checks out `dev`
    
- Still downloads all branches (unless combined with `--single-branch`)

---
### Clone only one branch
- Use 
`git clone -b <branch-name> --single-branch <repo-url>`:
```
git clone -b dev --single-branch https://github.com/user/project.git
```
Useful for very large repos.

---
## Bare clone (advanced)
```
git clone --bare https://github.com/user/project.git
```
- No working directory
    
- Only Git data
    
- Used for mirrors or servers
    

You’ll see something like:
```
project.git/
```

---
## What is `origin`?

After cloning:
```
git remote -v
```
You’ll see:
```
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```
`origin` is just a **default name**, not special — but widely used.

---
## Clone vs fork (important distinction)

- **Clone** → local copy
    
- **Fork** → server-side copy (GitHub/GitLab feature)
    

Typical flow:
```
fork → clone → work → push → pull request
```
