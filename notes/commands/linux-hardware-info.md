# Linux Hardware Info Commands

## uname
Displays system information — kernel version, architecture, hostname.

```bash
# Display kernel version only
uname -r
# → 7.0.0-14-generic

# Display all system information
uname -a
```

**uname -r output breakdown:**
```
7.0.0-14-generic
│ │ │  │
│ │ │  └── Distro specific info
│ │ └───── Patch release
│ └─────── Minor version
└───────── Kernel version
```

**Note**: `uname -r` shows the **kernel** version, not the OS version. The OS is Ubuntu — the kernel is the underlying Linux version it runs on.

## dmesg
Displays the kernel ring buffer — all messages logged by the kernel since boot. Essential for hardware diagnostics, bug resolution, and tracing the boot sequence.

```bash
# Display all kernel messages
dmesg

# Filter for USB messages
dmesg | grep -i usb

# Filter for disk messages
dmesg | grep -i sda

# Display with timestamps
dmesg -T

# Show only errors and warnings
dmesg --level=err,warn
```

**Professional use**: when a USB device or disk is not recognized, `dmesg | grep -i usb` shows exactly what the kernel saw when the device was plugged in.

## udevadm
Queries and monitors events from udev — the Linux device manager. udev handles device detection and creates entries in `/dev` when hardware is connected.

```bash
# Query information about a specific device
udevadm info --query=path --name=/dev/sda

# Monitor device events in real time
udevadm monitor
```

**udevadm monitor** shows two types of events:
- `KERNEL` — raw kernel uevent
- `UDEV` — processed event after udev rule application

**Professional use**: `udevadm monitor` while plugging in a USB device shows exactly what the kernel detects and how udev responds in real time.

## lspci
Lists all PCI devices configured on the system — network cards, graphics cards, USB controllers, storage controllers.

```bash
# List all PCI devices
lspci

# Verbose output with more details
lspci -v

# Filter for a specific device type
lspci | grep -i network
lspci | grep -i usb
```

## lsblk
Lists information about block devices — hard drives, SSDs, partitions, and their mount points.

```bash
# List all block devices
lsblk

# List with filesystem type
lsblk -f
```

**Output columns:**
| Column | Meaning |
|---|---|
| NAME | Device name |
| MAJ:MIN | Major and minor device numbers |
| RM | Removable device (1=yes) |
| SIZE | Device size |
| RO | Read-only (1=yes) |
| TYPE | disk, part (partition), rom |
| MOUNTPOINT | Where the device is mounted |

## lscpu
Displays detailed CPU information — architecture, cores, threads, speed, cache.

```bash
lscpu
```

Shows: architecture, CPU cores, threads per core, CPU speed, cache sizes, virtualization support.

## lsmem
Displays memory (RAM) information — total size, online/offline blocks.

```bash
lsmem

# Summary only
lsmem --summary
```

## free
Displays RAM and swap usage statistics — total, used, free, shared, cached.

```bash
# Display in megabytes
free -m

# Display in kilobytes
free -k

# Display in gigabytes
free -g

# Human readable (auto unit)
free -h
```

**Output columns:**
| Column | Meaning |
|---|---|
| total | Total installed memory |
| used | Memory currently in use |
| free | Completely unused memory |
| shared | Memory used by tmpfs |
| buff/cache | Memory used for buffers and cache |
| available | Memory available for new processes |

**Note**: `free` does not available mean the same as `free`. Linux uses unused RAM for cache — `available` is the real number of memory a new program can use.

## lshw
Lists complete hardware configuration of the system — CPU, memory, storage, network, all peripherals.

```bash
# Full hardware listing (requires sudo for complete info)
sudo lshw

# Short summary format
sudo lshw -short

# Filter for a specific class
sudo lshw -class network
sudo lshw -class disk
sudo lshw -class memory
```