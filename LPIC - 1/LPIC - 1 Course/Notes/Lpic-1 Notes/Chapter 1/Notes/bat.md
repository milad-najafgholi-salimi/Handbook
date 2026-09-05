![pic-13](Pics/13.png)

Bat is really good. Use it and thank me later.

```
sudo apt install bat

bat file
# or
batcat file
```

### The Name: `bat` vs. `batcat`
On **Debian and Ubuntu**, the binary is named `batcat` to avoid a name conflict with an older package; On most other Linux distributions, you just type `bat`.

- If you're on Ubuntu/Debian, you'll use `batcat` in your commands.
- A popular workaround is to create an alias: `alias bat='batcat'` in your `~/.bashrc` (or `~/.zshrc` if you are using *zsh* shell) file, so you can just type `bat`.

### Search (Just Like Less!)  
Because it uses `less` as its pager, the search commands are exactly what you already know.

- Press `/` to search forward.
    
- Press `?` to search backward.
    
- Press `n` to go to the next match.
    
- Press `N` to go to the previous match.

### Advanced Features

- **Show Git changes**: `batcat -d my_script.py` will highlight lines based on your Git status.
    
- **Disable paging**: If you want to just print to the terminal (like `cat`), use `-p` or `-pp` to also disable decorations.
    
- **Highlight specific lines**: Use the `--highlight-line` option. For example, `batcat --highlight-line 10:20` highlights lines 10 through 20.

### A Tip:
use `bat` for anything if you really love it:
```
command something | bat
```

Like:

```
man ls | bat
```

Also like (in Debian base distros):

```
man batcat | bat
```
