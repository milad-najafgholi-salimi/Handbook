`journalctl` is a command-line tool for viewing and analyzing logs collected by the `systemd` journal, which is the logging system on most modern Linux distributions. Think of it as a powerful, searchable, and centralized replacement for traditional, scattered log files.

In addition to these, most systems keep the boot logs in a text-like file too and they can be found in /var/log/boot or /var/log/boot.log in Debian
or Red-Hat based systems, respectively.

---
### What Makes `journalctl` Special?

Unlike older logging systems that store logs as plain text in various files under `/var/log/`, the `systemd` journal stores log data in a structured, indexed, binary format. This structure is what makes `journalctl` so powerful. It allows you to:
- **Filter logs with incredible precision:** You can quickly display logs from a specific service, a particular boot session, a time window, or a priority level (like only errors)
- **View logs in real-time:** Monitor live system activity as it happens, similar to `tail -f`.
- **Access rich metadata:** Each log entry includes fields like the process ID, user ID, and more, which can be used for advanced filtering.

---
### Common `journalctl` Commands and How to Use Them

Here is a practical guide to some of the most useful `journalctl` commands. Many of these can be combined for more precise log analysis.

| Command                                        | Description                                                                                                                           | Example                              |
| ---------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------ |
| **`journalctl`**                               | Shows all logs from the oldest to the newest, opened in a pager (usually `less`)                                                      | `journalctl`                         |
| **`journalctl -r`**                            | Shows logs in reverse chronological order (newest first)                                                                              | `journalctl -r`                      |
| **`journalctl -f`**                            | **Follow** or tail logs in real-time, showing new entries as they are written. Press `Ctrl+C` to exit                                 | `journalctl -f`                      |
| **`journalctl -n N`**                          | Shows only the last `N` lines (e.g., the last 50 lines)                                                                               | `journalctl -n 50`                   |
| **`journalctl -u [SERVICE]`**                  | Shows logs for a specific **unit** (service), like `sshd`, `nginx`, or `docker`                                                       | `journalctl -u ssh`                  |
| **`journalctl -k`**                            | Shows only **kernel** messages, similar to the `dmesg` command                                                                        | `journalctl -k`                      |
| **`journalctl -p [PRIORITY]`**                 | Filters by message **priority** or log level (e.g., `err`, `warning`, `info`, `debug`)                                                | `journalctl -p err`                  |
| **`journalctl -b [OFFSET]`**                   | Shows logs from the current **boot**. Use `-b -1` for the previous boot, `-b -2` for the one before that, etc.                        | `journalctl -b -1`                   |
| **`journalctl --since [TIME] --until [TIME]`** | Shows logs within a specific **time range**. Times can be absolute (`"2024-05-01 10:00"`) or relative (`"1 hour ago"`, `"yesterday"`) | `journalctl --since "1 hour ago"`    |
| **`journalctl -g [PATTERN]`**                  | **Grep** the logs for a specific pattern or regular expression                                                                        | `journalctl -g "error\|failed"`      |
| **`journalctl --disk-usage`**                  | Shows the total disk space currently used by the journal files                                                                        | `journalctl --disk-usage`            |
| **`journalctl --vacuum-size=SIZE`**            | Reduces disk usage by removing the oldest logs until the journal's total size is below the specified `SIZE` (e.g., `1G`)              | `sudo journalctl --vacuum-size=500M` |

---
### Putting It All Together: Real-World Examples
The real power of `journalctl` lies in combining its options. Here are some common troubleshooting scenarios:

- **A service won't start:** To see only the errors from the last boot for the `nginx` service, you can use:
```
journalctl -u nginx -b -p err
```
- **The system crashed on the last boot:** To investigate critical messages from the previous boot, the following command is helpful:
```
journalctl -b -1 -p crit
```
- **An application is acting up right now:** To watch logs for two related services in real-time, use:
```
journalctl -u nginx -u myapp -f
```
- **You need to send logs to a developer:** For exporting logs from a specific time window to a text file, you can redirect the output:
```
journalctl --since "2 hours ago" --until "1 hour ago" > /tmp/problem_logs.txt
```

---
### Configuration and Persistence

By default, on some systems, the journal may store logs only in memory (`/run/log/journal/`), meaning they are lost when you reboot. To keep logs for long-term analysis and to be able to look at previous boots with `journalctl -b -1`, you need to enable **persistent storage**.

To enable persistent logging, follow these steps:

1. **Create the directory** where logs will be stored persistently:
```
sudo mkdir -p /var/log/journal
```
2. **Restart the journal service** to apply the change:
```
sudo systemctl restart systemd-journald
```
After this, logs will be saved to disk and survive reboots.
