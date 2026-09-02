**APT** stands for **Advanced Package Tool**.

It’s the **package manager** used by Debian-based Linux systems (like **Ubuntu, Debian, Linux Mint**) to **install, update, and remove software**.

---

Instead of downloading programs from websites, you ask APT and it:

- finds the software
    
- downloads it
    
- installs it
    
- keeps it updated
    
- handles dependencies
    

---

## What APT manages

- Programs (like `git`, `vim`, `curl`)
    
- Libraries those programs need
    
- Updates and security patches
    

---

## Common APT commands

### Install software

`sudo apt install git`

### [[Update package]] list (important!)

`sudo apt update`

### Upgrade installed software

`sudo apt upgrade`

### Remove software

`sudo apt remove git`

---

## Where APT gets software from

APT downloads packages from **repositories** defined in:

- `/etc/apt/sources.list`
    
- `/etc/apt/sources.list.d/`
    

These are **trusted servers** maintained by your Linux distribution.

---

## What problem APT solves

Without APT, you would have to:

- download software manually
    
- install dependencies yourself
    
- update everything one by one
    

APT automates all of that.

---

## APT vs other package managers

|OS / Distro|Package manager|
|---|---|
|Ubuntu / Debian|APT|
|Fedora / RHEL|DNF / YUM|
|Arch Linux|pacman|
|macOS|Homebrew|
|Windows|winget / chocolatey|

---

## What APT is NOT

- Not a programming language
    
- Not Git
    
- Not a compiler
    
