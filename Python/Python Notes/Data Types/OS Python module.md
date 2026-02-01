The **`os` module** in Python is one of the most **fundamental built-in modules** for interacting with the operating system. It lets you **work with files, directories, paths, and environment variables**, and is essential for scripts that need to interact with the system rather than just Python objects.

---
## What is the `os` module?

- The `os` module provides **a way to interact with the operating system**.
    
- You can do things like:
    
    - Create, rename, delete directories and files
        
    - Check if files or directories exist
        
    - Get information about the system
        
    - Work with environment variables
        
    - Navigate paths and directories

---
## Importing the `os` module
```
import os
```
Everything in the `os` module is accessed via `os.`

---
## Working with the current working directory

### a. Get current directory
```
cwd = os.getcwd()
print(cwd)   # Prints the path of the current working directory
```
### b. Change directory
```
os.chdir('/path/to/directory')
print(os.getcwd())  # Now prints the new directory
```

---
## Listing files and directories
```
files = os.listdir('.')   # List all files and folders in the current directory
print(files)
```
You can replace `'.'` with any path to list files there.

---
## 5. Creating and deleting directories

### a. Create a new directory
```
os.mkdir('new_folder')       # Creates a single directory
os.makedirs('folder/sub')    # Creates nested directories if needed
```
### b. Remove directories
```
os.rmdir('new_folder')       # Removes an empty directory
os.removedirs('folder/sub')  # Removes nested empty directories
```
⚠️ Directories must be empty to remove them with `rmdir()` or `removedirs()`.

---
## 6. Working with files

### a. Check if a file exists
```
print(os.path.exists('example.txt'))   # True or False
```
### b. Check if a path is a file or directory
```
print(os.path.isfile('example.txt'))   # True if file
print(os.path.isdir('folder'))         # True if directory
```
### c. Rename or remove a file
```
os.rename('old.txt', 'new.txt')  # Rename file
os.remove('new.txt')             # Delete file
```

---
## Path operations (`os.path`)

The `os.path` submodule helps you **work with file and directory paths safely**, independent of the operating system.

### a. Join paths
```
path = os.path.join('folder', 'file.txt')
print(path)   # folder/file.txt (or folder\file.txt on Windows)
```
### b. Get the directory name or base name
```
path = 'folder/file.txt'
print(os.path.dirname(path))  # folder
print(os.path.basename(path)) # file.txt
```
### c. Split a path
```
dir_name, file_name = os.path.split('folder/file.txt')
print(dir_name, file_name)    # folder file.txt
```
### d. Absolute path
```
print(os.path.abspath('example.txt'))  # Full path to the file
```

---
## Environment variables
```
print(os.environ['HOME'])  # Access environment variable (Linux/Mac)
print(os.environ.get('USERNAME'))  # Windows
```
You can also set environment variables temporarily:
```
os.environ['MY_VAR'] = '123'
```

---
## 9. Executing system commands

You can run system commands directly using:
```
os.system('ls')   # On Linux/Mac
os.system('dir')  # On Windows
```
Note: For more advanced command execution, Python’s `subprocess` module is recommended.

---
## Useful `os` functions summary
|Function|Description|
|---|---|
|`os.getcwd()`|Get current working directory|
|`os.chdir(path)`|Change current directory|
|`os.listdir(path)`|List files and directories|
|`os.mkdir(path)`|Create a directory|
|`os.makedirs(path)`|Create nested directories|
|`os.rmdir(path)`|Remove empty directory|
|`os.remove(path)`|Delete a file|
|`os.rename(src, dst)`|Rename a file or directory|
|`os.path.exists(path)`|Check if path exists|
|`os.path.isfile(path)`|Check if path is a file|
|`os.path.isdir(path)`|Check if path is a directory|
|`os.path.join(a, b, ...)`|Join paths|
|`os.path.abspath(path)`|Get absolute path|
|`os.environ`|Access environment variables|

---
## One-line exam definition

> **The `os` module in Python provides functions to interact with the operating system, including file and directory operations, path manipulations, environment variables, and system commands.**

---
## Common mistakes students make

- Confusing **file paths** on Windows (`\`) vs Linux/Mac (`/`). Use `os.path.join()` to avoid errors.
    
- Forgetting to check if a file or directory exists before removing it.
    
- Forgetting to `import os` before using it.
    
- Trying to remove non-empty directories with `os.rmdir()` instead of `shutil.rmtree()`.