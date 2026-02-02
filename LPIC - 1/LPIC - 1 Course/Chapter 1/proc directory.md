The **`/proc` directory** in Linux is a **virtual (pseudo) filesystem** that provides **real-time information about the kernel, hardware, and running processes**.
## What Makes `/proc` Special

- Files **do not exist on disk**
    
- They are **created dynamically in memory**
    
- Their contents change **in real time**
    
- Reading them gives **current system information**
---
## Why `/proc` Exists

Before `/proc`, system tools needed complex kernel interfaces.  
`/proc` provides a **simple file-based interface** so programs can:

- Read kernel data
    
- Monitor processes
    
- Tune system behavior
    

Many Linux commands (`ps`, `top`, `free`, `uptime`) get their data from `/proc`.
## Structure of `/proc`

### 1. **Process Directories (`/proc/PID`)**

Each running process has a directory named after its **process ID (PID)**.

Example:

`/proc/1234/`

Common files inside:

|File|Purpose|
|---|---|
|`cmdline`|Command used to start the process|
|`status`|Process state, memory, UID|
|`stat`|Raw process statistics|
|`fd/`|Open file descriptors|
|`exe`|Symlink to executable|
|`cwd`|Current working directory|

---

### 2. **System Information Files**

These show kernel and hardware data.

|File|Description|
|---|---|
|`/proc/cpuinfo`|CPU details|
|`/proc/meminfo`|Memory usage|
|`/proc/uptime`|System uptime|
|`/proc/loadavg`|System load|
|`/proc/version`|Kernel version|

Example:

`cat /proc/cpuinfo`

---

### 3. **Kernel Control & Tuning Files**

Some `/proc` files can be **written to** (as root) to change kernel behavior.

Examples:

|File|Function|
|---|---|
|`/proc/sys/net/ipv4/ip_forward`|Enable routing|
|`/proc/sys/vm/swappiness`|Control swap usage|

Example:
```
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward
```
These settings are often managed permanently using `sysctl`.

---

## `/proc/sys` and `sysctl`

- `/proc/sys` contains kernel parameters
    
- `sysctl` is a safer interface to modify them
    

Example:
```
sysctl vm.swappiness
sysctl -w vm.swappiness=10
```

---

## How Programs Use `/proc`

- `ps` → reads `/proc/PID/stat`
    
- `top` → reads `/proc/meminfo` and process data
    
- `free` → reads `/proc/meminfo`
    
- `uptime` → reads `/proc/uptime`
    

---

## Security & Permissions

- Some files are readable by all users
    
- Process directories are restricted by ownership
    
- Sensitive info may require root access
    

---

## `/proc` vs Real Filesystems

|Feature|`/proc`|Disk FS|
|---|---|---|
|Stored on disk|❌|✅|
|Dynamic|✅|❌|
|Shows kernel state|✅|❌|
|Writable for tuning|Limited|Yes|

---
## Summary

- **`/proc` = virtual filesystem**
    
- Exposes kernel & process information
    
- Essential for monitoring and system tools
    
- Enables kernel tuning and diagnostics