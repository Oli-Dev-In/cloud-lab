# linux-text-and-search commands

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

### Writing to a file with cat

```bash
# Write content to a file (overwrites existing content)
cat > filename.txt
# Type your content, then press Ctrl+D to save and exit

# Append content to a file
cat >> filename.txt
# Type your content, then press Ctrl+D to save and exit
```

**Note**: for anything beyond simple writes, use a proper text editor like `nano` or `vim`.

## less
Displays file content page by page. Unlike `cat` which dumps everything at once, `less` lets you navigate through long files. Essential for reading logs.

```bash
# Open a file with less
less /var/log/syslog

# Open and search immediately
less +/search-term /var/log/syslog
```

**Navigation inside less:**
| Key | Action |
|---|---|
| `↑` `↓` | Scroll line by line |
| `Space` | Next page |
| `b` | Previous page |
| `/term` | Search forward |
| `n` | Next search result |
| `q` | Quit |

## more
Displays file content page by page — forward only. Predecessor of `less`. Cannot scroll back up.

```bash
more /var/log/syslog
```

**more vs less:**
| | more | less |
|---|---|---|
| Scroll down | Yes | Yes |
| Scroll back up | No | Yes |
| Search | Limited | Yes — use `/term` |
| Production use | Rarely | Standard |

**Note**: "less is more" — `less` replaced `more` because it does everything `more` does and more. Always prefer `less` in practice.

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

### Advanced usage — filtering and executing

```bash
# Find only regular files (not directories)
find /path -type f

# Find only directories
find /path -type d

# Find files owned by a specific user
find /path -user username

# Combine filters — regular files owned by specific user
find /path -type f -user username

# Execute a command on each result found
find /path -type f -user username -exec cp --parents {} /destination \;
```

**-exec syntax breakdown:**

| Element | Meaning |
|---|---|
| `-exec` | Execute a command for each file found |
| `{}` | Placeholder — replaced by the current file path |
| `\;` | Terminates the -exec command — required |

**Why `\;` ?** — tells `find` where the `-exec` command ends. The `\` escapes `;` which has special meaning in bash.

## locate
Fast file search using a pre-built database. Much faster than `find` but may be outdated.

```bash
# Find a file by name
locate City.txt

# Update the database if files are not found
sudo updatedb
```

**locate vs find:**
| | `locate` | `find` |
|---|---|---|
| Speed | Very fast | Slower |
| Data source | Pre-built database | Live filesystem scan |
| Up to date | May miss recent files | Always current |
| Use when | Quick search on known filenames | Precise filtering needed |

**Professional rule**: use `locate` for quick searches, `find` when you need precision or the file was recently created.

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

### Additional grep options

```bash
# Search for whole word only (not partial matches)
grep -w "exam" file.txt

# Show lines that do NOT match
grep -v "pattern" file.txt

# Show N lines after the match
grep -AN "pattern" file.txt

# Show N lines before the match
grep -BN "pattern" file.txt

# Show N lines before AND after the match
grep -AN -BN "pattern" file.txt
```

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

## file
Detects and displays the real type of a file — based on file content, not the extension. Useful when a file has no extension or a misleading one.

```bash
# Check the type of a file
file image.jpg

# Check the type of a script
file script.sh

# Check the type of a binary
file /bin/ls
```

**Example output:**
```
script.sh: Bourne-Again shell script, ASCII text executable
image.jpg: JPEG image data
/bin/ls: ELF 64-bit LSB pie executable
```