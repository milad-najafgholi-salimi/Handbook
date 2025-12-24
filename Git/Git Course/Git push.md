## What `git push` is (big picture)

`git push` is the Git command that **sends your local commits to a remote repository** (like GitHub, GitLab, or Bitbucket).

Think of Git like this:

- **Local repo** → your laptop (private workspace)
    
- **Remote repo** → shared server (where others can see your work)
    

You can make commits locally all day long, but **nothing leaves your machine until you push**.

---

## What happens when you run `git push`

When you type:
```
git push
```
Git does a few things behind the scenes:

1. Looks at your current branch (e.g. `main`, `dev`, `feature-x`)
    
2. Finds the remote it’s tracking (usually `origin`)
    
3. Sends all commits that the remote doesn’t have yet
    
4. Updates the remote branch to match yours
    

After that, your code is:

- Visible on GitHub
    
- Pullable by teammates
    
- Ready for CI, deployment, PRs, etc.
    

---

## The most common form
```
git push origin main
```
This means:

- **`origin`** → the remote repo name (default)
    
- **`main`** → the branch you’re pushing
    

You’re saying:  
_“Push my local `main` branch to the `main` branch on `origin`.”_

---

## First push of a new branch (important!)

If you just created a branch locally:
```
git checkout -b feature-login
```
Your first push needs this:
```
git push -u origin feature-login
```
Why `-u`?

- It sets an **upstream branch**
    
- After this, you can just run `git push` without extra arguments

---
### ❗ “no upstream branch”

Git doesn’t know where to push yet.

Fix:

`git push -u origin your-branch-name`

---

### ❗ Permission denied

Either:

- You don’t have access to the repo
    
- SSH keys / credentials aren’t set up correctly