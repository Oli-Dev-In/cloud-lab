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
-rw-r--r-- 1 root root  231 Apr 25 20:50 hosts
lrwxrwxrwx 1 root root   27 Apr 20 18:07 localtime -> /usr/share/zoneinfo/Etc/UTC
```

| Column | Value | Meaning |
|---|---|---|
| 1 | `drwxr-xr-x` | Type and permissions (see breakdown below) |
| 2 | `4` | Number of hard links |
| 3 | `root` | Owner user |
| 4 | `root` | Owner group |
| 5 | `4096` | Size in bytes |
| 6 | `Apr 25 20:52` | Last modification date and time |
| 7 | `ssh` | File or directory name |

**Column 1 — type and permissions breakdown**

d  rwx  r-x  r-x
^   ^    ^    ^
|   |    |    Others (everyone else)
|   |    Group
|   Owner (user)
Type: d=directory, -=file, l=symlink

**r, w, x meaning**

For a file:
- `r` — can read the file content
- `w` — can modify the file
- `x` — can execute the file as a program or script

For a directory:
- `r` — can list its contents with `ls`
- `w` — can create, delete, or rename files inside it
- `x` — can enter it with `cd`

A `-` means the permission is absent.

**Real example — deploy.sh**

-rwxr-x--- 1 olivier developers 4096 Apr 29 09:00 deploy.sh
- `-` — regular file
- `rwx` — owner (olivier) can read, write and execute
- `r-x` — group (developers) can read and execute, cannot write
- `---` — others have no permissions at all

**Symlink**

A symlink (symbolic link) is an empty file that points to another file or directory. Indicated by `l` as the first character and `->` showing the target.

```bash
lrwxrwxrwx 1 root root 27 Apr 20 18:07 localtime -> /usr/share/zoneinfo/Etc/UTC
```

`localtime` has no content of its own — it redirects to the real timezone file. Changing the timezone means changing where the symlink points, not moving files.

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