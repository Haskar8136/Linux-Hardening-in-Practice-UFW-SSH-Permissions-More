# Installation – UFW & Basic Setup

## 1. Update Your System
Before installing anything, make sure your package list is up to date.

```bash
sudo apt update && sudo apt upgrade -y   # Debian/Ubuntu/Kali
# or
sudo pacman -Syu                          # Arch
# or
sudo dnf update                           # Fedora
```
# 2. Install UFW
Debian / Ubuntu / Kali
```bash

sudo apt install ufw -y
```
Arch Linux
```bash

sudo pacman -S ufw
```
Fedora
```bash

sudo dnf install ufw 
```

Verify installation
```bash

ufw version
```
# 3. Set Default Policies
Before enabling UFW, define the default behavior:
```bash

sudo ufw default deny incoming
sudo ufw default allow outgoing
```
This blocks everything incoming unless explicitly allowed, while letting your system reach the internet normally.
# 4. Allow SSH (Critical – Don’t Skip)

If you’re connected remotely, allow SSH before enabling the firewall:
```bash

sudo ufw allow ssh
# or, if you use a custom port:
sudo ufw allow 2222/tcp
```
# 5. Enable UFW
```bash

sudo ufw enable
```
you should see:
Firewall is active and enabled on system startup
# 6. Check Status
```bash
sudo ufw status verbose
```
Expected output (example):
```bash
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing)
New profiles: skip

To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
```
