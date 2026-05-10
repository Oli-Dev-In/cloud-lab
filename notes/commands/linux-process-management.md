# Linux Process Management Commands

## ps
Process Status — displays information about currently running processes.

```bash
# Show all processes with detailed info
ps aux

# Show processes for current user
ps

# Find a specific process
ps aux | grep nginx
```

**ps aux breakdown:**
| Option | Meaning |
|---|---|
| `a` | All users |
| `u` | Detailed format with owner |
| `x` | Include processes without a terminal |

## top
Real-time process monitor. Refreshes automatically and shows CPU, memory usage per process.

```bash
top
```

**Key shortcuts inside top:**
| Key | Action |
|---|---|
| `q` | Quit |
| `k` | Kill a process (enter PID) |
| `M` | Sort by memory usage |
| `P` | Sort by CPU usage |

## htop
Improved version of top with easier navigation, color display, and mouse support.

```bash
htop
```

Preferred over top for interactive process management. May need to be installed: `sudo apt install htop`

## kill
Sends a signal to a process to stop, pause, or terminate it.

```bash
# Graceful stop — asks process to stop cleanly (default)
kill PID
kill -SIGTERM PID

# Force kill — immediately terminates, no cleanup
kill -9 PID
kill -SIGKILL PID

# Pause a process
kill -SIGSTOP PID
```

**Signals:**
| Signal | Number | Meaning |
|---|---|---|
| SIGTERM | 15 | Politely ask process to stop — can finish current task |
| SIGKILL | 9 | Force kill immediately — no choice |
| SIGSTOP | 19 | Pause the process |

**Professional rule**: always try SIGTERM first. Use SIGKILL only if the process doesn't respond.

## fg
Foreground — brings a background process back to the foreground. Opposite of `&`.

```bash
# Bring the last background process to foreground
fg

# Bring a specific job to foreground
fg %1
```