### Navigation (Moving Around)
| To Do This...                 | Press This...                      |
| ----------------------------- | ---------------------------------- |
| **Scroll down one line**      | `j` or `↓` (Down Arrow) or `Enter` |
| **Scroll up one line**        | `k` or `↑` (Up Arrow)              |
| **Scroll down one full page** | `Spacebar` or `f` (forward)        |
| **Scroll up one full page**   | `b` (backward)                     |
| **Go to the very top**        | `g` (think "go to start")          |
| **Go to the very bottom**     | `G` (think "go to end")            |
| **Go to line 150**            | Type `150` then press `g`          |

### Searching

Finding text inside a huge log file is where `less` shines.

|To Do This...|Press This...|
|---|---|
|**Search FORWARD** (downwards)|Type `/` then your search term, press `Enter`. Example: `/error`|
|**Search BACKWARD** (upwards)|Type `?` then your search term, press `Enter`. Example: `?warning`|
|**Find the NEXT match**|Press `n` (for "next")|
|**Find the PREVIOUS match**|Press `N` (capital N)|

> **Pro Tip:** Searches are case-_insensitive_ by default in modern `less`. If you want case-sensitive, type `/error` with a capital letter, or start `less` with the `-i` flag.