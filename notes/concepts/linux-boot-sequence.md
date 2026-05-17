# Linux Boot Sequence

## Overview

The Linux boot process has four sequential stages. Each stage must complete successfully before the next begins.

```
BIOS POST → Boot Loader (GRUB2) → Kernel Initialization → Service Initialization (systemd)
```

## Stage 1 — BIOS POST

**BIOS** (Basic Input/Output System) runs a **POST** (Power-On Self-Test) — a hardware check to confirm all components are functioning correctly. This stage is independent of Linux. If POST fails, the system cannot proceed.

## Stage 2 — Boot Loader (GRUB2)

After a successful POST, the BIOS loads the boot code from the first sector of the boot device (located in `/boot`). The boot loader displays a boot menu — in a dual-boot setup you choose between operating systems here.

The boot loader then loads the Linux kernel into memory and passes control to it.

**GRUB2** (Grand Unified Boot Loader Version 2) is the standard boot loader for most Linux distributions.

## Stage 3 — Kernel Initialization

The kernel is stored in compressed format and is decompressed into memory. It then:
- Initializes hardware
- Sets up memory management
- Loads necessary device drivers
- Searches for an INIT process to start user space

Boot messages during this stage are visible in `dmesg`.

## Stage 4 — Service Initialization (systemd)

Modern Linux distributions use **systemd** as the INIT process. systemd is responsible for:
- Mounting filesystems
- Starting system services in parallel (faster boot than older SYSV-INIT)
- Bringing the system to its configured target (runlevel)

```bash
# Verify that systemd is the INIT process
ls -l /sbin/init
# → lrwxrwxrwx /sbin/init -> /lib/systemd/systemd
```

## Runlevels and Systemd Targets

Runlevels define the operational state of the system — which services run and what mode the system boots into. Modern Linux uses systemd **targets** instead of traditional runlevels.

| Old Runlevel | Systemd Target | Description |
|---|---|---|
| 3 | `multi-user.target` | Command line interface only — no GUI. Standard for servers. |
| 5 | `graphical.target` | Full graphical interface. Standard for desktops. |

**Servers always run at runlevel 3 / multi-user.target** — no graphical interface needed, fewer resources used.

```bash
# Check current runlevel
runlevel

# Check current default systemd target
systemctl get-default

# Change default target to command line (server mode)
sudo systemctl set-default multi-user.target

# Change default target to graphical (desktop mode)
sudo systemctl set-default graphical.target
```

**Note**: changes to the default target take effect on the next reboot.