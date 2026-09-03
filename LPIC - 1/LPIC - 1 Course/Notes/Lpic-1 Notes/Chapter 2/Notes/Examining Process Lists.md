At any given time lots of active programs are running on the Linux system. Linux calls each running program a *process*. The Linux system assigns each process a **process ID** (*PID*) and manages how the process uses memory and CPU time based on that *PID*.

When a Linux system first boots, it starts a special process called the **init process**.
The *init* process is the core of the Linux system; it runs scripts that start all of the other processes running on the system, including the processes that start the text consoles and graphical windows you use to log in (see Chapter 5).

