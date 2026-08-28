# LPIC-1 Hardware – Everything You Need to Know

LPIC-1 hardware knowledge is about **recognition, interaction, and administration**, not repair or electronics.

---

## 1. Hardware vs Software (exam mindset)

Linux sees hardware through **layers**:
```
Physical device
↓
Firmware (BIOS / UEFI)
↓
Kernel
↓
Drivers
↓
sysfs / procfs
↓
User-space tools
```

LPIC-1 focuses on:

- Firmware basics
    
- Device identification
    
- Drivers and modules
    
- Storage, CPU, memory
    
- Input/output devices
    
- Power management
    

---

## 2. Firmware: BIOS and UEFI

### BIOS

- Legacy firmware
    
- MBR partitioning (2 TB limit)
    
- Real mode booting
    

### UEFI

- Modern replacement
    
- GPT partitioning
    
- Secure Boot support
    
- Boots `.efi` programs
    

### Exam points

- Linux supports **both**
    
- `/sys/firmware/efi` exists → system booted via UEFI
    
- UEFI + GPT is common on modern systems
    

---

## 3. CPU (Processor)

### CPU concepts you must know

|Concept|Meaning|
|---|---|
|Architecture|x86, x86_64, ARM|
|Cores|Independent execution units|
|Threads|SMT / Hyper-Threading|
|Clock speed|GHz|
|Endianness|Little endian on x86|

### Commands

`lscpu cat /proc/cpuinfo`

### Key files

`/sys/devices/system/cpu/`

### CPU frequency scaling
```
/scaling_governor
/scaling_cur_freq
```

Common governors:

- performance
    
- powersave
    
- ondemand
    
- schedutil
    

---

## 4. Memory (RAM)

### Types

- RAM (volatile)
    
- Swap (disk-backed)
    

### Commands
```
free -h
vmstat
cat /proc/meminfo
```

### Swap

`swapon --show`

Swap types:

- Swap partition
    
- Swap file
    

Exam note:

- Swap is **not a replacement for RAM**
    
- Used when memory pressure occurs
    

---

## 5. Storage Devices

### Disk types

|Type|Examples|
|---|---|
|HDD|/dev/sda|
|SATA SSD|/dev/sda|
|NVMe SSD|/dev/nvme0n1|
|USB|/dev/sdb|

---

### Device naming

|Device|Meaning|
|---|---|
|`/dev/sda`|First SATA/SCSI disk|
|`/dev/sda1`|First partition|
|`/dev/nvme0n1p1`|NVMe partition|

---

### Partitioning

|Scheme|Features|
|---|---|
|MBR|4 primary partitions|
|GPT|Large disks, many partitions|

Commands:
```
lsblk
blkid
fdisk
parted
```

---

### Filesystems (must know)

|Filesystem|Use|
|---|---|
|ext4|Default Linux FS|
|xfs|Large filesystems|
|vfat|FAT32 (UEFI, USB)|
|swap|Swap space|

Mounting:
```
mount
umount
/etc/fstab
```

---

## 6. Block vs Character Devices

|Type|Example|
|---|---|
|Block|Disks (`/dev/sda`)|
|Character|Keyboard, mouse|

Major/minor numbers:

`ls -l /dev/sda`

---

## 7. Device Drivers & Kernel Modules

### Kernel modules

- Drivers are usually **modules**
    
- Loaded dynamically
    

Commands:
```
lsmod
modprobe
modinfo
```

### Files

`/lib/modules/$(uname -r)/`

### Exam traps

- `insmod` does **not** resolve dependencies
    
- `modprobe` **does**
    

---

## 8. sysfs and procfs (VERY IMPORTANT)

### sysfs (`/sys`)

- Hardware and kernel objects
    
- One value per file
    
- Writable attributes
    

Examples:
```
/sys/class/net/
/sys/block/
/sys/devices/
```

---

### procfs (`/proc`)

- Process and runtime info
    

Examples:
```
/proc/cpuinfo
/proc/meminfo
/proc/interrupts
```

---

## 9. Input Devices

### Common input devices

- Keyboard
    
- Mouse
    
- Touchpad
    

Handled via:

- evdev
    
- udev
    

Commands:
```
lsusb
cat /proc/bus/input/devices
```

---

## 10. USB Devices

### USB concepts

- Hot-pluggable
    
- Managed by udev
    
- Tree structure
    

Commands:
```
lsusb
lsusb -t
```

USB info comes from:

`/sys/bus/usb/`

---

## 11. PCI Devices

PCI is used for:

- Network cards
    
- GPUs
    
- Sound cards
    

Commands:
```
lspci
lspci -k
```

Kernel drivers bind to PCI devices.

---

## 12. Network Hardware (Basics)

Devices:

`/sys/class/net/`

Commands:
```
ip link
ethtool
```
Common names:

- eth0 (legacy)
    
- enp0s3 (predictable naming)
    

---

## 13. Power Management

### ACPI

- Power states
    
- Battery info
    
- Thermal management
    

Files:
```
/sys/class/power_supply/
/sys/class/thermal/
```

Commands:
```
upower
acpi
```

---

## 14. Hotplug & udev

### udev

- Manages `/dev`
    
- Reacts to hardware events
    
- Uses sysfs attributes
    

Paths:
```
/etc/udev/rules.d/
/lib/udev/rules.d/
```

---

## 15. Hardware Detection Tools (HIGH-YIELD)

You should recognize **what each tool shows**:

|Tool|Shows|
|---|---|
|`lsblk`|Block devices|
|`lscpu`|CPU|
|`lsusb`|USB|
|`lspci`|PCI|
|`free`|Memory|
|`df`|Disk usage|
|`dmesg`|Kernel messages|
|`hwinfo`|Hardware summary|

---

## 16. Boot Hardware Interaction

During boot:

1. Firmware initializes hardware
    
2. Kernel loads drivers
    
3. init system starts services
    
4. udev creates devices
    

Kernel messages:

`dmesg`

---

## 17. Common LPIC-1 Exam Pitfalls

❌ Confusing `/proc` with `/sys`  
❌ Expecting device files before drivers load  
❌ Forgetting NVMe naming  
❌ Mixing filesystem and block device concepts  
❌ Thinking applications control hardware directly

---

## 18. What LPIC-1 does NOT require

You do **NOT** need:

- Electronics theory
    
- Soldering
    
- Driver programming
    
- Kernel compilation (LPIC-2 topic)
    
- Detailed ACPI tables
    

---

## 19. Final Exam-Oriented Summary

For LPIC-1, hardware knowledge means:

✔ Identify hardware  
✔ Know where Linux exposes it  
✔ Use the right commands  
✔ Understand storage & memory  
✔ Know firmware & boot basics  
✔ Understand drivers & modules