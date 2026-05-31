# Linux File Compression and Archival Commands

## du
Disk Usage — displays the size of a file or directory.

```bash
# Size in kilobytes
du -sk file.txt

# Human-readable size
du -sh file.txt
# → 98M    file.txt

# Human-readable size with ls
ls -lh file.txt
```

**Options:**
| Option | Meaning |
|---|---|
| `-s` | Summary — show total size only |
| `-k` | Size in kilobytes |
| `-h` | Human-readable (KB, MB, GB) |

## tar
Tape Archive — groups multiple files or directories into a single archive file (tarball). Does NOT compress by default — use `-z` to add gzip compression.

```bash
# Create an archive
tar -cf archive.tar file1 file2 file3

# Create a compressed archive (gzip)
tar -zcf archive.tar.gz file1 file2 file3

# List contents of an archive
tar -tf archive.tar

# Extract an archive
tar -xf archive.tar

# Extract a compressed archive
tar -xzf archive.tar.gz
```

**Options:**
| Option | Meaning |
|---|---|
| `-c` | Create archive |
| `-f` | Specify filename |
| `-t` | List contents |
| `-x` | Extract |
| `-z` | Compress/decompress with gzip |

**Professional use**: tar is the standard for packaging files for transfer or backup. `.tar.gz` (also called `.tgz`) is the most common format.

## gzip / gunzip
Fast compression. Most common compression tool — used by default with tar `-z`.

```bash
# Compress
gzip file.txt
# → creates file.txt.gz, original file is removed

# Decompress
gunzip file.txt.gz
```

## bzip2 / bunzip2
Better compression ratio than gzip but slower. Extension `.bz2`.

```bash
# Compress
bzip2 file.txt
# → creates file.txt.bz2

# Decompress
bunzip2 file.txt.bz2
```

## xz / unxz
Best compression ratio of the three but slowest. Extension `.xz`.

```bash
# Compress
xz file.txt
# → creates file.txt.xz

# Decompress
unxz file.txt.xz
```

## Comparison

| Tool | Extension | Speed | Compression ratio |
|---|---|---|---|
| gzip | `.gz` | Fast | Good |
| bzip2 | `.bz2` | Medium | Better |
| xz | `.xz` | Slow | Best |

**Professional rule**: use gzip for most cases — it is the fastest and universally supported. Use xz when compression ratio matters more than speed.

## Read compressed files without decompressing

```bash
zcat file.gz      # read gzip file
bzcat file.bz2    # read bzip2 file
xzcat file.xz     # read xz file
```