#  Advanced UFW Rules – Go Beyond the Basics

Once you've mastered the basics, these rules give you fine-grained control over your firewall.

---

## Rate Limiting (Anti-Brute Force)

Prevent bots from hammering your SSH port:
```bash

sudo ufw limit ssh

```
This allows 6 connections per 30 seconds from the same IP. After that, connections are dropped.

You can also limit specific ports:
```bash

sudo ufw limit 2222/tcp

```
## Allow by Subnet

Allow an entire private network:
```bash

sudo ufw allow from 192.168.1.0/24

```
Allow a specific range to a specific port:
```bash

sudo ufw allow from 10.0.0.0/16 to any port 3306

```
## Allow by Network Interface

Useful for servers with multiple interfaces (e.g., VPN + public).

Allow all traffic on the internal interface:
```bash

sudo ufw allow in on eth1 to any

```
Allow SSH only on the internal interface:
```bash

sudo ufw allow in on eth1 to any port 22

```
## Application Profiles

UFW comes with predefined profiles for common services.

List available profiles:
```bash

sudo ufw app list

```
Enable a profile:
```bash

sudo ufw allow 'OpenSSH'
sudo ufw allow 'Apache Full'

```
View details of a profile:
```bash

sudo ufw app info 'Apache Full'

```
## Deny Outgoing Traffic (Strict Mode)

By default, outgoing traffic is allowed. To restrict it:
```bash

sudo ufw default deny outgoing

```
Then explicitly allow what you need:
```bash

sudo ufw allow out 53           # DNS
sudo ufw allow out 80/tcp       # HTTP
sudo ufw allow out 443/tcp      # HTTPS
sudo ufw allow out 123/udp      # NTP (time sync)

```
 !!Warning: This can break updates and connectivity. Test carefully.
## Comment Your Rules

Add comments so you remember why a rule exists:
```bash

sudo ufw allow 8080 comment 'Web app staging server'
sudo ufw allow from 192.168.1.0/24 to any port 22 comment 'Internal dev SSH'

```
View comments:
```bash

sudo ufw status numbered

```
## Before/After Scripting

You can combine UFW commands into scripts for quick deployment.

Example: setup-webserver.sh
```bash

#!/bin/bash
ufw allow ssh
ufw allow 80/tcp
ufw allow 443/tcp
ufw --force enable

```
## Advanced Monitoring
Count blocked packets per IP
```bash

sudo grep "UFW BLOCK" /var/log/ufw.log | awk '{print $12}' | cut -d= -f2 | sort | uniq -c | sort -nr

```
Real-time alerts (requires inotify-tools)
```bash

sudo apt install inotify-tools
while inotifywait -e modify /var/log/ufw.log; do
    tail -1 /var/log/ufw.log | grep "BLOCK" && notify-send "🚫 UFW Block" "$(tail -1 /var/log/ufw.log)"
done

```
## What You've Learned

     Rate limiting to stop brute force

     Rules by subnet and interface

     Application profiles

     Strict outgoing control

     Comments and scripting

     Advanced log analysis
