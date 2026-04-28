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