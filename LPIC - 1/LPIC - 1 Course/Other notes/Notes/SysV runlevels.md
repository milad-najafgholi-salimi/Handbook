On SysV we were able to define different stages. On a Red Hat-based system we usually had 7:
- 0- Shutdown
- 1- Single-user mode (recovery); Also called S or s
- 2- Multi-user without networking
- 3- Multi-user with networking
- 4- to be customized by the admin
- 5- Multi-user with networking and graphics
- 6- Reboot

And in Debian based system we had:
- 0- Shutdown
- 1- Single-user mode
- 2- Multi-user mode with graphics
- 6- Reboot

In sysV you can change runlevel by `init [runlevel number]` command.
Example:
```
init 3  # Switch to text mode
init 5  # Switch to GUI mode
```