# Linux System Commands

## apt
Advanced Package Tool — manages software installation, updates, and removal on Ubuntu and Debian systems. Always requires `sudo`.

```bash
# Update the package list (refreshes the catalog — does NOT install updates)
sudo apt update

# Install available upgrades
sudo apt upgrade

# Install a specific package
sudo apt install package-name

# Remove a package
sudo apt remove package-name

# Remove a package and its configuration files
sudo apt purge package-name

# Search for a package
apt search package-name
```

**Always run `apt update` before `apt install`** — ensures you get the latest available version.

**Professional use**: installing tools on a Linux server — git, python, nginx, docker, and any other software your infrastructure needs.

## systemctl
Controls systemd — the Linux initialization system that manages all services. Used constantly in production to start, stop, and monitor services.

```bash
# Start a service
sudo systemctl start nginx

# Stop a service
sudo systemctl stop nginx

# Restart a service (after config changes)
sudo systemctl restart nginx

# Enable a service to start automatically at boot
sudo systemctl enable nginx

# Disable autostart
sudo systemctl disable nginx

# Check service status
sudo systemctl status nginx

# List all running services
systemctl list-units --type=service
```

**Professional use**: checking if SSH is running, restarting a service after modifying its config file, enabling a monitoring agent at boot.

## cron and crontab
cron is the Linux job scheduler — it executes commands automatically at scheduled times. crontab is the command used to create and manage cron jobs.

```bash
# Edit your crontab (opens in default editor)
crontab -e

# List your current cron jobs
crontab -l

# Remove all cron jobs
crontab -r
```

**Crontab syntax:**
```
* * * * * command
│ │ │ │ │
│ │ │ │ └── Day of week (0-7, 0 and 7 = Sunday)
│ │ │ └──── Month (1-12)
│ │ └────── Day of month (1-31)
│ └──────── Hour (0-23)
└────────── Minute (0-59)
```

**Examples:**
```bash
# Run a script every day at 2am
0 2 * * * /home/olivier/backup.sh

# Run every 5 minutes
*/5 * * * * /home/olivier/check.sh

# Run every Monday at 9am
0 9 * * 1 /home/olivier/report.sh
```

## add-apt-repository
Adds an external package repository (PPA — Personal Package Archive) to apt's sources. Used when software is not available in official Ubuntu repositories or when you need a newer version.

```bash
# Add a PPA
sudo add-apt-repository ppa:name/ppa

# Always run apt update after adding a repository
sudo apt update
sudo apt install package-name

# Remove a PPA
sudo add-apt-repository --remove ppa:name/ppa
```

**Professional note**: avoid unverified PPAs on production servers — security risk. Fine for lab and dev environments.

## dpkg
Low-level package installer. Installs `.deb` files directly without managing dependencies automatically. Use `apt` when possible — it handles dependencies. Use `dpkg` when you have downloaded a `.deb` file manually.

```bash
# Install a .deb file
sudo dpkg -i package.deb

# List all installed packages
dpkg -l

# Check if a specific package is installed
dpkg -l | grep package-name

# Remove a package
sudo dpkg -r package-name
```

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