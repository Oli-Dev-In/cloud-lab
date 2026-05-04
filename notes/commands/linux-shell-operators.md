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