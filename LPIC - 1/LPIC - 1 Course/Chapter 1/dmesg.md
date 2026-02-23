Linux will show you the boot process logs during the boot. Some desktop systems hide this behind a fancy splash screen which you can hide
using the Esc key or press Ctrl+Alt+F1.

due to several reasons, the kernel saves it's own logs into the "Kernel Ring Buffer". after the compilation of the boot process, the syslog daemon collects the *boot logs* and stores them in `/var/log/dmesg`.

to view all the logs including what has been logged after the boot process we use the `dmesg` command.

---
### What is `dmesg`?

`dmesg` (short for **display message** or **driver message**) is a command on Linux and other Unix-like operating systems that prints the message buffer of the kernel. The kernel is the core of the operating system, and it communicates with the user through this buffer during system operations, especially at boot time.

Think of it as the kernel's logbook. It records every event it deems important, from the moment the system powers on.

### What Kind of Information Does It Show?

The `dmesg` output is a stream of text messages. You'll typically find information about:

- **Hardware Detection:** When the kernel discovers hardware components like the CPU, RAM, hard drives (SATA, NVMe), PCIe devices, and USB devices.
    
- **Device Drivers:** Messages from drivers as they initialize and bind to hardware. For example, you'll see the graphics driver (like `i915` for Intel or `nvidia` for NVIDIA) initializing, or the network driver bringing up an interface (`eth0`, `wlan0`).
    
- **Kernel Modules:** Information about kernel modules being loaded and unloaded.
    
- **Boot Process:** A detailed, step-by-step log of the system booting up, including mounting filesystems, starting services, and checking disk integrity.
    
- **Errors and Warnings:** Crucial for troubleshooting. `dmesg` will show hardware failures, disk errors, USB malfunctions, and other system-level problems. For example, if a hard drive is failing, you might see I/O errors in the `dmesg` output.
    
- **Filesystem Messages:** Information about mounting and unmounting drives, checking filesystems, and any filesystem-related errors.
    

### Why is `dmesg` Useful? (Common Use Cases)

1. **Troubleshooting Hardware Issues:** If a new piece of hardware isn't working, `dmesg` is the first place to look. The error messages will often tell you exactly why the driver failed to load.
    
2. **Diagnosing Boot Problems:** If your system hangs or crashes during boot, you can often view the `dmesg` log from a recovery console to see the last few messages before the failure.
    
3. **Checking for System Errors:** You can periodically check `dmesg` for hardware errors like disk problems or USB resets that might indicate a developing issue.
    
4. **Identifying Connected Devices:** You can use it to see how the kernel has identified a newly plugged-in USB drive (e.g., as `/dev/sdb1`).
    

### How to Use the `dmesg` Command

The basic syntax is simply `dmesg` in a terminal, but this often produces a huge amount of text. Here are the most useful options with examples:

- **`dmesg | less`** : The output is often too long to fit on one screen. Piping it to `less` (or `more`) allows you to scroll through it page by page.
```
dmesg | less
```
**`dmesg | grep [search_term]`** : This is the most powerful way to use `dmesg`. You can filter the output to find specific information.

- To find information about a USB drive:
```
dmesg | grep -i usb
```
- To see what the kernel thinks about your SATA drives:
```
dmesg | grep -i sata
```
- To look for errors (case-insensitive):
```
dmesg | grep -i error
```
- To find out what your network card is doing:
```
dmesg | grep -i eth
```
or
```
dmesg | grep -i wlan
```
- **`dmesg -H`** : Provides human-readable output with timestamps and color-coding, making it easier to read.
```
dmesg -H
```
- **`dmesg -T`** : Prints human-readable timestamps. By default, `dmesg` shows the time since the kernel started. The `-T` flag converts this to a standard date and time, which is very helpful for correlating kernel events with other system logs.
```
dmesg -T
```
- **`dmesg -w`** : This follows the output in real-time, similar to `tail -f`. New kernel messages will appear on your screen as they are generated. This is great for watching what happens when you plug in a new device.
```
dmesg -w
```
- _(Press `Ctrl+C` to exit.)_
    
- **`dmesg --level=`** : Filter messages by their log level (e.g., `err`, `warn`, `info`). This helps you focus on critical messages.
```
dmesg --level=err,warn
```

---
## Summary
In short, `dmesg` is an essential tool for any Linux user or administrator who needs to understand what their system is doing at the lowest level and, more importantly, why it might be failing.