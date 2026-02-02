Linux like any other OS needs drivers to work with hardware. 
In Microsoft Windows, you need to install the drivers separately but in Linux, the system has most of the drivers built-in. 
But to prevent the kernel from loading all of them at the same time and to decrease the Kernel size, Linux uses Kernel Modules. 
Loadable kernel modules (.ko files) are object files that are used to extend the kernel of the Linux Distribution. 
They are used to provide drivers for new hardware like IoT expansion cards that have not been included in the Linux Distribution.
You can inspect the modules using the lsmod or manage them via modprobe commands.
# lsmod
**`lsmod`** is a Linux command used to **display the kernel modules that are currently loaded** into the running kernel.
## What Is a Kernel Module?

A **kernel module** is a piece of code that can be **loaded or unloaded at runtime** without rebooting.

Examples:

- Device drivers (Wi-Fi, USB, GPU)
    
- Filesystem support (ext4, ntfs)
    
- Networking features
    

---
## What `lsmod` Shows

When you run:

`lsmod`

You see a table like this:
```
Module                  Size  Used by
iwlwifi               413696  1
cfg80211              704512  1 iwlwifi
snd_hda_intel          57344  3
```

### Column Explanation

|Column|Meaning|
|---|---|
|**Module**|Name of the kernel module|
|**Size**|Memory used by the module (bytes)|
|**Used by**|Number of modules or processes using it|

If the **Used by** value is `0`, the module is loaded but not actively used.
## Why `lsmod` Is Useful

### 1. **Check Driver Status**

- Confirm if a hardware driver is loaded
    
- Example: Wi-Fi not working → check Wi-Fi module
    

---

### 2. **Troubleshooting**

- Identify conflicting or missing modules
    
- Check dependencies between modules
    

---

### 3. **System Monitoring**

- See what kernel features are active
    
- Useful in performance or security audits
## How `lsmod` Works Internally

`lsmod` reads information from:

`/proc/modules`

So `/proc/modules` and `lsmod` show the same data in different formats.

---

## Related Commands (Important)

### Load a Module

`sudo modprobe module_name`

### Remove a Module

`sudo modprobe -r module_name`

### Module Information

`modinfo module_name`

---

## Example Use Case

**Problem:** USB device not detected  
**Check:**

`lsmod | grep usb`

If the USB module isn’t listed, it may not be loaded.

---

## `lsmod` vs Related Commands

| Command    | Purpose             |
| ---------- | ------------------- |
| `lsmod`    | List loaded modules |
| `modprobe` | Load/unload modules |
| `modinfo`  | Show module details |
| `uname -r` | Show kernel version |

---
## What is `modprobe`?

`modprobe` is a **user-space utility for managing Linux kernel modules**. Kernel modules are pieces of code that can be loaded into or removed from the kernel at runtime (e.g., drivers for hardware, filesystem support, networking features).

### What `modprobe` does

- **Loads kernel modules** into the running kernel
    
- **Removes kernel modules**
    
- **Automatically resolves dependencies** between modules
    
- Reads configuration files to apply options and aliases
### Common uses
```
modprobe usb_storage     # Load the usb_storage module
modprobe -r usb_storage  # Remove the usb_storage module
```
### Key features

- **Dependency handling**  
    If a module depends on other modules, `modprobe` loads them automatically using:
```
/lib/modules/$(uname -r)/modules.dep
```

- Configuration support
	Reads:
```
/etc/modprobe.conf
/etc/modprobe.d/*.conf
```
- These files define:
    
    - Module aliases
        
    - Blacklisted modules
        
    - Module parameters
        
- **Preferred over `insmod`**  
    `modprobe` is safer and smarter than `insmod` because it handles dependencies and policies.
    

### Typical real-world use

- Hardware detection at boot
    
- Loading network drivers
    
- Enabling filesystems (e.g., `ext4`)
    
- Managing optional kernel features
---
## Direct Comparison: `modprobe` vs `lsmod`
| Aspect                   | `modprobe`            | `lsmod`                |
| ------------------------ | --------------------- | ---------------------- |
| Purpose                  | Manage kernel modules | Display loaded modules |
| Action type              | Load / unload modules | Read-only              |
| Modifies kernel state    | ✅ Yes                 | ❌ No                   |
| Dependency handling      | ✅ Automatic           | ❌ Not applicable       |
| Configuration aware      | ✅ Yes                 | ❌ No                   |
| Typical verbs            | _add / remove_        | _list / inspect_       |
| Requires root privileges | Usually yes           | No                     |

---
## Summary

- **`lsmod` lists loaded kernel modules**
    
- Helps identify drivers and kernel features
    
- Reads data from `/proc/modules`
    
- Essential for Linux system troubleshooting