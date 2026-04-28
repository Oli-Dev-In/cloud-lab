# Linux Navigation Commands

## pwd
Print Working Directory. Displays the full path of your current location in the filesystem. First reflex when lost in a terminal — always tells you exactly where you are.

```bash
olivier@ubuntu-server-01:~$ pwd
/home/olivier
```

## ls
List — displays the contents of a directory.

```bash
# List current directory
olivier@ubuntu-server-01:~$ ls

# List a specific directory
olivier@ubuntu-server-01:~$ ls /etc

# List with detailed information
olivier@ubuntu-server-01:~$ ls -l

# List all files including hidden files (starting with .)
olivier@ubuntu-server-01:~$ ls -a
.  ..  .bash_history  .bash_logout  .bashrc  .cache  .lesshst  .profile  .ssh
```

Hidden files and directories start with `.` — `ls` ignores them by default. `-a` stands for **all**.

### ls -l output explained

```bash
drwxr-xr-x 4 root root 4096 Apr 25 20:52 ssh
```

| Column | Value | Meaning |
|---|---|---|
| 1 | `drwxr-xr-x` | Type and permissions — `d` means directory, `-` means file, `l` means symlink |
| 2 | `4` | Number of hard links |
| 3 | `root` | Owner user |
| 4 | `root` | Owner group |
| 5 | `4096` | Size in bytes |
| 6 | `Apr 25 20:52` | Last modification date and time |
| 7 | `ssh` | File or directory name |

## cd
Change Directory — navigate to a different location in the filesystem.

```bash
# Go to a specific directory
olivier@ubuntu-server-01:~$ cd /etc
olivier@ubuntu-server-01:/etc$

# Go up one level to parent directory
olivier@ubuntu-server-01:/etc$ cd ..
olivier@ubuntu-server-01:/$

# Go to home directory
olivier@ubuntu-server-01:/$ cd ~
olivier@ubuntu-server-01:~$

# Go back to previous directory
olivier@ubuntu-server-01:~$ cd -
/
olivier@ubuntu-server-01:/$
```

## Navigation shortcuts

Universal shortcuts usable in any navigation command.

| Shortcut | Meaning | Example |
|---|---|---|
| `.` | Current directory | `git add .` — add everything in current directory |
| `..` | Parent directory | `cd ..` — go up one level |
| `~` | Home directory | `cd ~` — go to `/home/olivier` |
| `/` | Root of the filesystem | `cd /` — go to the root |
| `-` | Previous directory | `cd -` — go back to where you were |