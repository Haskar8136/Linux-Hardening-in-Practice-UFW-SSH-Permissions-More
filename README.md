  ╔════════════════════════════════════════════════════════╗
  ║                                                        ║
  ║   ██╗  ██╗ █████╗ ███████╗██╗  ██╗ █████╗ ██████╗      ║
  ║   ██║  ██║██╔══██╗██╔════╝██║ ██╔╝██╔══██╗██╔══██╗     ║
  ║   ███████║███████║███████╗█████╔╝ ███████║██████╔╝     ║
  ║   ██╔══██║██╔══██║╚════██║██╔═██╗ ██╔══██║██╔══██╗     ║
  ║   ██║  ██║██║  ██║███████║██║  ██╗██║  ██║██║  ██║     ║
  ║   ╚═╝  ╚═╝╚═╝  ╚═╝╚══════╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝  ╚═╝     ║
  ║                                                        ║
  ║   📚  UFW GUIDE: MASTER THE LINUX FIREWALL             ║
  ║                                                        ║
  ╚════════════════════════════════════════════════════════╝

---

[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
![Linux](https://img.shields.io/badge/Platform-Linux-orange)
![UFW](https://img.shields.io/badge/Firewall-UFW-blue)

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

---

## Why This Guide?

I wrote this after configuring UFW on production servers, **Monero nodes**, and my own machines.  
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
```

Done. Your server is now **90% safer**.

---

## How to Use This Guide

1. Start with [`01-installation.md`](01-installation.md)
2. Master the basics in [`02-basic-commands.md`](02-basic-commands.md)
3. Dive deeper in [`03-advanced-rules.md`](03-advanced-rules.md)
4. Monitor everything with [`04-monitoring.md`](04-monitoring.md)

---

## Contributing

Found a bug? A better way to explain something?  
Open an issue or a pull request. All help is welcome.

---

## Contact

Created by [**haskar**](https://github.com/Haskar8136) — if this helped you, **star the repo** ⭐

---

## License

MIT — use it, share it, improve it.
