---
title: Step 4 - Add Clients
parent_shelf: wireguard-gui-configuration
project_id: wireguard-gui
category: Setup
summary: Adding Clients
author: Vujca
order: 4
date: 2024-05-24
---
Click on **“Wireguard Clients”** to begin adding new client devices.

![Client Add](https://tomeksdev.com/assets/img/post/wireguard/client-add.png)

---

Click **“+ New Client”** and fill in the form:

- **Name & Email:** Optional identification for the client.
- **IP Allocation:** Auto-assigns next available IP in the subnet.
- **Allowed IPs:** Define network access (avoid using `0.0.0.0/0` if not needed).
- **Extra Allowed IPs:** Leave blank for most devices. Use only when routing to subnets behind routers/firewalls (e.g., Mikrotik, OPNSense).

![New Client](https://tomeksdev.com/assets/img/post/wireguard/new-client.png)