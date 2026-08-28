In Linux, the **root directory** is written as **`/`** (a single forward slash).  
It is the **top-level directory of the entire filesystem**—every file and directory on the system exists somewhere under `/`.

This is different from the **root user** (`root`). The root directory is about **filesystem structure**, not permissions.

---

## What the Root Directory (`/`) Is

- The starting point of the filesystem tree
    
- Contains **essential system directories**
    
- Defined by the **Filesystem Hierarchy Standard (FHS)**
    
- Required for the system to boot and run
    

Example:

`ls /`

---

## Major Directories Under `/` and What They Do

### `/bin` — Essential User Commands

Contains basic commands needed for the system to work, even in recovery mode.

Examples:

- `ls`
    
- `cp`
    
- `mv`
    
- `cat`
    
- `bash`
    

> On modern systems, `/bin` is often a symlink to `/usr/bin`.

---

### `/sbin` — System Administration Commands

Commands mainly used by the system or administrators.

Examples:

- `mount`
    
- `fsck`
    
- `ip`
    
- `reboot`
    

> Often symlinked to `/usr/sbin`.

---

### `/boot` — Bootloader Files

Contains files needed to start Linux.

Typical contents:

- `vmlinuz` – Linux kernel
    
- `initramfs` / `initrd` – initial RAM filesystem
    
- `grub/` – GRUB bootloader files
    

Without `/boot`, the system cannot boot.

---

### `/dev` — Device Files

Virtual files representing hardware and kernel interfaces.

Examples:

- `/dev/sda` – hard drive
    
- `/dev/null` – discards data
    
- `/dev/tty` – terminal
    

Managed dynamically by the kernel and `udev`.

---

### `/etc` — System Configuration

System-wide configuration files (mostly text).

Examples:

- `/etc/passwd` – user accounts
    
- `/etc/fstab` – filesystem mount rules
    
- `/etc/ssh/sshd_config` – SSH server config
    

> “Editable Text Configuration”

---

### `/home` — User Home Directories

Each regular user has a directory here.

Examples:

- `/home/alice`
    
- `/home/bob`
    

Contains personal files, settings, and downloads.

---

### `/root` — Root User’s Home

Home directory for the **root user**.

- Separate from `/home`
    
- Often protected and minimal
    

---

### `/lib` and `/lib64` — Essential Libraries

Shared libraries required by programs in `/bin` and `/sbin`.

Examples:

- `libc.so`
    
- Kernel modules in `/lib/modules/`
    

> Often symlinked to `/usr/lib` and `/usr/lib64`.

---

### `/usr` — User System Resources

Despite the name, this is **not for user home directories**.

Contains:

- `/usr/bin` – most user commands
    
- `/usr/sbin` – admin tools
    
- `/usr/lib` – libraries
    
- `/usr/share` – architecture-independent data
    

This is the **largest directory** on most systems.

---

### `/var` — Variable Data

Files that change frequently.

Examples:

- `/var/log` – system logs
    
- `/var/spool` – mail, print queues
    
- `/var/cache` – cached data
    
- `/var/lib` – application state
    

---

### `/tmp` — Temporary Files

Short-lived files.

- Cleared on reboot (or periodically)
    
- Writable by all users
    

---

### `/proc` — Process & Kernel Info (Virtual)

A virtual filesystem exposing live kernel data.

Examples:

- `/proc/cpuinfo`
    
- `/proc/meminfo`
    
- `/proc/[pid]/` – per-process info
    

No real files exist on disk here.

---

### `/sys` — Hardware & Kernel Interface (Virtual)

Another virtual filesystem used to interact with hardware.

Examples:

- `/sys/class/net` – network devices
    
- `/sys/block` – block devices
    

Used heavily by `udev`.

---

### `/run` — Runtime Data

Temporary system runtime information.

Examples:

- PID files
    
- Socket files
    

Exists only while the system is running.

---

### `/media` and `/mnt` — Mount Points

Used for mounting filesystems.

- `/media` – auto-mounted removable media (USBs, CDs)
    
- `/mnt` – temporary/manual mounts
    

---

### `/opt` — Optional Software

Third-party or vendor software installed separately from the system.

Examples:

- `/opt/google`
    
- `/opt/customapp`
    

---

## Special Notes

- Everything ultimately lives under `/`
    
- Linux uses **mounting** to attach other filesystems into this tree
    
- Many directories today are **symlinks** to `/usr/*` (called the _usr-merge_)
    

---

## Minimal Root Directory for Boot

At minimum, Linux needs:

- `/bin`
    
- `/sbin`
    
- `/lib`
    
- `/etc`
    
- `/dev`
    
- `/proc`
    
- `/sys`
    

---

## Summary

- `/` is the **top of the filesystem**
    
- Contains essential directories defined by the FHS
    
- Mix of real directories and virtual filesystems
    
- Core to how Linux boots, runs, and organizes data