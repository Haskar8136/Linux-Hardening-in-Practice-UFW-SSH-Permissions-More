# Basic UFW Commands – What You'll Use Every Day

Once UFW is installed and enabled, these are the commands you'll actually use. No fluff.

---

## Check Status

```bash

sudo ufw status

```
Shows a simple list of active rules.
```bash

sudo ufw status verbose

```
More details: default policies, logging level, etc.
```bash

sudo ufw status numbered

```
Shows rules with numbers — useful when you need to delete one.
## Allow Connections
```bash

sudo ufw allow 80                # Allow port 80 (HTTP)
sudo ufw allow 443/tcp            # Allow port 443 TCP (HTTPS)
sudo ufw allow ssh                 # Allow service by name (from /etc/services)
sudo ufw allow from 192.168.1.50   # Allow all traffic from a specific IP

```
Allow a port range
```bash

sudo ufw allow 6000:6007/tcp

```
## Deny Connections
```bash

sudo ufw deny 23                 # Deny port 23 (Telnet)
sudo ufw deny from 203.0.113.5   # Block all traffic from a specific IP

```
## Delete Rules
By exact command
```bash

sudo ufw delete allow 80

```
By rule number (safer)
```bash

sudo ufw status numbered
sudo ufw delete 3

```

## Enable / Disable / Reload
```bash

sudo ufw enable                   # Turn firewall on
sudo ufw disable                  # Turn firewall off (temporary)
sudo ufw reload                   # Reload rules without restart

```
## Reset Everything (Start Over)
```bash

sudo ufw reset

```
This disables UFW and deletes all rules. Useful when you mess up.

## Logging
```bash

sudo ufw logging on               # Enable logging (default: low)
sudo ufw logging medium            # More details
sudo ufw logging high              # Everything (can get noisy)

```
Logs are written to:
```bash

/var/log/ufw.log

```
Watch live:
```bash

sudo tail -f /var/log/ufw.log

```
## Quick Test – Allow Then Deny
```bash

sudo ufw allow 8080
sudo ufw status numbered
sudo ufw delete 1                  # Delete rule #1

```
