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
