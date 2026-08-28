**udev** is a **device manager in Linux**. It is responsible for **detecting hardware devices**, **naming them**, and **making them available to the system automatically** when they are added or removed.
## What udev Does

When you:

- Plug in a USB flash drive
    
- Connect a keyboard or mouse
    
- Add a hard disk
    
- Insert a network card
    

**udev automatically:**

1. Detects the device
    
2. Creates a device file in `/dev`
    
3. Assigns a consistent name (like `sda`, `ttyUSB0`)
    
4. Applies permissions and ownership
    
5. Triggers actions (scripts, services)
    

All of this happens **without rebooting**.

---
## Where is udev directory?
In Linux, **`udev` does not live in a single directory**, because it is a **device manager**, not just a folder. Its components are spread across several standard locations.

---

## Why udev Is Important

Before udev:

- Device files were static
    
- Admins had to manually create device entries
    
- Hot-plugging devices was unreliable
    

With udev:

- **Dynamic device handling**
    
- **Automatic hardware configuration**
    
- **Faster boot and better device control**

## How udev Works (Step by Step)

1. **Kernel detects hardware**
    
    - Example: USB device plugged in
        
2. **Kernel sends an event (uevent)**
    
3. **udev receives the event**
    
4. **udev checks its rules**
    
5. **udev creates a device node in `/dev`**
    
6. **Optional actions are executed**

## udev Rules

udev behavior is controlled by **rules** written in files.

### Rule Locations

- `/etc/udev/rules.d/` (custom rules)
    
- `/lib/udev/rules.d/` (default system rules)
    

### What Rules Can Do

- Rename devices
    
- Set permissions
    
- Create symbolic links
    
- Run programs or scripts
### Example Rule
```
SUBSYSTEM=="usb", ATTR{idVendor}=="0781", MODE="0666"
```
## Common Device Names Created by udev

| Device            | Example Name     |
| ----------------- | ---------------- |
| Hard disk         | `/dev/sda`       |
| USB drive         | `/dev/sdb`       |
| Serial device     | `/dev/ttyUSB0`   |
| Network interface | `eth0`, `enp3s0` |
## Useful udev Commands

### Check Device Info

`udevadm info --query=all --name=/dev/sda`

### Monitor Device Events

`udevadm monitor`

### Reload Rules
```
udevadm control --reload
udevadm trigger
```

---

## udev and systemd

- udev is now part of **systemd**
    
- The daemon is called **systemd-udevd**
    
- It runs very early during boot

## Summary

- **udev = Linux device manager**
    
- Handles hardware dynamically
    
- Creates `/dev` entries
    
- Controlled by rules
    
- Essential for modern Linux systems