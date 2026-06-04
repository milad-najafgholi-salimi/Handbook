In the world of programming and operating systems, a **zero exit status** is the universal signal for **“Success.”**

When a program finishes running, it sends a small integer back to the Operating System (the parent process). This is called the **Exit Code** or **Return Code**.

### 1. The Standard Rule

- **`0` (Zero):** Means “Success” / “No errors occurred.”
- **Non-zero (1, 2, 127, etc.):** Means “Failure” / “Something went wrong.”

Think of `0` as the “all clear” signal.

---

### 2. How it works in practice (Linux/macOS)

Every command you run in the terminal is a program that returns an exit status. You can check it immediately after a command by looking at the special variable `$?`.

**Example of Success:**
```
ls my_folder
# (If it works, the exit status is 0)
echo $?
# Output: 0
```
