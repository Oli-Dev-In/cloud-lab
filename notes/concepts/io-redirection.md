# IO Redirection

## The Three Standard Streams

Every Linux command has three communication channels:

| Stream | Number | Default | Description |
|---|---|---|---|
| `stdin` | 0 | Keyboard | Standard input — data the command receives |
| `stdout` | 1 | Screen | Standard output — normal command result |
| `stderr` | 2 | Screen | Standard error — error messages |

stdout and stderr both display on screen by default but are separate channels. This allows redirecting them independently.

## Redirecting stdout

```bash
# Redirect stdout to a file (overwrite)
echo $SHELL > shell.txt

# Redirect stdout to a file (append)
echo $SHELL >> shell.txt

# Explicit stdout redirect (1 is optional)
command 1> output.txt
```

## Redirecting stderr

```bash
# Redirect stderr to a file (overwrite)
cat missing_file 2> error.txt

# Redirect stderr to a file (append)
cat missing_file 2>> error.txt

# Discard errors completely (send to /dev/null)
cat missing_file 2> /dev/null
```

## /dev/null — The Blackhole

A special file that discards everything written to it. Reading from it returns nothing. Used to suppress unwanted output.

```bash
# Discard all errors
command 2> /dev/null

# Discard all output (stdout and stderr)
command > /dev/null 2>&1

# Common use — run a command silently
apt update > /dev/null 2>&1
```

**Professional use**: scripts and cron jobs often redirect to `/dev/null` to avoid cluttering logs with expected output. If a command fails silently and you don't know why — check if output is being sent to `/dev/null` by mistake.

## Redirecting both stdout and stderr

```bash
# Redirect stdout and stderr to the same file
command > output.txt 2>&1

# Discard all output
command > /dev/null 2>&1
```

## Pipes

The pipe `|` passes stdout of one command as stdin to the next. No intermediate file needed.

```bash
grep "error" /var/log/syslog | less
ps aux | grep nginx | wc -l
```

See `linux-shell-operators.md` for full pipe documentation.

## tee

Sends output simultaneously to the screen AND to a file. Useful when you need to see output in real time while saving it.

```bash
# Write to file AND display on screen
echo $SHELL | tee shell.txt

# Append to file AND display on screen
echo $SHELL | tee -a shell.txt
```

**tee vs redirection:**
| | `>` redirection | `tee` |
|---|---|---|
| Output to screen | No | Yes |
| Output to file | Yes | Yes |
| Use when | Just saving | Monitoring AND saving |

## Quick Reference

| Technique | Command |
|---|---|
| Redirect stdout | `command > file.txt` |
| Append stdout | `command >> file.txt` |
| Redirect stderr | `command 2> file.txt` |
| Append stderr | `command 2>> file.txt` |
| Redirect both | `command > file.txt 2>&1` |
| Discard all output | `command > /dev/null 2>&1` |
| Pipe to next command | `command1 \| command2` |
| Output to screen and file | `command \| tee file.txt` |