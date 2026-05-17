# Linux Disk and Filesystem Commands

## df
Disk Filesystem — displays disk space usage for all mounted filesystems.

```bash
# Human readable output
df -h

# Human readable with POSIX format (one line per filesystem)
df -hP

# Display specific filesystem
df -h /home
```

**Output columns:**
| Column | Meaning |
|---|---|
| Filesystem | Device or filesystem name |
| Size | Total size |
| Used | Space used |
| Avail | Space available |
| Use% | Percentage used |
| Mounted on | Mount point in the filesystem tree |

**Professional use**: check disk space before deployments, monitor partitions approaching 100% usage. A full disk causes services to crash.

```bash
# Quick check — any filesystem over 80% full?
df -h | grep -v "Use%" | awk '{ print $5 " " $6 }' | sort -rn
```