## What is an Interpreter?

An **interpreter** is a program that **reads source code and executes it directly**, usually **line by line**, without first creating a separate compiled executable file.
In simple terms:
```
Source Code → Interpreter → Execution
```

The interpreter:

1. Reads the code
2. Translates it into machine-understandable instructions
3. Executes it immediately

## Interpreter vs Compiler in General

Key difference:

Interpreter:

- Executes code **line by line**
- No separate executable file is produced
- Usually slower

Compiler:

- Translates the **entire program first**
- Produces a **compiled executable file**
- Usually faster

Examples:

Interpreter-based languages:

- Python
- JavaScript
- Ruby
- PHP

Compiled languages:

- C
- C++
- Go
- Rust

---
Question:
>Does Python have Compiler? Or just have interpreter?

Start of Answer:

Short answer:
> ✅ **Python has BOTH a compiler and an interpreter.**
> 
> ❌ It is NOT “just interpreted.”

When you run:
```
python script.py
```
This happens internally (CPython):
```
Source Code (.py)
        ↓
[Compiler]
        ↓
Bytecode (.pyc)
        ↓
[Interpreter / Virtual Machine]
        ↓
Machine Instructions
        ↓
CPU
```

>Note:
>CPython is the standard python interpreter that has compiler inside itself.

---
Question:
>But you said Python is an interpreter-based language. And now you say Python has both and I'm seeing in the terminology that you are showing, that the compiler is run before interpreter. I'm confusing now. 

Start of Answer:
## 1. دو چیز را جدا کن:

### 1) «زبان» (Python)

### 2) «Implementation» (مثلاً CPython)

وقتی می‌گوییم:

> “Python is an interpreted language”

این در واقع یک **برچسب ساده‌شده** است برای این واقعیت که **رایج‌ترین پیاده‌سازی Python یعنی CPython**، کد را به شکل **interpreted** اجرا می‌کند (نه به صورت یک executable مستقل مثل C++).

اما از نظر فنی:

- **Python (زبان)** فقط یک **specification/grammar** است.
- **CPython** یک **برنامه C** است که:
    - یک **compiler** داخلی دارد (source → bytecode)
    - و یک **interpreter / VM** دارد (bytecode → اجرای واقعی)

پس این دو جمله با هم تضاد ندارند:

- «Python یک interpreted language است» → از دید کاربر، چون شما کامپایل جداگانه و exe مستقل نمی‌بینید.
- «CPython هم compiler دارد هم interpreter» → از دید معماری داخلی.

End of Answer.

---
So there are many interpreters and it depends on what program or application is running.
### 1. Different Languages = Different Interpreters

If you have a Python script, you need a Python interpreter. If you have a Ruby script, you need a Ruby interpreter.

- **Python script** → `python.exe` (in Windows)
- **Ruby script** → `ruby.exe` (in Windows)
- **JavaScript (in Node)** → `node.exe` (in Windows)

Your operating system acts as a dispatcher: it sees the file extension (or the “shebang” line at the top of a script) and calls the corresponding interpreter program to handle that code.

### 2. Different “Flavors” of the Same Language

Even for one language like Python, there are multiple interpreters available, and they are different **programs**:

- **CPython:** The “standard” one (written in C). This is the one you probably use 99% of the time.
- **PyPy:** A different interpreter (written in Python/RPython) that uses **JIT (Just-In-Time) compilation** to make code run much faster.
- **Jython:** An interpreter for Python that runs on the **Java Virtual Machine (JVM)**.
- **IronPython:** An interpreter for Python that runs on the **.NET framework**.

These are all _different_ binary files on your disk. You could technically install all of them, and depending on how you call them, you are using a different “brain” to execute your Python code.

---
Question:
>What is a 'compiler'? Compare with 'Interpreter'.

Start of Answer:
### Compiler vs. Interpreter (The “Master” Comparison)

| Feature                 | Compiler                                            | Interpreter                                              |
| ----------------------- | --------------------------------------------------- | -------------------------------------------------------- |
| **Output**              | Creates a standalone binary file.                   | No standalone file created.                              |
| **Translation**         | Translates the **entire** program at once.          | Translates **line-by-line** (or statement-by-statement). |
| **Speed**               | Very fast execution (already in machine code).      | Generally slower (translation happens while running).    |
| **When is it checked?** | Errors are found _before_ execution (Compile-time). | Errors are found _during_ execution (Runtime).           |
End of Answer.