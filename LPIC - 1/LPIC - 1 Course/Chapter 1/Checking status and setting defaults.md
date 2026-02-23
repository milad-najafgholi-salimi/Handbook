You can check your current runlevel with `runlevel` command. It comes from **SysV** era but still works on **systemd** systems. The default was in
`/etc/inittab` .
It can also be done on grub kernel parameters.
Or using the `runlevel` and `telinit` command.
```
# runlevel
N 3
# telinit 5
# runlevel
3 5
# init 0 # shutdown the system
```
You can find the files in `/etc/init.d` and runlevels in `/etc/rc[0-6].d` directories where S indicates Start and K indicates Kill.
On systemd, you can find the configs in:
`/etc/systemd`
`/usr/lib/systemd/`
