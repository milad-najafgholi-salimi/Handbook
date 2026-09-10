Although there were plenty of limitations with **BIOS**, computer manufacturers learned to live with them, and **BIOS** became the default standard for IBM compatible systems for many years. However, as operating systems became more complicated, it eventually became clear that a new boot method needed to be developed.

Intel created the *Extensible Firmware Interface* (**EFI**) in 1998 to address some of the limitations of BIOS. It was somewhat of a slow process, but by 2005, the idea caught on with other vendors, and the *Unified EFI* (**UEFI**) specification was adopted as a standard.

These days just about all IBM-compatible desktop and server systems utilize the **UEFI** firmware standard.

Instead of relying on a single boot sector on a hard drive to hold the *boot loader* program, **UEFI** specifies a special disk partition, called the *EFI System Partition* (**ESP**), to store *boot loader* programs. This allows for any size of *boot loader* program, plus the ability to store multiple *boot loader* programs for multiple operating systems.

The **ESP** setup utilizes the old Microsoft **File Allocation Table** (*FAT*) filesystem to store the *boot loader* programs. On Linux systems, the **ESP** is typically mounted in the `/boot/efi` directory, and the *boot loader* files are typically stored using the `.efi` filename extension, such as `linux.efi`.

The **UEFI** firmware utilizes a built-in mini boot loader (sometimes referred to as a *boot manager*) that allows you to configure which *boot loader* program file to launch.

![pic-2](Pics/2.png)

With **UEFI** you need to register each individual boot loader file you want to appear at boot time in the *boot manager interface menu*. You can then select the boot loader to run each time you boot the system.

After the firmware finds and runs the boot loader, its job is done. The boot loader step in the boot process can be somewhat complicated; the next section dives into covering that.
