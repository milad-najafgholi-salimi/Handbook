Start a named session (recommended):
```
tmux new -s myproject
```

**`prefix`** means **hold `Ctrl`, press `b`, release both**.  
Example: `prefix + c` = `Ctrl-b` then `c`.

### Sessions (Your Workspaces):

| Action                                 | Command                          |
| -------------------------------------- | -------------------------------- |
| Detach from session (leave it running) | `prefix + d`                     |
| List all sessions                      | `tmux ls` (run **outside** tmux) |
| Re-attach to a session                 | `tmux a -t myproject`            |
| Rename current session                 | `prefix + $`                     |
| Kill a session                         | `tmux kill-session -t myproject` |

### Windows (Like Browser Tabs):

|Action|Command|
|---|---|
|Create a new window|`prefix + c`|
|Next window|`prefix + n`|
|Previous window|`prefix + p`|
|Go to window #3|`prefix + 3`|
|Rename current window|`prefix + ,` (that's comma)|
|List all windows|`prefix + w`|
|Kill current window|`prefix + &` (then press `y` to confirm)|
### Panes (Split Screen):

| Action                              | Command                                     |
| ----------------------------------- | ------------------------------------------- |
| Split vertically (left/right)       | `prefix + %`                                |
| Split horizontally (top/bottom)     | `prefix + "` (that's double-quote)          |
| Move to pane left/right/up/down     | `prefix + arrow keys`                       |
| Kill current pane                   | `prefix + x` (then press `y`)               |
| Make current pane fullscreen (zoom) | `prefix + z` (press again to unzoom)        |
| Swap pane with neighbor             | `prefix + {` (left) or `prefix + }` (right) |
| Show pane numbers                   | `prefix + q`                                |
| Go to pane #2                       | `prefix + q` then quickly press `2`         |

### Copy Mode (Scrolling & Copying):

To scroll up and see history:

1. Enter copy mode: `prefix + [`
    
2. Navigate with: `arrow keys`, `PageUp`, `PageDown`
    
3. Exit copy mode: `q` or `Enter`
    

**To copy text (using keyboard):**

1. `prefix + [` to enter copy mode
    
2. Move cursor to start of text
    
3. Press `Space` to begin selection
    
4. Move cursor to end of text
    
5. Press `Enter` to copy
    
6. Paste with: `prefix + ]`
    

**Easier way (no config needed):**  
Just hold `Shift` and select text with your mouse – it copies to your system clipboard directly (works in most terminals).

### Built-in Help

If you ever forget a key:

- `prefix + ?` – Shows every single keybinding in a scrollable list (press `q` to exit)

### Show time:
```
ctrl + b then press t
```

