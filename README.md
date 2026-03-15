#  UFW Guide: Master the Linux Firewall

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Linux](https://img.shields.io/badge/Platform-Linux-orange)](https://www.kernel.org)
[![UFW](https://img.shields.io/badge/Firewall-UFW-blue)](https://help.ubuntu.com/community/UFW)

A **practical, no-fluff guide** to mastering UFW (Uncomplicated Firewall) on Linux.  
Perfect for beginners and a solid reference for pros.

---

## What's Inside

| File | Description |
|------|-------------|
| [`01-installation.md`](01-installation.md) | Install UFW on any major distro |
| [`02-basic-commands.md`](02-basic-commands.md) | Essential commands you'll use daily |
| [`03-advanced-rules.md`](03-advanced-rules.md) | Rate limiting, port ranges, app profiles |
| [`04-monitoring.md`](04-monitoring.md) | Logs, real-time monitoring, traffic analysis |
| [`05-troubleshooting.md`](05-troubleshooting.md) | Fix common issues (SSH lockout, conflicts) |
| [`06-practical-examples.md`](06-practical-examples.md) | Real-world setups (servers, home PCs, nodes) |

---

## Why This Guide?

I wrote this after configuring UFW on production servers, Monero nodes, and my own machines.  
No theory. Just **what actually works**.

You'll learn how to:

-  Secure a Linux box in 5 minutes
-  Block attackers and bots
-  Monitor who's knocking on your ports
-  Never lock yourself out again

---

## Tested On

- Ubuntu 22.04 / 24.04  
- Debian 12  
- Kali Linux  
- Raspberry Pi OS  
- Arch (btw)

---

## Prerequisites

- A Linux machine (physical or VPS)  
- `sudo` access  
- 5 minutes of focus  

---

## Quick Start (tl;dr)

```bash
sudo apt update && sudo apt install ufw -y          # Debian/Ubuntu
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow ssh                                   # Or port 22
sudo ufw enable
