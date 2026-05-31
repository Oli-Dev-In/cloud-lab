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

### Navigation in command mode
```bash
h    # move left
j    # move down
k    # move up
l    # move right
# Arrow keys also work
```

### Entering insert mode
| Key | Cursor position |
|---|---|
| `i` | Before current character |
| `a` | After current character |
| `o` | New line below |
| `I` | Beginning of line |
| `A` | End of line |
| `O` | New line above |

### Command mode operations
```bash
YY        # copy current line
P         # paste above current line
DD        # delete current line
D3D       # delete 3 lines
X         # delete character under cursor
U         # undo
Ctrl+R    # redo
ZZ        # save and quit
```

### Search in command mode
```bash
/pattern    # search forward
?pattern    # search backward
n           # next match (forward)
N           # previous match (backward)
```

### Last line mode (press : from command mode)
```bash
:w          # save
:q          # quit
:wq         # save and quit
:q!         # quit without saving
```

### Three modes summary
| Mode | How to enter | How to exit |
|---|---|---|
| Command mode | Default / `Esc` | — |
| Insert mode | `i`, `a`, `o`, `I`, `A`, `O` | `Esc` |
| Last line mode | `:` | `Enter` or `Esc` |

**vim vs vi**: vim is "VI Improved" — adds autocomplete, syntax highlighting, spell checking, plugins. On modern Linux systems, `vi` is often a symlink to vim.