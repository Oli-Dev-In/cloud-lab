# Linux Shell Operators

## > — Output redirection (overwrite)
Redirects the output of a command to a file. If the file exists, it is overwritten. If it does not exist, it is created.

```bash
# Write command output to a file (overwrites)
echo "Hello" > file.txt

# Save the list of files to a text file
ls -l > directory-listing.txt
```

## >> — Output redirection (append)
Same as `>` but appends to the end of the file instead of overwriting. Existing content is preserved.

```bash
# Append to a file
echo "New line" >> file.txt

# Append command output to a log file
echo "Task completed" >> logfile.txt
```

## & — Background execution
Runs a command in the background, freeing the terminal immediately for other commands.

```bash
# Run a long process in the background
apt upgrade &

# The terminal returns immediately and you can keep working
```

**Professional use**: launching services or long processes without blocking the terminal.

## && — Conditional chaining
Executes the second command only if the first command succeeds. If the first command fails, the second is never executed.

```bash
# Update package list, then upgrade only if update succeeded
apt update && apt upgrade

# Create a directory, then move into it only if creation succeeded
mkdir new-project && cd new-project
```

**Professional use**: scripts and CI/CD pipelines where each step depends on the previous one succeeding. If step 1 fails, you don't want step 2 to run on a broken state.

**Key difference between & and &&:**

| Operator | Meaning |
|---|---|
| `&` | Run in background, don't wait for result |
| `&&` | Run second command only if first succeeded |

## | — Pipe
Takes the output of one command and passes it directly as input to the next command. Creates powerful command chains without intermediate files.

```bash
# Basic syntax
command1 | command2 | command3

# Find a specific package among all installed packages
rpm -qa | grep wget
dpkg -l | grep nginx

# Count how many packages are installed
dpkg -l | wc -l

# Find a specific running process
ps aux | grep nginx

# View last 10 lines of a log file
cat /var/log/syslog | tail -10

# List files sorted by size, show only top 5
ls -lS | head -5

# Search for errors in logs, count occurrences
grep "ERROR" /var/log/syslog | wc -l
```

**Professional use**: pipe is one of the most powerful tools in Linux. Almost every real command in production combines multiple tools with pipes — list processes, filter by name, count results, sort output.

**Key concept**: the left command's stdout becomes the right command's stdin. Data flows left to right through the chain.