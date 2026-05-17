# Bash Environment

## Shells

A shell is the program that interprets your commands in the terminal. There are several shell variants — each is a different implementation with its own syntax and features.

| Shell | Name | Notes |
|---|---|---|
| `sh` | Bourne Shell | The original Unix shell |
| `bash` | Bourne Again Shell | Default on most Linux systems including Ubuntu. Standard in cloud/DevOps. |
| `csh` / `tcsh` | C Shell | C-like syntax |
| `ksh` | Korn Shell | Combines features of sh and csh |
| `zsh` | Z Shell | Popular on macOS, highly customizable |

**In production**: bash is the standard. All scripts and automation in cloud/DevOps are written in bash by default.

Check your current shell:
```bash
echo $SHELL
# → /bin/bash
```

## Variables

### Local variables
Exist only in the current shell session. Not passed to child processes. Disappear when the terminal is closed.

```bash
MY_VAR="hello"
echo $MY_VAR
```

### Environment variables
Exported variables — available to the current shell AND all child processes (scripts and programs launched from this shell).

```bash
export MY_VAR="hello"
```

### Viewing environment variables
```bash
env          # list all exported environment variables
echo $MY_VAR # print a specific variable
```

### Common environment variables
| Variable | Meaning |
|---|---|
| `$SHELL` | Path to the default shell |
| `$HOME` | Path to the home directory |
| `$PATH` | Directories where the shell looks for commands |
| `$USER` | Current logged-in user |

## $PATH — How Linux Finds Commands

`$PATH` is an environment variable containing a list of directories where the shell looks for executable commands. When you type a command, the shell searches each directory in PATH in order until it finds the executable.

```bash
# Display your current PATH
echo $PATH
# → /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

# Check which directory a command comes from
which python3
# → /usr/bin/python3

# Add a new directory to PATH (current session only)
export PATH=$PATH:/opt/OBS/bin

# Add permanently
echo 'export PATH=$PATH:/opt/newprogram/bin' >> ~/.profile
```

**Why it matters**: if a command is not found, it means its directory is not in your PATH. Adding a directory to PATH makes its programs available as commands from anywhere.

## $HOME

Environment variable containing the path to the current user's home directory. Equivalent to `~`.

```bash
echo $HOME
# → /home/olivier
```

## Built-in vs External Commands

Linux commands are divided into two types:

**Built-in commands** — integrated directly into the shell. Always available regardless of what is installed on the system. No file exists on disk for them.

Examples: `cd`, `pwd`, `export`, `mkdir`, `echo`, `type`

**External commands** — separate binary programs stored on disk. Located by the shell using `$PATH`. Can be installed or removed.

Examples: `mv`, `cp`, `ls`, `grep`, `find`, `python3`

```bash
# Check if a command is built-in or external
type cd
# → cd is a shell builtin

type mv
# → mv is /usr/bin/mv
```

**Why it matters**: built-in commands run faster since the shell does not need to search PATH or load a program. External commands give you flexibility — you can install new tools and make them available as commands by adding their directory to PATH.

## Making configuration permanent with ~/.profile

Commands and settings typed directly in the terminal are lost when the session closes. To make them permanent, add them to `~/.profile` — a file executed automatically at every login.

```bash
# Make a variable permanent
echo 'export MY_VARIABLE="example_value"' >> ~/.profile

# Make an alias permanent
echo 'alias ll="ls -l"' >> ~/.profile

# Customize the prompt permanently
echo 'PS1="[\d]\u@\h:\w$ "' >> ~/.profile
```

**Pattern**: `echo 'configuration line' >> ~/.profile`

After editing `~/.profile`, apply changes immediately without logging out:
```bash
source ~/.profile
```

## The Bash Prompt (PS1)

`PS1` is the environment variable that controls what is displayed before the cursor in the terminal.

```bash
# Default Ubuntu prompt
PS1="\u@\h:\w\$ "

# Prompt with date
PS1="[\d]\u@\h:\w$ "

# Prompt with dynamic date
PS1="[\$(date +%a\ %b\ %d)]\u@\h:\w\$ "
```

**PS1 variables:**
| Variable | Meaning |
|---|---|
| `\u` | Current user |
| `\h` | Hostname (short) |
| `\H` | Hostname (full) |
| `\w` | Current directory (full path) |
| `\W` | Current directory (basename only) |
| `\d` | Date (e.g. Mon May 16) |
| `\t` | Time 24h (HH:MM:SS) |
| `\T` | Time 12h (HH:MM:SS) |
| `\@` | Time 12h (am/pm) |
| `\n` | Newline |
| `\s` | Shell name |
| `\v` | Shell version |
| `\$` | $ for normal user, # for root |
| `\!` | History number of the command |
| `\#` | Command number in current session |
| `\\` | Literal backslash |

## Bash Auto-completion

Press `Tab` to auto-complete commands, file names, and paths.
Press `Tab` twice to see all available options when there are multiple matches.

```bash
cd /home/oli    # press Tab → auto-completes to /home/olivier
ls /etc/ssh     # press Tab Tab → shows all files in /etc/ssh
```