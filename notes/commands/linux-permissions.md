# Linux Permissions Commands

## sudo
Superuser do — executes a single command with root privileges, then immediately returns to normal user. The safest way to perform administrative tasks.

```bash
# Run a single command as root
sudo apt update

# Open a file that requires root access
sudo nano /etc/hosts
```

**Key principle**: you are root only for the duration of one command. The next command runs as your normal user again. This is intentional — principle of least privilege.

**In production**: nobody works permanently connected as root on a server. Always use `sudo` for individual commands that require it.

## su
Switch User — changes your current user identity until you type `exit`.

```bash
# Switch to another user (requires that user's password)
su claude

# Switch to root (requires root password)
su

# Return to previous user
exit
```

**Difference with sudo**:

| | sudo | su |
|---|---|---|
| Scope | One command only | Entire session until exit |
| Password required | Your own password | Target user's password |
| Risk | Low — limited scope | Higher — full session as other user |
| Used in production | Yes — standard | Rarely — root su often disabled |

## chmod
Change mode — modifies the permissions of a file or directory.

### Symbolic notation
Format: `chmod who+/-/=which file`

**Who:**
| Symbol | Meaning |
|---|---|
| `u` | user (owner) |
| `g` | group |
| `o` | others |
| `a` | all (u + g + o) |

**What:**
| Symbol | Meaning |
|---|---|
| `+` | add permission |
| `-` | remove permission |
| `=` | set exactly these permissions and remove all others |

**Which:**
| Symbol | Meaning |
|---|---|
| `r` | read |
| `w` | write |
| `x` | execute |

```bash
# Add execute permission for owner only
chmod u+x script.sh

# Add execute for owner and group
chmod ug+x script.sh

# Remove write permission for others
chmod o-w file.txt

# Set read-only for everyone (removes everything else)
chmod a=r file.txt
```

### Octal notation
Each permission has a numeric value: `r=4`, `w=2`, `x=1`, `-=0`

Add the values for each group (owner, group, others) to get a three-digit number.

| Octal | Permissions | Meaning |
|---|---|---|
| `7` | `rwx` | 4+2+1 |
| `6` | `rw-` | 4+2+0 |
| `5` | `r-x` | 4+0+1 |
| `4` | `r--` | 4+0+0 |
| `0` | `---` | 0+0+0 |

```bash
# owner=rwx, group=r-x, others=r-x — standard for scripts and directories
chmod 755 script.sh

# owner=rw-, group=r--, others=r-- — standard for config files
chmod 644 config.yml

# owner=rw-, group=---, others=--- — private files (SSH keys)
chmod 600 ~/.ssh/id_rsa

# owner=rwx, group=---, others=--- — private scripts
chmod 700 script.sh
```

**In production**: octal notation is the standard in scripts, Terraform, and Ansible. Symbolic notation is used for quick manual changes.

## chown
Change owner — changes the owner and/or group of a file or directory. Requires sudo.

```bash
# Change owner only
sudo chown newowner file.txt

# Change owner and group at the same time
sudo chown newowner:newgroup file.txt

# Change group only
sudo chown :newgroup file.txt

# Recursive — change owner for a directory and all its contents
sudo chown -R newowner:newgroup directory/
```

**Real example:**
```bash
# Give root ownership of a config file
sudo chown root:root /etc/myconfig.conf

# Give a user ownership of their home directory contents
sudo chown -R olivier:olivier /home/olivier/
```

## chgrp
Change group — changes only the group of a file. Shortcut when you don't need to change the owner.

```bash
# Change group only
sudo chgrp newgroup file.txt

# Recursive
sudo chgrp -R newgroup directory/
```

**Note**: `chown :newgroup file` and `chgrp newgroup file` do the same thing. `chgrp` is more explicit when you only want to change the group.

## id
Displays your current user ID, group ID, and all groups you belong to.

```bash
olivier@ubuntu-server-01:~$ id
uid=1000(olivier) gid=1000(olivier) groups=1000(olivier),4(adm),24(cdrom),27(sudo)
```

Useful to verify which groups you belong to and whether you have sudo access.

## groups
Displays only the groups the current user belongs to.

```bash
olivier@ubuntu-server-01:~$ groups
olivier adm cdrom sudo
```

## passwd
Changes a user's password.

```bash
# Change your own password
passwd

# Change another user's password (requires sudo)
sudo passwd username
```