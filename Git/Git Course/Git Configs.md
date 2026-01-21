A **Git config** is a set of settings that control Git’s behavior  
(e.g. username, email, editor, diff tool).

---

## Config Levels (Priority Order)

1. **System** – applies to all users
    
    - File: `/etc/gitconfig`
        
2. **Global** – applies to one user
    
    - File: `~/.gitconfig` or `~/.config/git/config`
        
3. **Local** – applies to one repository
    
    - File: `.git/config`
        

**Local overrides Global, Global overrides System**

---

## View Configs

### Show all configs

`git config --list`

### Show global configs

`git config --global --list`

### Show local configs (inside repo)

`git config --local --list`

### Show config source

`git config --list --show-origin`

---

## Common Git Configs

### User identity
```
git config --global user.name "Your Name"
git config --global user.email "you@email.com"
```
### Default editor

`git config --global core.editor "vim"`

### Default branch name

`git config --global init.defaultBranch main`

### Line ending handling
```
git config --global core.autocrlf input   # Linux/macOS
git config --global core.autocrlf true    # Windows
```

---

## Edit Config Files Directly

### Edit global config

`git config --global --edit`
or 
`git config --global -e`

### Edit local repo config

`git config --local --edit`
or
`git config --local -e`

---

## Remove a config

`git config --global --unset user.name`

---

## Check a single value

`git config user.name`

---
## List All your Configs
`git config -l`

## Key Points to Remember

- Configs control **behavior**, not code
    
- Git chooses config by **scope priority**
    
- Always set `user.name` and `user.email`
    
- Use `--show-origin` to debug config issues
    