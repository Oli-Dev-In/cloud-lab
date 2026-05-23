# Linux Package Management

## What is a Package

A package is a compressed archive containing all the files necessary for specific software to run — binaries, supporting files, configuration files, and metadata including dependencies list.

A **dependency** is a program or library that must be present for the software to function correctly. Without it, installation fails.

## Two Families of Linux Distributions

Linux distributions are categorized by their package management system. The two main families are not compatible with each other — a `.deb` package cannot be installed directly on an RPM-based system and vice versa.

| Family | Package format | Distributions |
|---|---|---|
| Debian-based | `.deb` | Ubuntu, Debian, Linux Mint, elementary OS |
| RPM-based | `.rpm` | RHEL, CentOS, Fedora |

## What is a Package Manager

A package manager automates installation, upgrade, configuration, and removal of software packages. Key functions:

- Verifies package integrity and authenticity via digital certificates and checksums
- Resolves dependencies automatically — installs all required components
- Manages software repositories — remote or local sources of packages
- Prevents "dependency hell" — the nightmare of manually resolving chains of dependencies

## Package Manager Hierarchy

Both families have two layers — a low-level tool that handles individual packages, and a high-level tool that adds dependency resolution and repository management.

| Layer | Debian-based | RPM-based |
|---|---|---|
| Low-level (no dependency resolution) | DPKG | RPM |
| High-level (with dependency resolution) | APT | YUM / DNF |

**Professional rule**: always use the high-level tool (APT or YUM) — it handles dependencies automatically. Use the low-level tool (DPKG or RPM) only when installing a manually downloaded package file.

## Repositories

Repositories are structured collections of packages hosted on servers. Package managers connect to repositories to find and download software.

**Debian-based repository configuration:**
```bash
/etc/apt/sources.list        # main repository sources file
/etc/apt/sources.list.d/     # additional repository files
```

**RPM-based repository configuration:**
```bash
/etc/yum.repos.d/            # directory containing .repo files
```

## APT vs APT-GET

Both manage packages on Debian-based systems. APT is the modern replacement for APT-GET.

| | APT | APT-GET |
|---|---|---|
| Output | Clean, with progress bars | Functional but verbose |
| Search | `apt search package` | Requires separate `apt-cache search` |
| Professional use | Current standard | Legacy — still works but not preferred |

**Use APT** for all daily package management. APT-GET still works but APT is cleaner and more intuitive.