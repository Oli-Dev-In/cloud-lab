# Linux Filesystem Structure

## Core concept

In Linux, everything starts from `/` — the root of the filesystem. Unlike Windows which uses separate drive letters (`C:\`, `D:\`), Linux has a single tree starting from `/`. Everything — disks, devices, system files, user folders — is accessible from this single root.

A fundamental Linux philosophy: **everything is a file**. Hardware devices, system state, configuration — all represented as files.

## Essential commands

### pwd
Print Working Directory. Displays the full path of your current location in the filesystem. First reflex when lost in a terminal.

```bash
olivier@ubuntu-server-01:~$ pwd
/home/olivier
```

### ls
List — displays the contents of a directory.

```bash
olivier@ubuntu-server-01:~$ ls /
bin   cdrom  etc   lib    lost+found  mnt  proc  run   snap  sys  usr
boot  dev    home  lib64  media       opt  root  sbin  srv   tmp  var
```

`ls /` asks Linux to list all folders at the root of the filesystem.

### ~
Shortcut representing your personal home directory. For user olivier, `~` is equivalent to `/home/olivier`. Usable in any command.

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