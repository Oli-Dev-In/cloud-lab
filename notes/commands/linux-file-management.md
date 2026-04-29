# Linux File Management Commands

## mkdir
Make Directory — creates one or more directories.

```bash
# Create a single directory
mkdir my-folder

# Create multiple directories at once
mkdir folder1 folder2 folder3

# Create a directory and all missing parent directories
mkdir -p parent/child/grandchild
```

`-p` stands for "parents" — creates the full path even if intermediate directories don't exist yet.

## touch
Creates an empty file. If the file already exists, updates its timestamp to the current time.

```bash
# Create an empty file
touch file.txt

# Create multiple files at once
touch file1.txt file2.txt file3.txt
```

The file type is determined by the extension you give it — `touch script.sh` creates a shell script file, `touch config.yaml` creates a YAML file.

## cp
Copy — copies files or directories from source to destination.

```bash
# Copy a file
cp source.txt destination.txt

# Copy a file into a directory
cp source.txt directory/

# Copy a directory and all its contents (recursive)
cp -r source-directory/ destination-directory/

# Verbose — shows what is being copied
cp -v source.txt destination.txt

# Interactive — asks before overwriting existing files
cp -i source.txt destination.txt
```

**Professional note**: `-v` (verbose) is useful on large operations to see exactly what is happening in real time. `-i` (interactive) protects against accidental overwrites.

## mv
Move — moves or renames files and directories. Unlike `cp`, the original is removed.

```bash
# Move a file to a different directory
mv file.txt /other/directory/

# Rename a file (same as moving to a new name in the same directory)
mv old-name.txt new-name.txt

# Move a directory
mv source-directory/ destination/

# Verbose
mv -v source.txt destination.txt

# Interactive — asks before overwriting
mv -i source.txt destination.txt
```

**Key concept**: renaming and moving are the same operation in Linux. `mv old new` moves the file from the path `old` to the path `new`. There is no dedicated rename command in Linux — `mv` handles both.

## rm
Remove — permanently deletes files and directories. No trash bin, no undo.

```bash
# Delete a file
rm filename.txt

# Delete a directory and all its contents
rm -r directory/

# Force delete without confirmation (dangerous)
rm -f filename.txt

# Recursive + force (extremely dangerous — always verify the path first)
rm -rf directory/

# Interactive — asks for confirmation before each deletion
rm -i filename.txt

# Verbose — shows each file as it is deleted
rm -v filename.txt
rm -rv directory/
```

**Professional rule**: always double-check the path before running `rm`. In production, prefer `rm -i` when in doubt. Never run `rm -rf` without verifying the exact target. Use `-v` with `-r` to see exactly what is being deleted in real time.

## rmdir
Remove directory — deletes empty directories only. Refuses if the directory contains anything.

```bash
rmdir empty-directory/
```

Safer than `rm -r` when you want to confirm a directory is empty before deleting it.