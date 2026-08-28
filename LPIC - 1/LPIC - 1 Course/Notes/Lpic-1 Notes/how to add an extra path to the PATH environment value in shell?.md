There are several ways to add an extra path to the `PATH` environment variable in shell, depending on whether you want it to be temporary or permanent.

## Temporary (Current Session Only)

### For Bash/Zsh/Sh:
```
# Add to the front (highest priority)
export PATH=/new/path:$PATH

# Add to the end (lowest priority)
export PATH=$PATH:/new/path

# Add multiple paths
export PATH=/new/path1:/new/path2:$PATH
```

## Permanent (Persists Across Sessions)

### For Bash (add to one of these files):

- `~/.bashrc` - for interactive shell sessions
    
- `~/.bash_profile` or `~/.profile` - for login shells

```
# Edit the file
nano ~/.bashrc

# Add this line at the end
export PATH=/new/path:$PATH

# Reload the file
source ~/.bashrc
```

### For Zsh:
```
# Edit ~/.zshrc
nano ~/.zshrc

# Add
export PATH=/new/path:$PATH

# Reload
source ~/.zshrc
```

### System-wide (for all users):
```
# Edit /etc/environment (no export needed)
sudo nano /etc/environment
# Add: PATH="/usr/local/sbin:/usr/local/bin:/new/path:..."

# Or add to /etc/profile
sudo nano /etc/profile
export PATH=/new/path:$PATH
```
