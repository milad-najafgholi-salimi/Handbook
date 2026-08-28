## 1. What are wildcards?

**Wildcards** are special characters that stand in for **one or more characters** in text patterns.  
They are most commonly used in:

- Command-line shells (bash, zsh, PowerShell)
    
- Programming languages
    
- File systems
    
- Search tools
    

Wildcards **do not match arbitrarily**—each has specific rules depending on the environment.

---

## 2. What is file globbing?

**File globbing** is the process where a program (usually the shell) **expands wildcard patterns into actual filenames** before a command runs.

Example:

`ls *.txt`

What really happens:

1. The shell looks in the current directory
    
2. Finds all files ending in `.txt`
    
3. Rewrites the command as:
    
    `ls file1.txt notes.txt report.txt`
    
4. Then executes `ls`
    

💡 **Key point:**  
Globbing is usually done by the **shell**, not the command (`ls` never sees `*.txt`).

---

## 3. Common wildcard characters

### `*` — match any number of characters

- Matches **zero or more** characters
    
- Does **not** match directory separators (`/`)
    

`*.log        # error.log, access.log file*        # file, file1, file_backup`

---

### `?` — match exactly one character

`file?.txt    # file1.txt, fileA.txt`

❌ Does not match:

`file10.txt   # too many characters`

---

### `[ ]` — character classes

Matches **one character from a set or range**.

`file[123].txt    # file1.txt, file2.txt, file3.txt file[a-z].txt    # filea.txt through filez.txt`

Negation:

`file[!0-9].txt    # fileA.txt but not file1.txt`

---

## 4. Recursive globbing (`**`)

In some shells (bash with `globstar`, zsh by default):

`**/*.py`

Matches:

- `main.py`
    
- `src/app.py`
    
- `src/utils/helpers.py`
    

This is **not POSIX standard** and must be enabled in bash:

`shopt -s globstar`

---

## 5. Hidden files and globbing

Files starting with `.` (dotfiles) are **not matched by `*`** by default.

`*         # does NOT match .bashrc .*        # matches .bashrc, .git`

⚠️ `.*` also matches `.` and `..` in some shells.

---

## 6. Globbing vs regular expressions (very important)

|Feature|Globbing|Regular Expressions|
|---|---|---|
|Who expands it|Shell|Program/library|
|`*` meaning|Any characters|Repeat previous token|
|Recursive matching|Limited|Fully supported|
|Anchored by default|Yes|No|
|Complexity|Simple|Powerful|

Example:

`ls file.*       # glob grep "file.*"   # regex`

These behave very differently.

---

## 7. When globbing happens (order of operations)

Typical shell expansion order:

1. Brace expansion `{a,b}`
    
2. Variable expansion `$VAR`
    
3. Command substitution `$(...)`
    
4. **Globbing**
    
5. Word splitting
    

This matters:

`echo "$HOME/*.txt"`

➡️ No globbing (quoted)

`echo $HOME/*.txt`

➡️ Globbing occurs

---

## 8. Quoting disables globbing

`ls "*.txt"`

The shell passes the literal `*.txt` to `ls`.

This is often required when:

- You want a program to handle the pattern
    
- The pattern is not a filename
    

---

## 9. What happens if nothing matches?

Depends on the shell:

### Bash (default)

`ls *.doesnotexist`

➡️ `*.doesnotexist` passed literally

Optional behavior:

`shopt -s nullglob`

➡️ Pattern expands to **nothing**

---

## 10. Globbing in programming languages

### Python

`import glob  glob.glob("*.txt")`

### Node.js

`glob("**/*.js")`

Languages usually:

- Do **not** auto-expand wildcards
    
- Require libraries
    

---

## 11. Practical real-world examples

### Delete files safely

`rm -- *.tmp`

### Process batches

`for f in *.csv; do   echo "Processing $f" done`

### Exclude patterns

`rsync -av --exclude="*.log" src/ dest/`

---

## 12. Common pitfalls

❌ Expecting globbing in scripts without a shell  
❌ Confusing regex with glob syntax  
❌ Accidentally matching too many files (`rm *`)  
❌ Forgetting hidden files are excluded

---

## 13. Summary

- **Wildcards** are pattern characters like `*`, `?`, `[ ]`
    
- **Globbing** is the shell expanding those patterns into filenames
    
- Globbing happens **before** a command runs
    
- It is **not regex**
    
- Quoting disables it
    
- Behavior varies by shell