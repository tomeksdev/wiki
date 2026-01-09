---
title: Step 3 - Server Interface Configuration
parent_shelf: wireguard-gui-configuration
project_id: wireguard-gui
category: Setup
summary: Server Interface Configuration
author: Vujca
order: 3
date: 2024-05-24
---
In the **WireGuard Interface** section:

- **Server Interface Addresses:** Enter a private IP with a subnet (e.g., `10.0.0.1/24`). This will be the VPN server’s internal IP.
- **Listen Port:** Set to `443` to avoid port blocks on restrictive networks.

**Post Up Script:**
```bash
iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o ens192 -j MASQUERADE
```

**Post Down Script:**
```bash
iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o ens192 -j MASQUERADE
```

These scripts handle firewall rules and routing.

![Server Settings](https://tomeksdev.com/assets/img/post/wireguard/server-settings.png)