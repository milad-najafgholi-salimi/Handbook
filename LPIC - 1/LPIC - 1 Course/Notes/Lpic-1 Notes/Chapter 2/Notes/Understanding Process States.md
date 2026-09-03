Processes that are swapped into virtual memory are called *sleeping*. Often the Linux kernel places a process into sleep mode while the process is waiting for an event.

When the event triggers, the kernel sends the process a signal. If the process is in **interruptible sleep** mode, it will receive the signal immediately and wake up. If the process is in **uninterruptible sleep** mode, it only wakes up based on an external event, such as hardware becoming available. It will save any other signals sent while it was sleeping and act on them once it wakes up.

If a process has ended but its parent process hasn’t acknowledged the termination signal because it’s sleeping, the process is considered a *zombie*. It’s stuck in a limbo state between running and terminating until the parent process acknowledges the termination signal.
