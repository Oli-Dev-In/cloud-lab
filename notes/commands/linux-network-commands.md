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
Secure Copy — copies files between two machines over SSH. Same security as SSH.

```bash
# Copy a local file to a remote server
scp file.txt olivier@server:/home/olivier/

# Copy a file from a remote server to local machine
scp olivier@server:/home/olivier/file.txt .

# Copy with a specific SSH port
scp -P 2222 file.txt olivier@127.0.0.1:/home/olivier/

# Copy a directory recursively
scp -r directory/ olivier@server:/home/olivier/
```

**Professional use**: sending scripts or config files to AWS EC2 instances.

## updog
Simple Python tool that creates a temporary web server to share files on a local network. Not used in production — useful for quick file transfers between machines on the same network.

```bash
# Start a web server in the current directory
updog
```