### 1. The Most Important Shortcut (Search)

**`/`** (forward slash) + **word** → Searches **forward** for that word.  
**`?`** (question mark) + **word** → Searches **backward**.  
**`n`** → Go to the **next** search result.  
**`N`** (Shift+n) → Go to the **previous** search result.

> **Pro tip:** Search for flags exactly. Type `/--help` to find the `--help` option instantly.

### 2. Scrolling Like a Pro

| Key                    | Action                             |
| ---------------------- | ---------------------------------- |
| **`Space`** or **`f`** | Scroll down one full page          |
| **`b`**                | Scroll **up** one full page (back) |
| **`Enter`**            | Scroll down **one line** at a time |
| **`d`**                | Scroll down half a page            |
| **`u`**                | Scroll up half a page              |

### 3. Jump to the Top / Bottom

| Key               | Action                               |
| ----------------- | ------------------------------------ |
| **`g`**           | Go to the **very top** of the manual |
| **`G`** (Shift+g) | Go to the **very bottom**            |

### 4. Get Help Inside `man`

**`h`** → Opens the built-in help screen with **every** shortcut. (Press `q` to close it).

### 5. Quitting

**`q`** → Quit and return to your terminal. (Always works, always safe).

## Open to a Specific Section

Man pages are divided into sections. To open a specific one:
```
man 5 passwd   # Opens the file format description, not the command
man 1 passwd   # Opens the command itself (default)
```

Type `man man` to see the full list of sections.

## Man Page Sections

Man pages are organized into **sections**:

|Section|Content|
|---|---|
|1|User commands (executable programs)|
|2|System calls (kernel functions)|
|3|Library functions (C standard library)|
|4|Special files (devices, /dev files)|
|5|File formats and configuration files|
|6|Games and screensavers|
|7|Miscellaneous (macro packages, conventions)|
|8|System administration commands|