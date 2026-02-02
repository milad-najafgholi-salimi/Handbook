**`sysfs`** is a **virtual filesystem in Linux** that exposes the **kernel’s internal view of hardware, drivers, and kernel subsystems** to user space in a **structured, file-based interface**.
**[[Sysfs - Explain above, like you're a child]]**

It lets you **inspect and control kernel objects** by reading and writing plain text files.

---

## 1. What sysfs is (high-level)

- A **pseudo-filesystem** (no data stored on disk)
    
- Mounted at:
    
    `/sys`
    
- Backed directly by **kernel data structures**
    
- Created at runtime
    
- Each file typically represents:
    
    - A device
        
    - A driver
        
    - A kernel parameter
        
    - A relationship between objects
        

In short:

> **sysfs = kernel objects → files**

---

## 2. Why sysfs exists

Before sysfs, Linux used:

- `/proc` (process + kernel info mixed together)
    
- Ad-hoc ioctl interfaces
    
- Inconsistent user-space APIs
    

Problems:

- Hard to discover
    
- Hard to script
    
- Poor structure
    

**sysfs was created to:**

- Separate **process info** (`/proc`) from **hardware/kernel objects**
    
- Provide a **stable, discoverable API**
    
- Support **udev**, hotplug, and dynamic device management
    

---

## 3. sysfs vs procfs

|Feature|sysfs (`/sys`)|procfs (`/proc`)|
|---|---|---|
|Purpose|Devices & kernel objects|Processes & kernel stats|
|Structure|Object-oriented|Process-centric|
|Files|Mostly small text values|Mix of text & binary|
|Writable|Yes (carefully)|Sometimes|
|Backed by|Kernel object model (kobjects)|Process tables & kernel state|

Rule of thumb:

- **Hardware & drivers → `/sys`**
    
- **Processes & runtime stats → `/proc`**
    

---

## 4. Core concepts behind sysfs

### 4.1 kobjects

sysfs mirrors the kernel’s **kobject hierarchy**.

Each kobject:

- Has a name
    
- Has attributes
    
- Can belong to a parent
    

This directly becomes:

`/sys/<subsystem>/<object>/<attribute>`

---

### 4.2 Attributes = files

Each file usually:

- Contains **one value**
    
- Is [[ASCII]] text
    
- Is read with `cat`
    
- Is modified with `echo`
    

Example:
```
cat /sys/class/backlight/intel_backlight/brightness
echo 500 | sudo tee /sys/class/backlight/intel_backlight/brightness
```

---

## 5. Major directories in `/sys`

### `/sys/devices`

The **real hardware topology**.

- Physical buses
    
- Devices
    
- CPU cores
    
- PCI tree
    

Example:

`/sys/devices/pci0000:00/0000:00:14.0/usb1/1-2/`

---

### `/sys/class`

**High-level device classes** (logical grouping).

Examples:
```
/sys/class/net/          # network interfaces
/sys/class/block/        # disks
/sys/class/backlight/    # displays
/sys/class/thermal/      # temperature sensors
```

Each entry is usually a **symlink into `/sys/devices`**.

---

### `/sys/block`

Block devices only:
```
/sys/block/sda/
/sys/block/nvme0n1/
```

Convenience layer over `/sys/devices`.

---

### `/sys/bus`

Bus types:
```
/sys/bus/pci/
/sys/bus/usb/
/sys/bus/i2c/
```

Includes:

- Devices
    
- Drivers
    
- Bind/unbind controls
    

---

### `/sys/module`

Loaded kernel modules:

`ls /sys/module/`

Each module exposes:

- Parameters
    
- Reference counts
    
- State
    

---

### `/sys/kernel`

Kernel-wide features:

- cgroups
    
- tracing
    
- memory
    
- security frameworks
    

---

## 6. Reading vs writing sysfs

### Reading (safe)

`cat /sys/class/net/eth0/operstate`

Returns:

`up`

### Writing (powerful and dangerous)
```
echo 1 | sudo tee /sys/block/sda/device/delete
```

That **removes a device from the kernel**.

⚠️ Writing to sysfs:

- Requires root
    
- Takes effect immediately
    
- Has no confirmation
    
- Can crash hardware or the system
    

---

## 7. sysfs and udev

**udev relies heavily on sysfs**.

Workflow:

1. Device appears
    
2. Kernel creates sysfs entries
    
3. udev reads attributes
    
4. udev creates:
    
    - `/dev` nodes
        
    - Permissions
        
    - Symlinks
        
    - Triggers scripts
        

Example udev rule:
```
ATTR{idVendor}=="046d", ATTR{idProduct}=="c52b"
```

Those `ATTR{}` values come from sysfs.

---

## 8. sysfs design rules (important)

Kernel developers enforce strict rules:

- One value per file
    
- Text only
    
- No complex parsing
    
- Stable ABI
    
- No policy in kernel
    

This is why sysfs looks simple—even crude.

---

## 9. sysfs is not a filesystem in the usual sense

- No storage
    
- No timestamps
    
- No file sizes that matter
    
- Permissions reflect kernel intent
    
- Files appear/disappear dynamically
    

Running:

`stat /sys/class/net/eth0/mtu`

Shows “files” that don’t behave like disk files.

---

## 10. Common real-world uses

- Inspect hardware:
```
lspci -vv
```
(internally reads sysfs)
    
- Change CPU governor:
```
echo performance | sudo tee /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
```
- Control LEDs:
```
echo timer | sudo tee /sys/class/leds/input3::capslock/trigger
```
    
- Debug drivers
    

---

## 11. When _not_ to use sysfs directly

Avoid:

- Application-level logic
    
- Persistent configuration
    
- Anything requiring validation
    

Instead:

- Use `udev`
    
- Use `systemd`
    
- Use purpose-built tools (`ip`, `ethtool`, `lsblk`)
    

---

## 12. Summary

- **sysfs** is a **virtual filesystem** exposing kernel objects
    
- Located at **`/sys`**
    
- Mirrors the kernel’s internal object model
    
- Readable and sometimes writable
    
- Central to Linux hardware discovery and control
    
- Not meant for casual or unsafe use