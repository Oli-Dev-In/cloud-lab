# Linux System Commands

## apt
Advanced Package Tool — high-level package manager for Debian-based systems (Ubuntu, Debian, Linux Mint). Automatically resolves dependencies. Always use `apt` over `dpkg` for standard package management.

```bash
# Update the package list (refresh catalog — does NOT install updates)
sudo apt update

# Install available upgrades
sudo apt upgrade

# Install a specific package
sudo apt install package-name

# Remove a package (keep config files)
sudo apt remove package-name

# Remove a package AND its config files
sudo apt purge package-name

# Search for a package
apt search package-name

# Show package details
apt show package-name
```

**Always run `apt update` before `apt install`** — ensures you get the latest available version.

**APT flow**: APT → DPKG → installed package. APT is the front-end, DPKG does the actual installation.

## dpkg
Low-level package manager for Debian-based systems. Installs `.deb` files directly. Does NOT resolve dependencies automatically — use `apt` instead unless you have a manually downloaded `.deb` file.

```bash
# Install a .deb file
sudo dpkg -i package.deb

# Remove a package
sudo dpkg -r package-name

# List installed packages
dpkg -l

# Check status of a specific package
dpkg -s package-name

# List files installed by a package
dpkg -L package-name
```

**When to use dpkg**: only when you have downloaded a `.deb` file manually and need to install it directly. For everything else, use `apt`.

## rpm
Low-level package manager for RPM-based systems (RHEL, CentOS, Fedora). Works with `.rpm` files. Does NOT resolve dependencies — use `yum` or `dnf` instead.

```bash
# Install a package
sudo rpm -ivh package.rpm

# Uninstall a package
sudo rpm -e package-name

# Upgrade a package
sudo rpm -Uvh package.rpm

# Query installed package
rpm -q package-name

# Verify package integrity
rpm -Vf /path/to/file
```

**rpm options for install:**
- `-i` install
- `-v` verbose
- `-h` show progress with hash marks

## yum
High-level package manager for RPM-based systems. Resolves dependencies automatically. Equivalent of `apt` for Red Hat/CentOS systems.

```bash
# Install a package
sudo yum install package-name

# Remove a package
sudo yum remove package-name

# Update a specific package
sudo yum update package-name

# Update all packages
sudo yum update

# List configured repositories
yum repolist

# Find which package provides a command
yum provides scp
```

**Always confirm the transaction summary** before proceeding with yum install or update — review what will be installed or changed.

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

## runlevel
Displays the previous and current runlevel of the system.

```bash
runlevel
# → N 5   (N = no previous runlevel, 5 = current runlevel)
```

## systemctl get-default
Displays the current default systemd target — the mode the system boots into.

```bash
systemctl get-default
# → graphical.target   (boots to GUI)
# → multi-user.target  (boots to command line)
```

## systemctl set-default
Changes the default systemd target — takes effect on next reboot.

```bash
# Switch to command line mode (server standard)
sudo systemctl set-default multi-user.target

# Switch back to graphical mode
sudo systemctl set-default graphical.target
```
