`systemd` is a **system and service manager** for Linux operating systems. It is currently the standard `init` system (the first process started at boot, with PID 1) for the vast majority of major Linux distributions, including Red Hat Enterprise Linux, Fedora, Ubuntu, Debian, SUSE, and many others.

However, calling it just an `init` system is an understatement. `systemd` is more accurately described as a comprehensive **suite of software** that provides a wide range of system components for a modern Linux system.

---
The **systemd** is made around **units**. A unit can be a service, group of services, or an action. Units do have a name, a type, and a configuration file.
There are 12 unit types: 
- automount, device, mount, path, scope, service, slice, snapshot, socket, swap, target & timer.

We use `systemctl` to work with these units and `journalctl` to see the logs.

The units can be found in these places (sorted by priority):
1. `/etc/systemd/system/`
2. `/run/systemd/system/`
3. `/usr/lib/systemd/system`

```
systemctl list-unit-files
systemctl cat ntpd.service
systemctl cat graphical.target
```
We can use these commands to work with services:
```
# systemctl stop sshd
# systemctl start sshd
# systemctl status sshd
# systemctl is-active sshd
# systemctl is-failed sshd
# systemctl restart sshd
# systemctl reload sshd # re-reads the configuration of the service configs
# systemctl daemon-reload sshd # re-reads the configuration of the systemd configs of this service
# systemctl enable sshd
# systemctl disable sshd
```
there are other commands too:
```
# systemctl is-system-running # running, degraded, maintenance, initializing, starting, stopping
# systemctl --failed
```
to check the logs, we have to use the `journalctl` utility - (see [[journalctl]]):
```
# journalctl # show all journal
# journalctl --no-pager # do not use less
# journalctl -n 10 # only 10 lines
# journalctl -S -1d # last 1 day
# journalctl -xe # last few logs
# journalctl -u ntp # only ntp unit
# journalctl _PID=1234
```
#### SysV
`SysV` is the older init system. Still can be used on many systems. The control files are located at `/etc/init.d/` and are closer to the general bash scripts.
In many cases you can call like:
```
/etc/init.d/ntpd status
/etc/init.d/ntpd stop
/etc/init.d/ntpd start
/etc/init.d/ntpd restart
```

---
### The Core Philosophy

`systemd` was created to address the limitations of the older SysVinit system. Its primary goals were to:

- **Be Faster:** Boot the system by starting services **in parallel**, rather than one after another.
    
- **Be Cleaner:** Use a unified, declarative configuration system instead of complex shell scripts.
    
- **Be More Dynamic:** Handle modern hardware like hot-pluggable devices and manage dependencies between services intelligently.
    
- **Centralize Management:** Provide a single, consistent interface (`systemctl`) to manage services, logs, system state, and more.

---
### Key Concepts: Units and Targets

`systemd` manages system resources using **units**.

#### What is a Unit?

A unit is a resource that `systemd` knows how to manage. Each unit is defined in a simple plain-text file (a `.service` file, a `.socket` file, etc.). The most important unit types are:

- **Service units (`.service`):** Represent a system service (like a web server, database, or SSH daemon). This is the most common unit type.
    
- **Target units (`.target`):** Group other units together to represent a particular system state (like `multi-user.target` for a text-mode system or `graphical.target` for a system with a GUI). These are conceptually similar to "runlevels" in SysVinit but are more flexible.
    
- **Socket units (`.socket`):** Represent a socket (like an IPC or network socket). `systemd` can listen on a socket and start the associated service only when a connection arrives. This is called **socket activation**.
    
- **Mount units (`.mount`):** Define mount points for filesystems.
    
- **Timer units (`.timer`):** Act as a replacement for `cron` jobs. They can trigger the execution of other units on a schedule or at specific times.
    

#### What is a Target?

A target is a special unit that groups other units. Instead of runlevels (0-6), `systemd` uses targets.

- `poweroff.target` (runlevel 0)
    
- `rescue.target` (runlevel 1)
    
- `multi-user.target` (runlevel 3) – A multi-user, non-graphical system.
    
- `graphical.target` (runlevel 5) – A multi-user system with a graphical login.
    
- `reboot.target` (runlevel 6)

>**Note:** runlevels 2 and 4 undefined to provide **maximum flexibility for system administrators**

---
### Key Features and Components

`systemd` is an umbrella project that includes many components, making it a complete system management layer.

- **`systemctl` (The Control Tool):** This is the primary command-line interface to manage `systemd`. You use it to start, stop, enable, disable, and check the status of services and other units.
```
systemctl start sshd.service   # Start the SSH service
systemctl enable sshd.service  # Make it start at boot
systemctl status sshd.service  # Check if it's running
systemctl list-units           # List all active units
systemctl isolate graphical.target # Switch to graphical mode
```
- **`journald` (The Logging Daemon):** `systemd` includes its own logging system. It collects log messages from the kernel, services, and applications in a structured, indexed, binary format.
    
    - You view these logs with the **`journalctl`** command. ([[journalctl| see here]])
        
    - This centralizes all logs and makes them incredibly searchable.
        
- **`logind` (The Login Manager):** Manages user logins, sessions, and seats. It handles things like:
    
    - Launching user sessions.
        
    - Managing permissions for devices (e.g., allowing a user to suspend the system if they are logged in locally).
        
    - Handling `multiseat` configurations (multiple independent user stations on one computer).
        
- **`networkd` (The Network Manager):** A network configuration daemon that can handle complex network setups. It's often used in server environments or containers for its speed and simplicity.
    
- **`resolved` (The DNS Resolver):** A daemon to manage DNS resolution. It can act as a local DNS cache and supports DNSSEC for security.
    
- **`timedated` (The Time Manager):** Manages system time and timezone settings.
    
- **`udev` (The Device Manager):** `systemd` incorporated `udev`, the device manager that handles hot-pluggable hardware. It dynamically creates device nodes in `/dev` and runs rules when devices are added or removed.
    

### ✅ Advantages of `systemd`

- **Speed:** Parallel startup makes boot times significantly faster.
    
- **Consistency:** A single, unified set of tools and interfaces for managing the entire system.
    
- **Standardization:** Provides a common standard across different Linux distributions, making system administration skills more portable.
    
- **Powerful Features:** Socket activation, on-demand service starting, and robust logging with `journald`.
    
- **Dependency Management:** Clearly defined and resolved dependencies between services ensure they start in the correct order.
    

### ❌ Criticisms of `systemd`

`systemd` has not been without controversy. Some of the common criticisms include:

- **Violation of Unix Philosophy:** Critics argue that it violates the classic Unix principle of "do one thing and do it well" by becoming a massive, monolithic suite of software that handles too many things.
    
- **Complexity:** It is seen as overly complex compared to the relatively simple shell scripts of SysVinit.
    
- **"Linuxification":** Some argue that it is deeply tied to Linux and makes it harder to port software to other Unix-like systems (like the BSDs).
    
- **Logging Format:** The binary format of `journald` logs is controversial because it's not easily readable by traditional Unix text-processing tools (though `journalctl` and tools like `less` can read them, and output can be piped).
    

Despite the controversy, `systemd` is now deeply embedded in the Linux ecosystem. Most major distributions have adopted it, and for better or worse, learning to work with `systemd` and its tool `systemctl` is an essential skill for modern Linux system administration.