## Understanding Runlevels (SysV init) vs. Targets (systemd)

### Traditional Runlevels (SysV init)

|Runlevel|Purpose|
|---|---|
|0|Halt/shutdown|
|1|Single-user mode (maintenance)|
|2|Multi-user mode without networking|
|3|Multi-user mode with networking|
|4|Not used/customizable|
|5|Multi-user with networking + GUI|
|6|Reboot|

### systemd Targets (Modern Equivalent)

|Target|Equivalent Runlevel|Purpose|
|---|---|---|
|poweroff.target|0|Shut down|
|rescue.target|1|Single-user mode|
|multi-user.target|3|Multi-user, text mode|
|graphical.target|5|Multi-user with GUI|
|reboot.target|6|Reboot|
|emergency.target|N/A|Minimal emergency shell|

---

## 1. Setting Default Runlevel/Boot Target

### **SysV init** (/etc/inittab)
```
# View current default runlevel
grep initdefault /etc/inittab

# Set default to runlevel 3
id:3:initdefault:
```
### **systemd** (Modern systems)
```
# View current default target
systemctl get-default

# Set default to multi-user.target (runlevel 3)
sudo systemctl set-default multi-user.target

# Set default to graphical.target (runlevel 5)
sudo systemctl set-default graphical.target

# List all available targets
systemctl list-units --type=target --all
```

---
## 2. Changing Between Runlevels/Boot Targets

### SysV init Commands
```
# Switch to runlevel 3 (multi-user)
init 3
telinit 3

# Switch to single-user mode (runlevel 1)
init 1
telinit 1

# Check current runlevel
who -r
runlevel
```
### systemd Commands
```
# Switch to multi-user.target
sudo systemctl isolate multi-user.target

# Switch to graphical.target
sudo systemctl isolate graphical.target

# Switch to rescue mode (single-user)
sudo systemctl isolate rescue.target

# Switch to emergency mode (minimal environment)
sudo systemctl isolate emergency.target

# Check current target
systemctl list-units --type=target | grep -E "graphical|multi-user|rescue"
```

---
## Scattered notes

The preferred method to shut down or reboot the system is to use the `shutdown` command, which first sends a warning message to all logged-in users and blocks any further non-root logins. It then signals init to switch runlevels. The init process then sends all running processes a **SIGTERM** signal, giving them a chance to save data or otherwise properly terminate. After 1 minute or another delay, if specified, init sends a **SIGKILL** signal to forcibly end each remaining process.
- Default is a 1-minute delay and then going to runlevel 1
- -h will halt the system
- -r will reboot the system
- Time is hh:mm or n (minutes) or now
- Whatever you add, will be broadcasted to logged-in users using the wall command
- If the command is running, ctrl+c or the shutdown -c will cancel it
```
shutdown -r 60 Reloading updated kernel
```
for more advanced users:
- -t60 will delay 60 seconds between **SIGTERM** and **SIGKILL**
- if you cancel a shutdown, users will get the news
#### Halt, reboot, and poweroff
- The `halt` command halts the system.
- The `poweroff` command halts the system and then attempts to power it off.
- The `reboot` command halts the system and then reboots it.

On most distros, these are symbolic links to the systemctl utility

#### Notifying users
It is good to be informed! Especially if the system is going down; Especially on a shared server. Linux has different tools for system admins to notify their users:
- `wall`: Sending *wall messages* to logged-in users
- `/etc/issue`: Text to be displayed on the tty terminal logins (before login)
- `/etc/issue.net`: Text to be displayed on the remote terminal logins (before login)
- `/etc/motd`: Message of the day (after login). Some companies add "Do not enter if you are not allowed" texts here for legal reasons.
- `mesg`: Command controls if you want to get wall messages or not. You can do `mesg n` and `who -T` will show **mesg** status. Note that `shutdown` wall messages do not respect the **mesg** status

**systemctl** sends wall messages for emergency, halt, power-off, reboot, and rescue

---
## 3. Shutdown and Reboot Commands

### **Shutdown Command** (most flexible)
```
# Shutdown immediately
sudo shutdown -h now

# Shutdown in 5 minutes
sudo shutdown -h +5

# Shutdown at specific time (e.g., 2:30 PM)
sudo shutdown -h 14:30

# Reboot immediately
sudo shutdown -r now

# Reboot in 10 minutes with custom message
sudo shutdown -r +10 "System will reboot for kernel update"

# Cancel a pending shutdown
sudo shutdown -c
```
### Other Shutdown/Reboot Commands
```
# Halt the system
sudo halt
sudo halt -p  # Power off after halting

# Power off
sudo poweroff

# Reboot
sudo reboot

# Reboot forcefully (skips some cleanup)
sudo reboot -f

# Halt with specific message
sudo wall "System going down for maintenance in 5 minutes"
```

---
## 4. Alerting Users Before System Events

### Using wall (write to all users)
```
# Send message to all logged-in users
wall "System will shutdown for maintenance at 2:00 PM. Please save your work."

# Send message before runlevel change
sudo shutdown -r +10 "Rebooting for kernel update" &
sudo wall "System will reboot in 10 minutes for kernel update"
```
### Using shutdown with message
```
# Built-in notification
sudo shutdown -h +15 "System maintenance in 15 minutes - please log out"

# Check who is logged in before sending alerts
who
users
w
```
### Using write command (specific user)
```
# Send message to specific user
write username
This is a test message
^D (Ctrl+D to send)
```

---
## 5. Properly Terminating Processes

### Graceful Process Termination
```
# Send SIGTERM (graceful termination) - default
kill 1234
kill -15 1234

# Send SIGKILL (forceful - last resort)
kill -9 1234

# Kill all processes with specific name
killall firefox
pkill firefox

# Send specific signal to process group
kill -TERM -1234
```
### Runlevel Change Process

When switching runlevels, init/systemd automatically:

1. Sends SIGTERM to processes in the old runlevel
    
2. Waits a few seconds for graceful shutdown
    
3. Sends SIGKILL to any remaining processes
    
4. Starts processes for the new runlevel
    
### View and Manage Processes
```
# View process tree
pstree

# Check process status
ps aux | grep process-name

# List processes by runlevel (SysV)
ls /etc/rc?.d/

# Check systemd service status
systemctl status service-name
```

---
## 6. ACPI (Advanced Configuration and Power Interface)

ACPI handles power management events like:

- Power button presses
    
- Lid closure (laptops)
    
- Battery status
    
- Thermal events

### ACPI Awareness Commands
```
# Check ACPI status
acpi -V

# Check battery status
acpi -b

# Check thermal information
acpi -t

# View ACPI events in real-time
acpi_listen

# Check if ACPI is running
systemctl status acpid
```
### ACPI Configuration
```
# ACPI daemon configuration
/etc/acpi/events/
/etc/acpi/handler.sh

# Systemd handles many ACPI events automatically
/etc/systemd/logind.conf

# Example: Configure power button behavior
# Edit /etc/systemd/logind.conf
HandlePowerKey=poweroff  # or ignore, reboot, halt, suspend, hibernate
```
### Common ACPI Events and Handling
```
# View current power settings
systemd-inhibit --list

# Test ACPI events (as root)
echo -n "button/power PWRF 00000080 00000000" > /proc/acpi/event

# Check log for ACPI events
journalctl -u acpid
dmesg | grep -i acpi
```

---
## Practical Examples

### Complete Maintenance Scenario
```
# 1. Check current state
who
runlevel  # or systemctl get-default

# 2. Alert users
wall "System maintenance in 10 minutes - switching to single-user mode"

# 3. Schedule the change
sudo shutdown -r +10 "Rebooting for maintenance" &

# 4. Or manually change runlevels
sudo init 1  # Switch to single-user mode

# 5. Perform maintenance tasks
fsck /dev/sda1
mount -o remount,ro /

# 6. Return to normal mode
sudo init 5  # or sudo systemctl isolate graphical.target
```
### Emergency Recovery
```
# Boot into rescue mode from GRUB
# Add 'single' or '1' to kernel command line

# Or from running system
sudo systemctl isolate rescue.target

# Emergency shell (minimal environment)
sudo systemctl isolate emergency.target
# Then remount root as read-write if needed
mount -o remount,rw /
```

---
## Key Differences Summary

|Operation|SysV init|systemd|
|---|---|---|
|Set default|Edit /etc/inittab|`systemctl set-default`|
|Change runlevel|`init 3`|`systemctl isolate multi-user.target`|
|View current|`runlevel`|`systemctl get-default`|
|Shutdown|`shutdown -h now`|`shutdown -h now` or `systemctl poweroff`|
|Reboot|`shutdown -r now`|`shutdown -r now` or `systemctl reboot`|
|Single-user|`init 1`|`systemctl isolate rescue.target`|

Remember: Most modern distributions use **systemd**, so focus more on systemd commands while understanding the traditional SysV concepts for compatibility.