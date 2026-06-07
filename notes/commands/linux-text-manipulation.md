# Linux Text Manipulation Commands

## sed
Stream EDitor — processes and transforms text in files or streams. Performs substitutions, deletions, and line selections without opening a file in an editor. Essential for scripting and automation.

```bash
# Basic substitution — replace first occurrence per line
sed 's/old/new/' file.txt

# Global substitution — replace ALL occurrences
sed 's/old/new/g' file.txt

# Modify file directly (in-place)
sed -i 's/old/new/g' file.txt

# Preview changes without modifying the file
sed 's/old/new/g' file.txt

# Delete lines containing a pattern
sed '/pattern/d' file.txt

# Display specific lines (lines 5 to 10)
sed -n '5,10p' file.txt

# Chain multiple operations
sed -e 's/old1/new1/g' -e 's/old2/new2/g' file.txt
```

**sed substitution syntax breakdown:**
```
sed 's/old/new/g' file
      ^  ^   ^  ^
      |  |   |  └── flag: g=global, empty=first only
      |  |   └───── replacement string
      |  └───────── pattern to find
      └──────────── s = substitute command
```

**Key options:**
| Option | Meaning |
|---|---|
| `-i` | In-place — modifies the file directly |
| `-e` | Expression — chain multiple sed commands |
| `-n` | Suppress default output — use with `p` to print specific lines |
| `g` flag | Global — replace all occurrences per line |
| `d` command | Delete matching lines |
| `p` command | Print matching lines |

**Professional use**: sed is the standard tool for text substitution in scripts and automation. Never use a text editor (nano/vim) when you need to modify files programmatically.

**Always verify after modification:**
```bash
# Check old string is gone
sudo grep "old" file.txt    # should return nothing

# Check new string is present
sudo grep "new" file.txt    # should return modified lines
```

**Files in /root require sudo:**
```bash
sudo sed -i 's/old/new/g' /root/file.txt
sudo grep "new" /root/file.txt
```