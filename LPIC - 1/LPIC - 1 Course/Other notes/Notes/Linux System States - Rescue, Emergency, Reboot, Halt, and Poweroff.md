## **1. RESCUE MODE** (Single-user mode equivalent)

Rescue mode provides a **maintenance environment** with local filesystems mounted and essential services running, but **no networking**.

### **Characteristics:**

- ✅ Local filesystems mounted (read-write)
    
- ✅ Basic system services running
    
- ❌ No network services
    
- 👤 Root user only
    
- 🔧 Full root filesystem access (read-write)
    

### **How to Access:**
```
# From running system (systemd)
sudo systemctl isolate rescue.target

# From boot (GRUB)
# Add to kernel command line:
systemd.unit=rescue.target
# OR simply:
1  # or 'single' or 's'

# Check current mode
systemctl list-units --type=target
```
### **Typical Use Cases:**

- Filesystem repairs (`fsck`)
    
- Password recovery
    
- Configuration file fixes
    
- Troubleshooting boot issues
    

### **Example Rescue Session:**
```
# Enter rescue mode
sudo systemctl isolate rescue.target

# Check mounted filesystems
mount | grep "^/dev"

# Fix a filesystem issue
fsck /dev/sda1

# Remount root as read-write if needed (usually already rw)
mount -o remount,rw /

# Exit rescue mode (reboot)
exit  # or Ctrl+D
# Then select normal boot target
sudo systemctl default
```

---
## **2. EMERGENCY MODE** (Minimal environment)

Emergency mode is the **most minimal** environment - only a **read-only root filesystem** and absolutely nothing else.

### **Characteristics:**

- ✅ Only root filesystem mounted (read-only)
    
- ❌ No other filesystems mounted
    
- ❌ No services running
    
- ❌ No networking
    
- 👤 Root user only
    
- 🔧 Minimal shell environment
    

### **How to Access:**
```
# From running system (systemd)
sudo systemctl isolate emergency.target

# From boot (GRUB)
# Add to kernel command line:
systemd.unit=emergency.target
# OR:
emergency

# From rescue mode (if things go wrong)
systemctl emergency
```
### **Typical Use Cases:**

- Critical filesystem corruption
    
- When rescue mode won't start
    
- Low-level debugging
    
- When you need absolute minimal environment
    

### **Example Emergency Session:**
```
# Enter emergency mode
sudo systemctl isolate emergency.target

# Check root mount (read-only)
mount | grep "on / "

# Remount root as read-write for repairs
mount -o remount,rw /

# Check/fix filesystems
fsck /dev/sda1

# After repairs, either:
exit  # returns to previous state
# OR
systemctl reboot
```

---
## **3. REBOOT** (Restart the system)

Reboot **stops all processes, unmounts filesystems, and restarts the system**.

### **Methods:**
```
# Modern systemd way
sudo systemctl reboot

# Traditional commands
sudo reboot
sudo shutdown -r now
sudo shutdown -r +5 "Rebooting in 5 minutes"

# Forceful reboot (skips some cleanup)
sudo reboot -f

# Via magic SysRq (if system frozen)
echo 1 > /proc/sys/kernel/sysrq
echo b > /proc/sysrq-trigger  # Immediate reboot (dangerous!)
```
### **What Happens During Reboot:**

1. All processes receive SIGTERM (graceful shutdown)
    
2. Wait for processes to terminate
    
3. Send SIGKILL to remaining processes
    
4. Unmount all filesystems
    
5. Sync data to disk
    
6. Restart the system
    

---

## **4. HALT** (Stop the system)

Halt **stops all processes and halts the CPU**, but typically **does not cut power** (system may display "System halted" message).

### **Characteristics:**

- ✅ All processes terminated
    
- ✅ Filesystems unmounted/synced
    
- ✅ CPU halted
    
- ❌ Power usually remains on
    
- 💡 "Halted" state - may need manual power-off
    

### **Methods:**
```
# Modern systemd way
sudo systemctl halt

# Traditional commands
sudo halt
sudo halt -f  # Forceful (skips shutdown sequence)

# Via shutdown (some implementations)
sudo shutdown -H now

# Check if system is halted
# You'll see: "System halted." message
```
### **What Happens During Halt:**
```
# Behind the scenes sequence
1. systemctl halt
2. → All services stopped
3. → Filesystems unmounted
4. → Kernel halts CPU
5. → "System halted" message
6. → Power remains on
```

---
## **5. POWEROFF** (Stop and cut power)

Poweroff **does everything halt does, PLUS sends ACPI signal to cut power**.

### **Characteristics:**

- ✅ All processes terminated
    
- ✅ Filesystems unmounted/synced
    
- ✅ CPU halted
    
- ✅ Power cut (via ACPI)
    
- 💡 Complete shutdown - safe to unplug/move hardware
    

### **Methods:**
```
# Modern systemd way
sudo systemctl poweroff

# Traditional commands
sudo poweroff
sudo shutdown -P now
sudo halt -p  # Halt with poweroff

# Forceful poweroff
sudo poweroff -f

# Via ACPI directly
echo -n "poweroff" > /sys/power/state
```
### **What Happens During Poweroff:**
```
# Behind the scenes sequence
1. systemctl poweroff
2. → All services stopped
3. → Filesystems unmounted
4. → Kernel halts CPU
5. → ACPI power-off signal sent
6. → Power supply cuts electricity
7. → No lights, no fan, completely off
```

---
## **Comparison Table**

|Feature|Rescue|Emergency|Reboot|Halt|Poweroff|
|---|---|---|---|---|---|
|**Root FS**|Read-write|Read-only|N/A|N/A|N/A|
|**Other FS**|Mounted|Unmounted|N/A|N/A|N/A|
|**Networking**|❌ No|❌ No|N/A|N/A|N/A|
|**Services**|Basic only|None|Stopped|Stopped|Stopped|
|**CPU State**|Running|Running|Restarted|Halted|Halted|
|**Power State**|On|On|On → Restart|On|Off|
|**Typical Command**|`systemctl rescue`|`systemctl emergency`|`reboot`|`halt`|`poweroff`|

---

## **Practical Scenarios**

### **Scenario 1: Filesystem Check**
```
# Boot to emergency mode for fsck
sudo systemctl emergency

# Remount root as read-write
mount -o remount,rw /

# Check filesystem
fsck /dev/sda1

# Reboot after repair
systemctl reboot
```
### **Scenario 2: Password Recovery**
```
# Boot to rescue mode
# At GRUB, add '1' to kernel line

# Mount root if not already rw
mount -o remount,rw /

# Change password
passwd root

# Reboot normally
exec /sbin/init  # or exit
```
### **Scenario 3: Proper Server Shutdown**
```
# Alert users first
wall "Server poweroff in 5 minutes"

# Schedule graceful shutdown
sudo shutdown -P +5 "Scheduled maintenance"

# Or immediate but clean
sudo systemctl poweroff
```
### **Scenario 4: Emergency Stop (Frozen System)**
```
# If system is frozen but responsive to SysRq
# Hold Alt+SysRq, then type: R E I S U O
# R: Switch keyboard from raw mode
# E: Send SIGTERM to all processes
# I: Send SIGKILL to all processes
# S: Sync all filesystems
# U: Remount filesystems read-only
# O: Power off

# Or if you remember only one:
echo o > /proc/sysrq-trigger  # Immediate poweroff
```

---
## **Key Takeaways**

1. **Emergency** → Most minimal, root read-only (for critical repairs)
    
2. **Rescue** → Full filesystem access, still no network (for maintenance)
    
3. **Reboot** → Restarts the system (for updates/kernel changes)
    
4. **Halt** → Stops everything but leaves power on (rarely used today)
    
5. **Poweroff** → Complete shutdown, cuts power (normal shutdown)
    

**Modern systems** typically use `systemctl` commands:

- `systemctl rescue` → Rescue mode
    
- `systemctl emergency` → Emergency mode
    
- `systemctl reboot` → Reboot
    
- `systemctl halt` → Halt
    
- `systemctl poweroff` → Poweroff
    

**Legacy commands** still work (they're symlinks to systemctl):

- `reboot` → `systemctl reboot`
    
- `halt` → `systemctl halt`
    
- `poweroff` → `systemctl poweroff`
