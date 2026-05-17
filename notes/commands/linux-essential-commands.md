# Linux Essential Commands

## whoami
Displays the currently logged-in user. Simple but useful when managing 
multiple servers or switching between users.

```bash
olivier@ubuntu-server-01:~$ whoami
olivier
```

## man
Manual — displays the official built-in documentation for any command. 
A cloud engineer does not memorize every option of every command. 
`man` is always the first step before searching online.

```bash
olivier@ubuntu-server-01:~$ man ls
```

**Navigation inside man:**

| Key | Action |
|---|---|
| `↑` `↓` | Scroll line by line |
| `Space` | Scroll page by page |
| `q` | Quit and return to terminal |

## --help
Quick summary of a command's usage and options. Faster than `man` when you just need a reminder of a specific option.

```bash
grep --help
ls --help
chmod --help
```

**Difference with man:**
- `--help` — short summary, fast, directly in terminal
- `man` — full documentation, detailed, navigable

## clear
Clears the terminal screen. Keyboard shortcut: `Ctrl + L`.

```bash
olivier@ubuntu-server-01:~$ clear
```
## whatis
Displays a one-line description of a command. Faster than `man` when you just need to know what a command does.

```bash
whatis ls
whatis grep
```

## apropos
Searches the man page descriptions for a keyword. Useful when you know what you want to do but not which command to use.

```bash
apropos copy      # find commands related to copying
apropos network   # find commands related to networking
```

**Difference with whatis**: `whatis` describes a specific command you already know. `apropos` helps you find a command when you only know the concept.

## which
Shows the exact path of an executable command. Useful when multiple versions of a program are installed.

```bash
which python3    # → /usr/bin/python3
which bash       # → /bin/bash
which ls         # → /bin/ls
```

## chsh
Change Shell — changes your default shell permanently.

```bash
# Change default shell to zsh
chsh -s /bin/zsh

# Change default shell back to bash
chsh -s /bin/bash
```

Takes effect at next login.

## alias
Creates a shortcut name for a command or sequence of commands.

```bash
# Create an alias for the current session only
alias ll="ls -l"
alias la="ls -la"
alias cls="clear"

# Make an alias permanent
echo 'alias ll="ls -l"' >> ~/.profile

# List all current aliases
alias

# Remove an alias
unalias ll
```

## export
Makes a variable available to child processes — programs and scripts launched from the current shell. Without export, a variable is local to the current shell only.

```bash
# Define a local variable — NOT visible to child processes
MY_VAR="hello"

# Export a variable — visible to child processes
export MY_VAR="hello"

# Export an already defined variable
MY_VAR="hello"
export MY_VAR

# Modify an existing environment variable
export PATH="$PATH:/new/directory"

# Make a variable permanent across sessions
echo 'export MY_VARIABLE="example_value"' >> ~/.profile

# List all currently exported variables
export -p
```

**Why it matters in cloud/DevOps**

Environment variables are how you pass configuration to programs without hardcoding values. In production you will constantly use exported variables for:

- AWS credentials: `export AWS_ACCESS_KEY_ID="..."` 
- Terraform configuration: `export TF_VAR_region="eu-west-1"`
- Application config: `export DATABASE_URL="..."`
- PATH modifications: adding new tools to your shell's search path

**Local vs exported — concrete example:**

```bash
# This variable stays in the current shell
SECRET="my_value"
bash -c 'echo $SECRET'    # → empty, child process cannot see it

# This variable is passed to child processes
export SECRET="my_value"
bash -c 'echo $SECRET'    # → my_value
```

**Important**: `export` only passes variables to child processes — never to the parent shell. A child cannot modify the parent's environment.

## env
Lists all currently exported environment variables in the session.

```bash
env

# Find a specific variable
env | grep PATH
```
