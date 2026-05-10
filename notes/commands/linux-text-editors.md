# Linux Text Editors

## nano
Simple terminal text editor. Shortcuts are displayed at the bottom of the screen. Used for quick config file edits.

```bash
# Open or create a file
nano filename.txt

# Open a system config file
sudo nano /etc/hosts
```

**Key shortcuts:**
| Shortcut | Action |
|---|---|
| `Ctrl + O` | Save file |
| `Ctrl + X` | Exit |
| `Ctrl + K` | Cut line |
| `Ctrl + U` | Paste line |
| `Ctrl + W` | Search |

## vim
Powerful terminal text editor with a steep learning curve. Used by senior engineers for speed once mastered. Has distinct modes.

```bash
# Open or create a file
vim filename.txt
```

**Modes:**
| Mode | How to enter | Purpose |
|---|---|---|
| Normal | Default on open / `Esc` | Navigate, copy, delete |
| Insert | `i` | Type and edit text |
| Command | `:` | Save, quit, search |

**Essential commands:**
| Command | Action |
|---|---|
| `i` | Enter insert mode |
| `Esc` | Return to normal mode |
| `:w` | Save |
| `:q` | Quit |
| `:wq` | Save and quit |
| `:q!` | Quit without saving (use when stuck) |

**Professional note**: if you accidentally open vim and don't know how to exit, press `Esc` then type `:q!` and press Enter.