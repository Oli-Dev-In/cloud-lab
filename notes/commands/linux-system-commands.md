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