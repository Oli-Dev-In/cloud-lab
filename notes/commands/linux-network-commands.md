# Linux Network Commands

## wget
Download files from the internet directly to the server. Simple and straightforward.

```bash
# Download a file
wget https://example.com/file.txt

# Download and save with a specific name
wget -O custom-name.txt https://example.com/file.txt

# Download in background
wget -b https://example.com/largefile.zip
```

## curl
Client URL — sends HTTP requests from the terminal. More powerful than wget — downloads files but also interacts with APIs and web services.

```bash
# Download a file
curl -O https://example.com/file.txt

# Call an API and see the response
curl https://api.example.com/status

# Send data to an API (POST request)
curl -X POST -d "data=value" https://api.example.com/endpoint

# Include headers in the response
curl -I https://example.com
```

**wget vs curl:**
| | wget | curl |
|---|---|---|
| Primary use | Download files | Interact with HTTP APIs and services |
| Simplicity | Simpler for downloads | More options and flexibility |
| Production use | Download scripts, packages | Test APIs, call AWS endpoints, health checks |

## scp
Secure Copy — copies files between two machines over SSH. Same security as SSH. File transfer equivalent of cp for remote machines.

```bash
# Copy local file to remote server
scp /local/file.txt user@host:/remote/path/

# Copy remote file to local machine
scp user@host:/remote/file.txt /local/path/

# Copy with specific SSH port
scp -P 2222 file.txt user@127.0.0.1:/home/user/

# Copy a directory recursively
scp -r /local/directory/ user@host:/remote/path/

# Copy between two remote servers (from jump host)
scp /tmp/file.txt banner@stapp03:/home/data/
```

**scp syntax:**
```
scp source destination
         ^              ^
         |              └── user@host:/path (remote)
         └── /local/path or user@host:/path
```

**Verify transfer after scp:**
```bash
# Connect and check
ssh user@host
ls /destination/path/
```

**Professional use**: scp is the standard for one-off file transfers between servers. For recurring transfers or synchronization, use `rsync` instead — more efficient and resumable.

**Note on 100% confirmation:**
```
nautilus.txt.gpg    100%  105   307.5KB/s   00:00
```
The `100%` in scp output confirms the file was fully transferred without corruption.

## updog
Simple Python tool that creates a temporary web server to share files on a local network. Not used in production — useful for quick file transfers between machines on the same network.

```bash
# Start a web server in the current directory
updog
```