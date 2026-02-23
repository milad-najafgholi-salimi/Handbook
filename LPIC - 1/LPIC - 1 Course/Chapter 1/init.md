`init` (short for **initialization**) is the **first process** that starts when a Linux system boots. It is the parent of all other processes on the system, with a Process ID (PID) of **1**. Its primary job is to start, stop, and manage all other processes and services according to a predefined configuration.

Think of it as the "first manager" or the "ancestor" of everything running on your computer.

You can check the hierarchy of processes using the `pstree` command.

---
- *There are different init systems:*
	- **SysVinit** is based on Unix System V. Not being used much anymore but people loved it because it followed Unix philosophies. you may see it on older machines or even on recently installed ones.
	- **upstart** was an event-based replacement for the traditional init daemon developed by Canonical (The people behind Ubuntu). The goal of the project was to build a replacement for SysV when it got released in 2007. eventually, the project got discontinued due to the wide adoption of Systemd. Even Ubuntu uses Systemd these days, but upstart still can be found in google's ChromeOS.
	- **Systemd** is the new replacement. It is hated by Linux elitists for not following Unix principles but it's widely adopted by major distros. It can
start services in parallel and do lots of fancy stuff!

---
### The Two Eras of `init`

The role of `init` has remained the same, but how it accomplishes its task has changed dramatically over the years.

#### 1. The Classic: **SysVinit** (System V Init)

For decades, most Linux distributions used SysVinit, named after the original Unix System V.

- **How it worked:** It used a series of shell scripts to start services. These scripts were located in directories like `/etc/rc.d/` or `/etc/init.d/`.
    
- **Runlevels:** SysVinit used a concept called **runlevels** (numbered 0 through 6) to define different system states.
    
    - **Runlevel 0:** Halt (shut down the system).
        
    - **Runlevel 1:** Single-user mode (maintenance/rescue mode).
        
    - **Runlevel 3:** Multi-user mode with networking (text-based console).
        
    - **Runlevel 5:** Multi-user mode with networking and a graphical interface (GUI).
        
    - **Runlevel 6:** Reboot.
        
- **Drawbacks:** SysVinit was reliable but **slow and rigid**. It started services one after another in a fixed, linear order, even if they didn't depend on each other. This led to slow boot times.
> **Note:** The designers of the SysVinit system intentionally left runlevels 2 and 4 undefined to provide **maximum flexibility for system administrators**

#### 2. The Modern Standard: **systemd**

Today, the vast majority of major Linux distributions (including Red Hat Enterprise Linux, Fedora, Ubuntu, Debian, and many others) have replaced SysVinit with **systemd**. This is likely what your system uses.

- **Why it was created:** To solve the performance and flexibility problems of SysVinit. It was designed to be faster and to handle modern hardware and software requirements more effectively.
    
- **How it works:** Instead of scripts and runlevels, systemd uses **units**. A unit can be a service (`.service`), a mount point (`.mount`), a socket (`.socket`), a device (`.device`), and more. Units are defined in simple configuration files.
    
- **Parallelization:** systemd's biggest innovation is its ability to start services **in parallel** whenever possible. Instead of waiting for one service to finish starting before starting the next, it identifies dependencies and starts independent services simultaneously, drastically speeding up boot times.
    
- **On-Demand Starting:** systemd can delay the start of a service until it is actually needed. For example, a service that listens for network connections (like a web server) can be started the moment the first connection arrives. This is called socket activation.
    
- **Key Commands:** systemd is managed by the `systemctl` command. This is your primary tool for interacting with the init system.
    
    - `systemctl start [service]` – Start a service.
        
    - `systemctl stop [service]` – Stop a service.
        
    - `systemctl status [service]` – Check if a service is running and see its logs.
        
    - `systemctl enable [service]` – Configure a service to start automatically at boot.
        
    - `systemctl disable [service]` – Prevent a service from starting automatically at boot.
        
    - `systemctl list-units` – List all active units.
        

### The Core Responsibilities of `init`

Whether it's SysVinit or systemd, the `init` process (PID 1) has three fundamental jobs:

1. **Booting the System:** It is the first process started by the kernel. Its initial task is to bring the system to a usable state by mounting filesystems and starting essential services.
    
2. **Process Management:** It acts as the ultimate parent. If a process finishes and its child processes are still running, those "orphaned" child processes are adopted by `init`. It also handles the reaping of zombie processes (processes that have finished executing but still have an entry in the process table).
    
3. **System State Management:** It handles transitions between system states (like shutdown, reboot, single-user mode). When you run `shutdown` or `reboot`, you are ultimately asking `init` to handle that transition.
    

### How to Check Your `init` System

To find out which `init` system your Linux distribution is using, you can run this command in the terminal:
```
ps -p 1
```
This shows the process with PID 1. The output will look something like this:

- **If you see `init`:** Your system is likely using **SysVinit** (or a variant like Upstart).
    
- **If you see `systemd`:** Your system is using **systemd**.
    

In short, `init` (PID 1) is the foundational process that starts and manages everything else. While the classic SysVinit used sequential scripts and runlevels, the modern standard **systemd** uses parallelization and units for a faster, more efficient boot process, and it is managed with the `systemctl` command.
