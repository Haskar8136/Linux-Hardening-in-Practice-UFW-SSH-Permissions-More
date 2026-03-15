# Monitoring – Watch Your Firewall in Action

Once UFW is running, you need to know what's happening. Who's knocking? What's being blocked? This guide shows you how to listen.

---

## Basic Status Checks

Quick overview:
```bash

sudo ufw status

```
Detailed view:
```bash

sudo ufw status verbose

```
Numbered rules (for easy deletion):
```bash

sudo ufw status numbered

```
## Understanding UFW Logs

UFW logs everything to:
```bash

/var/log/ufw.log

```
View the last 20 lines:
```bash

sudo tail -20 /var/log/ufw.log

```
Follow in real time:
```bash

sudo tail -f /var/log/ufw.log

```
## What a Blocked Connection Looks Like

Example log entry:
```

Mar 15 10:23:45 server kernel: [UFW BLOCK] IN=eth0 OUT= MAC=... SRC=45.13.179.5 DST=192.168.2.206 LEN=40 TOS=... PROTO=TCP DPT=22

```
What it means:
```
    SRC=45.13.179.5 → Attacker IP

    DPT=22 → Target port (SSH)

    [UFW BLOCK] → Connection was dropped

```
Top attacking IPs
```bash

sudo grep "UFW BLOCK" /var/log/ufw.log | awk '{print $12}' | cut -d= -f2 | sort | uniq -c | sort -nr | head -10

```
Most attacked ports
```bash

sudo grep "UFW BLOCK" /var/log/ufw.log | awk '{print $14}' | cut -d= -f2 | sort | uniq -c | sort -nr | head -10

```
## Simple Monitoring Script

Create a file monitor-ufw.sh:
```bash
#!/bin/bash

# Simple UFW monitor - shows recent blocks

echo "📊 UFW Block Monitor - Last 60 seconds"
echo "----------------------------------------"

while true; do
    clear
    echo "$(date)"
    echo ""
    echo "🔴 Top attackers in last 60s:"
    sudo journalctl --since "60 seconds ago" | grep "UFW BLOCK" | awk '{print $12}' | cut -d= -f2 | sort | uniq -c | sort -nr | head -5
    
    echo ""
    echo "🎯 Top targeted ports:"
    sudo journalctl --since "60 seconds ago" | grep "UFW BLOCK" | awk '{print $14}' | cut -d= -f2 | sort | uniq -c | sort -nr | head -5
    
    sleep 5
done

```
Make it executable and run:
```bash

chmod +x monitor-ufw.sh
./monitor-ufw.sh

```
## Traffic Volume Monitoring
Packets allowed vs blocked (summary)
```bash

sudo grep UFW /var/log/ufw.log | awk '{print $8}' | sort | uniq -c

```
Example output:
```text

  5432 [UFW ALLOW]
   876 [UFW BLOCK]

```
Bandwidth usage per IP (requires iptables)
```bash

sudo iptables -nvL -t filter

```
## Real-time Alerts (Desktop)

Install inotify-tools:
```bash

sudo apt install inotify-tools -y

```
Create ufw-alerts.sh:
```bash

#!/bin/bash
# Alert on new blocks

while inotifywait -e modify /var/log/ufw.log; do
    LAST_LINE=$(sudo tail -1 /var/log/ufw.log)
    if echo "$LAST_LINE" | grep -q "UFW BLOCK"; then
        IP=$(echo "$LAST_LINE" | grep -oP 'SRC=\K[0-9.]+')
        PORT=$(echo "$LAST_LINE" | grep -oP 'DPT=\K[0-9]+')
        notify-send "🚫 UFW Blocked" "IP $IP tried to access port $PORT"
    fi
done

```
Run in background:
```bash

chmod +x ufw-alerts.sh
./ufw-alerts.sh &

```
## Log Rotation (Optional)

UFW logs can grow large. Check rotation config:
```bash

sudo cat /etc/logrotate.d/ufw

```
If missing, create it:
```bash

sudo tee /etc/logrotate.d/ufw <<EOF
/var/log/ufw.log {
    rotate 7
    daily
    missingok
    notifempty
    compress
    delaycompress
    sharedscripts
    postrotate
        invoke-rc.d rsyslog reload >/dev/null 2>&1 || true
    endscript
}
EOF

```
## Export for Analysis

Save current stats to a file:
```bash

sudo grep "UFW BLOCK" /var/log/ufw.log > ufw-blocks-$(date +%Y%m%d).txt

```
Or parse with Python:
```python3

#!/usr/bin/env python3
import re
from collections import Counter

with open('/var/log/ufw.log') as f:
    logs = f.read()

ips = re.findall(r'SRC=([0-9.]+)', logs)
ports = re.findall(r'DPT=([0-9]+)', logs)

print("Top 10 attackers:")
for ip, count in Counter(ips).most_common(10):
    print(f"  {ip}: {count}")

print("\nTop 10 attacked ports:")
for port, count in Counter(ports).most_common(10):
    print(f"  {port}: {count}")

```
## What You've Learned

     Read and understand UFW logs

     Track attackers and targeted ports

     Build real-time monitors

     Create desktop alerts

     Export data for deeper analysis
