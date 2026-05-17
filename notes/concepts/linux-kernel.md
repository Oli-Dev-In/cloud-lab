# Linux Kernel

## What is the Linux Kernel

The kernel is the primary component of an operating system — the core interface between computer hardware and application processes. Applications never communicate directly with hardware. They always go through the kernel via system calls.

**Analogy**: the kernel is like a librarian in a library. The library is the OS, the books are hardware resources, the students are application processes. Without the librarian (kernel), students (processes) would grab resources haphazardly. The librarian manages allocation, tracks usage, and ensures orderly operation.

## Four Core Functions

| Function | Description |
|---|---|
| Memory Management | Tracks memory usage and allocation across all processes |
| Process Management | Schedules processes on the CPU and determines execution order |
| Device Drivers | Acts as intermediary between hardware devices and software processes |
| System Calls and Security | Handles requests from processes and enforces security policies |

## Monolithic but Modular

The Linux kernel is **monolithic** — it handles CPU scheduling, memory management, and other operations within a single large binary running in kernel space.

But it is designed to be **modular** — it can be extended dynamically via kernel modules without recompiling or rebooting the entire kernel. This is how device drivers are loaded on demand.

## Kernel Space vs User Space

The kernel divides memory into two areas:

**Kernel Space**
- Reserved exclusively for the kernel and its critical services
- Has complete, unrestricted access to all hardware resources
- Where device drivers, kernel code, and kernel extensions run

**User Space**
- Where all user applications run — Python, Java, Docker containers, shell scripts
- Has restricted access to hardware — cannot access it directly
- Communicates with the kernel via **system calls**

```
Hardware
    ↑
Kernel Space  ← kernel code, device drivers
    ↑ system calls
User Space    ← applications, programs, shells
```

## System Calls

System calls are the secure interface through which user space programs request services from the kernel. When a program needs to access hardware or system resources, it makes a system call.

Examples of system calls:
- `open()` — open a file
- `read()` — read file content
- `write()` — write to a file
- `getpid()` — get current process ID
- `close()` — close a file

```bash
# When you run this command:
cat /etc/os-release
# The cat program makes system calls: open(), readdir(), close()
# The kernel handles the actual file access
```

## Checking Kernel Version

```bash
# Display kernel version
uname -r
# → 7.0.0-14-generic

# Display all system information
uname -a
```

**Version format**: `4.15.0-72-generic`
- `4` — kernel version
- `15` — major version
- `0` — minor version
- `72` — patch level
- `generic` — distro specific info