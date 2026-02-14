**venv** is Python's built-in module for creating lightweight, isolated Python environments. It's the recommended way to manage project-specific dependencies.

---
### What is a Virtual Environment?

A virtual environment is a self-contained directory that contains:

- A specific Python interpreter
    
- Its own pip
    
- Its own installed packages
    
- Project-specific dependencies isolated from other projects
    

### Key Benefits

- Avoid version conflicts between projects
    
- No need for system-wide package installation
    
- Reproducible environments
    
- Can use different Python versions per project
    

---

## Creating and Using venv

### **Windows**

#### Creating an environment
```
# Navigate to your project folder
cd C:\Users\YourName\myproject

# Create virtual environment (common names: venv, .venv, env)
python -m venv venv
# or
py -m venv venv
```
**Note:** You can name your venv whatever you want instead of `venv`; Which means: `python -m venv test`.
**Note:** `.` before directory name, will hide it. Like: `.test`
#### Activating the environment
```
# Command Prompt
venv\Scripts\activate

# PowerShell
venv\Scripts\Activate.ps1

# Git Bash
source venv/Scripts/activate
```
#### Deactivating
```
deactivate
```

---
### **Linux/macOS**

#### Creating an environment
```
# Navigate to your project folder
cd ~/myproject

# Create virtual environment
python3 -m venv venv
# or
python -m venv venv
```
**Note:** You can name your venv whatever you want instead of `venv`; Which means: `python -m venv test`.
**Note:** `.` before directory name, will hide it. Like: `.test`
#### Activating the environment
```
source venv/bin/activate
```
#### Deactivating
```
deactivate
```

---
## Common Workflow
```
# 1. Create project directory and enter it
mkdir myproject
cd myproject

# 2. Create virtual environment
python -m venv .venv

# 3. Activate it
# Windows: .venv\Scripts\activate
# Linux/Mac: source .venv/bin/activate

# 4. Your prompt changes (shows environment name)
(.venv) $

# 5. Install packages (they go into .venv)
pip install requests flask

# 6. Save dependencies
pip freeze > requirements.txt

# 7. Later, someone can recreate environment
pip install -r requirements.txt

# 8. When done, deactivate
deactivate
```

---
## Best Practices

### Naming Conventions
```
# Common names (all indicate it's a venv and should be gitignored)
python -m venv venv
python -m venv .venv
python -m venv env
```
### .gitignore

Always add to `.gitignore`:
```
venv/
.venv/
env/
ENV/
__pycache__/
*.pyc
```
### requirements.txt Management
```
# Create/update requirements
pip freeze > requirements.txt

# Install from requirements
pip install -r requirements.txt

# Install in development mode (editable)
pip install -e .
```

---
## Common Commands Reference
|Action|Windows|Linux/macOS|
|---|---|---|
|Create|`python -m venv venv`|`python3 -m venv venv`|
|Activate|`venv\Scripts\activate`|`source venv/bin/activate`|
|Deactivate|`deactivate`|`deactivate`|
|Delete|`rmdir /s venv`|`rm -rf venv`|
|Check Python|`where python`|`which python`|
|List packages|`pip list`|`pip list`|

---

## Troubleshooting

### **Common Issues**

1. **"venv is not installed"** (Linux)
```
sudo apt install python3-venv
```
2. **PowerShell execution policy** (Windows)
```
Set-ExecutionPolicy Unrestricted -Scope Process
```
3. **"pip not found"**
    
    - Ensure you're in activated environment
        
    - Upgrade pip: `python -m pip install --upgrade pip`
        
4. **Different Python version**
```
# Specify Python version when creating
py -3.9 -m venv venv  # Windows
python3.9 -m venv venv  # Linux/Mac
```
