`git fetch` **downloads new data from a remote repository**—such as:

- new commits
    
- new branches
    
- updated tags
    

…but **it does not change your working directory or your current branch**.

Think of it as:

> “Show me what’s changed on the remote, but don’t apply it yet.”

Use:
```
git fetch
```
And if you want to update your local repository like your remote repository, after fetching use this:
```
git pull
```
Also when you didn't know what to do just send `git status` command. This command will tell you what you need to do.