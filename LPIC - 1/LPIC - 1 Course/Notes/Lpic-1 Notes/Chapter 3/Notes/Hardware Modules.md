The Linux kernel needs device drivers to communicate with the hardware devices installed on your Linux system. However, compiling device drivers for all known hardware devices into the kernel would make for an extremely large kernel binary file.

To avoid that situation, the Linux kernel uses kernel *modules*, which are individual hardware driver files that can be linked into the kernel at runtime. That way, the system can link only the modules needed for the hardware present on your system.

If the kernel is configured to load hardware device modules, the individual module files must be available on the system as well. If you’re compiling a new Linux kernel, you’ll also need to compile any hardware modules along with the new kernel.

Module files may be distributed either as source code that needs to be compiled or as binary object files on the Linux system that are ready to be dynamically linked to the main kernel binary program. If the module files are distributed as course code files, you must compile them to create the binary object file. The `.ko` file extension is used to identify the module object files.

The standard location for storing module object files is in the `/lib/modules` directory. This is where the Linux module utilities (such as `insmod` and `modprobe`) look for module object library files by default.

Each kernel has its own directory for its own modules (such as `/lib/modules/4.3.3`), allowing you to create separate modules for each kernel version on the system if needed.

The modules the kernel will load at boot time are listed in the `/etc/modules` file, one per line. Most hardware modules can be loaded dynamically as the system automatically detects hardware devices, so this file may not contain very many modules.

If needed, you can customize a kernel module to define unique parameters required, such as hardware settings required for the device to operate. The kernel module configurations are stored in the `/etc/modules.conf` configuration file.

Finally, some modules may depend on other modules being loaded first to operate properly. These relationships are defined in the `modules.dep `file, stored in the `/lib/modules/version/` directory, where version is the kernel version. The format for each entry is:
```
modulefilename: dependencyfilename1 dependencyfilename2 ...
```

When you use the `modules_install` target to install the modules, it calls the `depmod` utility, which determines the module dependencies and generates the `modules.dep` file automatically. If you modify or add any modules after that, you must manually run the `depmod` command to update the `modules.dep` file.

