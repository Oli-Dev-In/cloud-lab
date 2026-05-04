# Linux File Reading Commands

## echo
Prints text or the value of a variable to the terminal. Simple but used constantly in scripts to display messages or write content to files.

```bash
# Print text to the terminal
echo "Hello World"

# Write text to a file (overwrites existing content)
echo "Hello World" > file.txt

# Append text to a file
echo "Hello World" >> file.txt

# Print the value of a variable
echo $HOME
```

## cat
Concatenate — displays the full content of a file in the terminal. Also used to combine multiple files.

```bash
# Display file content
cat file.txt

# Display multiple files
cat file1.txt file2.txt

# Display with line numbers
cat -n file.txt
```

**Professional use**: quick way to read config files, logs, or scripts without opening an editor.

## find
Searches for files and directories in the filesystem by name, type, size, date, or permissions.

```bash
# Find a file by name in current directory and subdirectories
find . -name "file.txt"

# Find all .txt files from root
find / -name "*.txt"

# Find only directories named "logs"
find / -type d -name "logs"

# Find only files named "config"
find / -type f -name "config"

# Find files modified in the last 7 days
find . -mtime -7
```

**Key options:**
| Option | Meaning |
|---|---|
| `-name` | Search by filename |
| `-type f` | Files only |
| `-type d` | Directories only |
| `-mtime` | Modified time in days |

## grep
Global Regular Expression Print — searches for a pattern inside file content. Unlike `find` which searches for files by name, `grep` searches what is written inside files.

```bash
# Search for a word inside a file
grep "error" logfile.txt

# Case-insensitive search
grep -i "error" logfile.txt

# Show line numbers
grep -n "error" logfile.txt

# Search recursively in all files in a directory
grep -r "error" /var/log/

# Show lines that do NOT match
grep -v "error" logfile.txt

# Count the number of matching lines
grep -c "error" logfile.txt
```

**Professional use**: searching logs for errors, finding configuration values, filtering command output.

## wc
Word Count — counts lines, words, and bytes in a file.

```bash
# Count lines, words and bytes
wc file.txt

# Count lines only
wc -l file.txt

# Count words only
wc -w file.txt

# Count bytes only
wc -c file.txt
```

**Output format**: `lines words bytes filename`

**Professional use**: quickly check how many lines a log file has, count entries in a list.