# SSH Security Configuration

## sshd_config — SSH Server Configuration File

The SSH daemon configuration file controls how the SSH server behaves. Located at `/etc/ssh/sshd_config`.

**Important distinction:**
| File | Purpose |
|---|---|
| `/etc/ssh/ssh_config` | SSH **client** configuration |
| `/etc/ssh/sshd_config` | SSH **server** (daemon) configuration |

Always edit `sshd_config` to change server behavior.

## What is a Daemon

A daemon is a process that runs permanently in the background without user interaction. `sshd` = SSH daemon — it listens continuously for incoming SSH connections. Equivalent to a Windows "service".

## config.d directories

A Linux convention — instead of one large config file, additional configuration files can be placed in a `.d` directory. The main file loads them automatically. Allows modular configuration without touching the main file.

Example: `/etc/ssh/sshd_config.d/` contains additional SSH configuration files.

## Disabling Root SSH Login

Direct root login via SSH is a security risk — if compromised, an attacker has immediate full system access. Best practice is to disable it and use sudo from a normal user account.

```bash
# Find the relevant parameter
sudo grep PermitRootLogin /etc/ssh/sshd_config

# Edit the config file
sudo nano /etc/ssh/sshd_config
# Change: PermitRootLogin yes → PermitRootLogin no

# Apply changes — restart the service
sudo systemctl restart sshd

# Verify service is running correctly
sudo systemctl status sshd

# Verify the parameter
sudo grep PermitRootLogin /etc/ssh/sshd_config
```

## Key sshd_config Parameters

| Parameter | Value | Meaning |
|---|---|---|
| `PermitRootLogin` | `yes` | Root can login directly via SSH |
| `PermitRootLogin` | `no` | Root login disabled — use sudo instead |
| `PermitRootLogin` | `prohibit-password` | Root can only login with SSH key, not password |

## Critical Rule — Restart After Config Changes

**Modifying a config file does nothing until the service is restarted.**

```bash
sudo systemctl restart sshd    # apply changes
sudo systemctl status sshd     # verify service started correctly
```

`systemctl status` does not require sudo — it is read-only.
`systemctl restart/stop/start` requires sudo — it modifies the system.

## Non-interactive Shells

Used for service accounts and backup agents that need to exist on the system but must not be able to login interactively.

| Shell | Behavior |
|---|---|
| `/sbin/nologin` | Denies login and displays a message — preferred |
| `/bin/false` | Denies login silently, returns false immediately |

```bash
# Create user with non-interactive shell
sudo useradd -s /sbin/nologin username

# Verify
grep username /etc/passwd
# → username:x:1001:1001::/home/username:/sbin/nologin
```

## Home Directory — Declared vs Physical

When creating a user with `-M`, `/etc/passwd` still shows a home directory path but the directory does not physically exist on disk.

```bash
sudo useradd -M username
grep username /etc/passwd
# → username:x:1001:1001::/home/username:/bin/bash  ← declared but not created

ls /home/username
# → ls: cannot access '/home/username': No such file or directory
```