# Linux Filesystem Structure

## Core concept

In Linux, everything starts from `/` — the root of the filesystem. Unlike Windows which uses separate drive letters (`C:\`, `D:\`), Linux has a single tree starting from `/`. Everything — disks, devices, system files, user folders — is accessible from this single root.

A fundamental Linux philosophy: **everything is a file**. Hardware devices, system state, configuration — all represented as files.

## The prompt

The terminal prompt gives you four pieces of information at a glance:

```bash
olivier@ubuntu-server-01:/etc$
```

| Element | Meaning |
|---|---|
| `olivier` | Current logged-in user |
| `@` | Separator — "at" |
| `ubuntu-server-01` | Hostname of the server you are working on |
| `:/etc` | Current directory — where you are in the filesystem |
| `~` | Special shortcut for home directory — when shown in prompt means you are in `/home/olivier` |
| `/` | Root of the filesystem — when shown in prompt means you are at the top of the Linux directory tree |
| `$` | Normal user with limited rights |
| `#` | Root user — absolute administrator with full system rights. Always check this symbol before running powerful commands. |

## File Types in Linux

Linux has seven file types. The type is shown as the first character in `ls -l` output.

| Identifier | Type | Description |
|---|---|---|
| `-` | Regular file | Standard files — text, images, scripts, binaries, config files |
| `d` | Directory | A folder containing other files and directories |
| `c` | Character device | Hardware devices that transfer data character by character — keyboards, terminals |
| `b` | Block device | Hardware devices that transfer data in blocks — hard drives, SSDs |
| `l` | Symbolic link (symlink) | A pointer to another file or directory |
| `s` | Socket file | Used for inter-process communication over a network |
| `p` | Named pipe | Used for inter-process communication on the same machine |

**Identify file type with `file` command:**
```bash
file /home/olivier/          # → directory
file script.sh               # → Bourne-Again shell script
file /dev/sda                # → block special
file insync.sock             # → socket
file link-to-script          # → symbolic link to /home/sara/script.sh
```

**Identify file type with `ls -l`:**
```bash
ls -l /dev/sda
# brw-rw---- 1 root disk 8, 0 Apr 25 20:40 /dev/sda
# ^ first character 'b' = block device
```

## Key directories

### /home
Personal folders for all system users. `/home/olivier` is my personal directory — equivalent of `C:\Users\ol1wo` on Windows.

### /etc
Contains all system configuration files — SSH, network, services. Frequently visited when managing a server.

### /var
Short for "variable". Contains data that changes constantly — system logs, databases, temporary service files. When something breaks, check `/var/log` first.

### /usr
Short for "User System Resources". Contains installed programs and libraries. Most commands used daily come from `/usr/bin`.

### /bin and /sbin
Essential system commands. `ls`, `pwd`, `cd` live here.

### /tmp
Temporary files. Cleared on every reboot.

### /proc
Not a real folder — an interface to the Linux kernel. Reading files here gives real-time system state information.

### /dev
Short for "devices". All hardware devices are represented as files here. The hard drive is `/dev/sda`. This is the Linux philosophy in practice: **everything is a file**.

### /root
Home directory for the root user specifically. Separate from /home — the root user does not have a directory under /home.

### /opt
Third-party software and applications are installed here. If you deploy an application like a web server or monitoring agent manually, /opt is the standard location.

### /mnt
Temporary mount point for filesystems. When you mount a network share, an external disk, or a repository temporarily, /mnt is the conventional location. Unmount when done.

### /media
External media is automatically mounted here. USB drives, DVDs, and other removable storage appear under /media when plugged in — equivalent of drive letters (G:, H:) on Windows.

### /lib and /lib64
Shared libraries required by programs at runtime. Similar to .dll files on Windows. Programs in /bin and /usr/bin depend on libraries stored here.