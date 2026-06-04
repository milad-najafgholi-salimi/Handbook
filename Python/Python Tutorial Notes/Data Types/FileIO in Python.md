In Python, **file I/O** (input/output) is essential for working with files — whether it's reading from a file, writing to a file, or manipulating files on the system. Python provides a built-in set of functions and methods for dealing with file operations, and it’s incredibly **simple and intuitive** to use.

---
## Opening a File (`open()`)

The **`open()`** function is the most important function when working with files. It allows you to open a file in a specific mode (read, write, etc.).

### Syntax:
```
file = open('filename', 'mode')
```
- filename: Path to the file (can be absolute or relative)
- mode: The mode in which the file is opened (read, write, append, etc.)

#### Modes:

| Mode   | Description                                                                        |
| ------ | ---------------------------------------------------------------------------------- |
| `'r'`  | Read (default). Opens the file for reading. File must exist.                       |
| `'w'`  | Write. Opens the file for writing (creates a new file or overwrites if it exists). |
| `'a'`  | Append. Opens the file for appending (creates a new file if it doesn’t exist).     |
| `'rb'` | Read in binary mode.                                                               |
| `'wb'` | Write in binary mode.                                                              |
| `'r+'` | Read and write.                                                                    |

---
## Reading from a File

Once a file is opened in read mode (`'r'`), you can use several methods to read its contents.

### a. **`read()`** – Reads the entire content of the file
```
file = open('example.txt', 'r')
content = file.read()
print(content)
file.close()
```
### b. **`readline()`** – Reads one line at a time
```
file = open('example.txt', 'r')
line1 = file.readline()
line2 = file.readline()
print(line1, line2)
file.close()
```
### c. **`readlines()`** – Reads all lines as a list
```
file = open('example.txt', 'r')
lines = file.readlines()
print(lines)    # List of lines
file.close()
```

---
## Writing to a File

To write to a file, you need to open it in **write (`'w'`)** or **append (`'a'`)** mode.

### a. **`write()`** – Writes a string to the file (overwrites if the file exists)
```
file = open('example.txt', 'w')
file.write('Hello, world!')
file.close()
```
### b. **`writelines()`** – Writes a list of strings (does not add newlines)
```
lines = ['Hello\n', 'World\n']
file = open('example.txt', 'w')
file.writelines(lines)
file.close()
```

---
## File Modes in Detail

- **`'r'`**: Open for reading (default). If the file does not exist, it throws a `FileNotFoundError`.
    
- **`'w'`**: Open for writing. If the file exists, it **overwrites** the content. If it doesn’t exist, a new file is created.
    
- **`'a'`**: Open for **appending**. If the file exists, new content is added at the end. If the file doesn’t exist, a new file is created.
    
- **`'rb'`/`'wb'`**: Opens the file in **binary mode** for reading or writing.
    
- **`'r+'`**: Open for both reading and writing. The file must exist.

---
## File Handling Best Practices (Context Manager)

Instead of manually opening and closing files, **Python’s `with` statement** is a **best practice**. It ensures that the file is properly closed after its use, even if there are errors.
```
with open('example.txt', 'r') as file:
    content = file.read()
    print(content)
# File is automatically closed here
```
### Why use `with`?

- It automatically handles closing the file after the block is executed.
    
- It prevents file leaks (files being left open if an error occurs).

---
## File Pointer: `seek()` and `tell()`

### a. **`seek()`** – Move the file pointer to a specific position
```
file = open('example.txt', 'r')
file.seek(5)    # Move the pointer to the 5th byte
print(file.read())   # Starts reading from byte 5
file.close()
```
### b. **`tell()`** – Returns the current position of the file pointer
```
file = open('example.txt', 'r')
print(file.tell())   # Output: 0 (starts at the beginning)
file.read(5)         # Reads 5 bytes
print(file.tell())   # Output: 5 (moved 5 bytes forward)
file.close()
```

---
## Working with Binary Files

You can also read and write **binary files** using `'rb'` (read binary) and `'wb'` (write binary) modes.

### Example (reading binary data):
```
file = open('example.jpg', 'rb')
binary_data = file.read()
file.close()
```
### Example (writing binary data):
```
file = open('example_copy.jpg', 'wb')
file.write(binary_data)
file.close()
```

---
## File Operations (Renaming, Deleting, etc.)

Python’s `os` module can be used for other file operations, like renaming or deleting files.

### a. **Renaming a file**
```
import os
os.rename('oldname.txt', 'newname.txt')
```
### b. **Deleting a file**
```
import os
os.remove('example.txt')
```
### c. **Checking if a file exists**
```
import os
if os.path.exists('example.txt'):
    print("File exists!")
else:
    print("File does not exist.")
```

---
## Handling Errors (File Not Found, Permissions, etc.)

When dealing with file I/O, it’s important to handle errors gracefully using **`try`** and **`except`** blocks.
```
try:
    file = open('example.txt', 'r')
    content = file.read()
    print(content)
except FileNotFoundError:
    print("File not found!")
except IOError:
    print("An error occurred while reading the file.")
finally:
    file.close()  # Always close the file
```

---
## One-liner Exam Definition

> **File I/O in Python refers to reading from and writing to files using functions like `open()`, along with various methods like `read()`, `write()`, and `seek()`, with the `with` statement being the recommended practice for handling files efficiently.**

---
## Common Mistakes Students Make

- **Forgetting to close files**: Always close files using `file.close()`, or preferably, use the `with` statement to manage this automatically.
    
- **Not handling file exceptions**: Use `try` and `except` to catch potential errors like `FileNotFoundError` or `IOError`.
    
- **Opening files in the wrong mode**: Always choose the correct mode (`'r'`, `'w'`, `'a'`, etc.) based on your operation.