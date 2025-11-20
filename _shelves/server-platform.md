---
title: Server Platform
section: architecture
shelf_id: server-platform
category: Infrastructure
author: Vujca
summary: Hardware standards, firmware cadence, and base OS for compute nodes.
read_time: 5
date: 2025-03-28
tags:
  - server
  - hardware
---
## Hardware SKUs
- Dell R750 for dense compute
- Supermicro SYS-620 for storage heavy workloads

## Firmware cadence
- Out-of-band BMC updates quarterly
- BIOS updates twice a year once validated in staging rack

## Base OS image
- AlmaLinux 9
- CIS level 1 hardening applied via Ansible baseline role
- Telemetry via node_exporter and osquery
