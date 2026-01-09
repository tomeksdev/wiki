---
title: Installation Steps
shelf_id: wireguard-install
nav_id: wireguard-install
nav_title: WireGuard Install
nav_icon: fa-solid fa-shield-halved
category: Guides
summary: Install and manage the WireGuard GUI installer project.
author: Vujca
order: 1
project_id: wireguard-gui
date: 2024-05-24
---
### Requirements

- A Debian-based Linux distribution (e.g. Ubuntu, Debian).
- Root/sudo access.
- Internet connection.

### Installation Steps

```
wget https://github.com/tomeksdev/wireguard-install-with-gui/releases/download/v1.0.0/wg-server-install.tar.gz
tar -xzvf wg-server-install.tar.gz
chmod +x wireguard-server-inst.sh
sudo ./wireguard-server-inst.sh
```

The script will:
- Install required packages (e.g. `wireguard`, `wireguat-ui`, `curl` and `tar`).
- Set up the WireGuard server.
- Make changes in `sysctl.conf` for IPv4/IPv6
- Create services and wireguar UI start script
