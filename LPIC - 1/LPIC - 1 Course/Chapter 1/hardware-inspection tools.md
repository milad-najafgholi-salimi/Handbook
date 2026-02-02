These four commands are **hardware-inspection tools** in Linux.  
They all _list_ things, but each one looks at **a different layer of the system**.

I’ll explain **what each command shows**, **where the data comes from**, **common options**, and **when you should use it**.

---

# 1. `lsusb` — USB Devices

### What it does

Lists **USB buses and USB devices** connected to the system.

### Data source

- Reads from **`/sys/bus/usb`**
    
- Uses USB descriptors provided by devices
    

### Basic usage

`lsusb`

Example output:
```
Bus 002 Device 003: ID 046d:c534 Logitech, Inc. Unifying Receiver
```

### Useful options
```
lsusb -v        # verbose (very detailed)
lsusb -t        # tree view (USB topology)
```

### When to use it

- USB mouse/keyboard not working
    
- Checking USB IDs for drivers
    
- Debugging USB hubs or ports
    

---

# 2. `lspci` — PCI / PCIe Devices

### What it does

Lists **PCI and PCI Express devices**.

These include:

- GPUs
    
- Network cards
    
- Sound cards
    
- SATA/NVMe controllers
    

### Data source

- Reads from **`/sys/bus/pci`**
    
- Uses PCI configuration space
    

### Basic usage

`lspci`

Example:
```
00:02.0 VGA compatible controller: Intel Corporation UHD Graphics
```

### Useful options
```
lspci -v        # verbose
lspci -vv       # very verbose
lspci -k        # show kernel driver in use
```

Example:
```
lspci -k | grep -A3 VGA
```

### When to use it

- Checking GPU or network hardware
    
- Verifying drivers in use
    
- Diagnosing PCI device issues
    

---

# 3. `lsblk` — Block Devices (Disks & Partitions)

### What it does

Lists **block devices** in a **tree format**.

Includes:

- Hard drives
    
- SSDs
    
- NVMe devices
    
- Partitions
    
- LVM, RAID, loop devices
    

### Data source

- Reads from **`/sys/block`**
    
- Queries udev metadata
    

### Basic usage

`lsblk`

Example:
```
NAME   MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
sda      8:0    0  1T   0 disk
├─sda1   8:1    0 512M  0 part /boot
└─sda2   8:2    0 999G  0 part /
```
### Useful options
```
lsblk -f    # show filesystem info
lsblk -o    # custom columns
lsblk -p    # full device paths
```

Example:

`lsblk -f`

### When to use it

- Viewing disks and partitions
    
- Before mounting or formatting
    
- Understanding storage layout
    

---

# 4. `lshw` — Complete Hardware Overview

### What it does

Shows **detailed hardware information** for the entire system.

Covers:

- CPU
    
- RAM
    
- Motherboard
    
- Storage
    
- Network
    
- USB
    
- PCI devices
    

### Data source

- Reads from `/proc`, `/sys`, DMI tables
    
- Requires root for full details
    

### Basic usage

`sudo lshw`

### Useful options
```
lshw -short       # summary view
lshw -class cpu   # only CPUs
lshw -class disk  # only disks
```

Example:

`sudo lshw -short`

### When to use it

- Full system inventory
    
- Hardware documentation
    
- Diagnosing complex hardware issues
    

---

# Quick Comparison Table

|Command|Focus|Best For|
|---|---|---|
|`lsusb`|USB devices|USB troubleshooting|
|`lspci`|PCI/PCIe devices|GPU, NIC, controllers|
|`lsblk`|Storage devices|Disks & partitions|
|`lshw`|All hardware|Full system overview|

---

# How They Work Together (Real-World Example)

**“My Wi-Fi isn’t working”**

1. `lspci` → Is the Wi-Fi card detected?
    
2. `lspci -k` → Is a driver loaded?
    
3. `lsusb` → If it’s a USB Wi-Fi adapter
    
4. `lshw -class network` → Detailed status
    

---

# Important Notes

- `lsusb` and `lspci` usually work without root
    
- `lshw` needs `sudo` for complete info
    
- `lsblk` is safe (read-only), but often used before dangerous commands like `mkfs`
    

---

## Summary

- **`lsusb`** → USB layer
    
- **`lspci`** → PCI/PCIe layer
    
- **`lsblk`** → Storage layout
    
- **`lshw`** → Big picture hardware view