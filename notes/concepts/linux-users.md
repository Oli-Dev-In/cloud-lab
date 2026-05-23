# Linux Users and Accounts

## /etc/passwd — User Database

Every user account on a Linux system is stored in `/etc/passwd`. Each line represents one user with seven fields separated by colons.

```
username:x:UID:GID:comment:home_directory:shell
```

**Real example:**
```
yousuf:x:1696:1696::/var/www/yousuf:/bin/bash
```

| Field | Value | Meaning |
|---|---|---|
| `yousuf` | username | Login name |
| `x` | password | Password is stored in /etc/shadow (x = placeholder) |
| `1696` | UID | User ID — unique numeric identifier |
| `1696` | GID | Primary group ID |
| `` | comment | Optional user description (empty here) |
| `/var/www/yousuf` | home directory | User's home directory |
| `/bin/bash` | shell | Default shell on login |

**Read a specific user's entry:**
```bash
grep username /etc/passwd
```

## UID — User ID

Every user has a unique numeric ID. Linux uses UIDs internally — usernames are just human-readable aliases.

| UID range | Purpose |
|---|---|
| 0 | root — absolute administrator |
| 1-999 | System users — services and daemons |
| 1000+ | Regular users created manually |

```bash
# Check your own UID
id
# → uid=1000(olivier) gid=1000(olivier) groups=1000(olivier)...

# Check another user's UID
id username
```

## useradd vs adduser

Two commands exist to create users on Linux — they are not the same.

**`useradd`** — low-level command, non-interactive, predictable, scriptable. Professional standard in DevOps and automation.

**`adduser`** — interactive script that wraps useradd, asks questions, creates home directory automatically. Used for manual one-off user creation.

**Professional rule**: always use `useradd` in scripts and automated environments. Use `adduser` only for manual interactive creation on a desktop.

## /etc/shadow — Password Database

Passwords are not stored in `/etc/passwd` — they are stored encrypted in `/etc/shadow`, readable only by root. The `x` in `/etc/passwd` is just a placeholder indicating the password is in `/etc/shadow`.

```bash
# View shadow file (requires sudo)
sudo cat /etc/shadow
```

## Jump Host Pattern

In professional environments you often cannot connect directly to servers. A **jump host** (also called bastion host) is an intermediate server you connect to first, then SSH from there to internal servers.

```
Your machine → SSH → Jump Host → SSH → Target Server
```

```bash
# Connect to jump host first
ssh user@jump-host

# Then connect to internal server
ssh user@internal-server
```

This is a standard security pattern in cloud infrastructure — AWS calls it a bastion host.q