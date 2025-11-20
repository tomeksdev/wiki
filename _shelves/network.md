---
title: Network Fabric
section: architecture
shelf_id: network
category: Infrastructure
summary: Blueprint for core routing, segmentation, and observability of the on-prem network fabric.
author: Vujca
read_time: 6
date: 2025-05-01
tags:
  - network
  - architecture
---
## Topology
- Dual core switches with EVPN fabric
- Distribution layer collapsed in secondary rack for resiliency
- Access layer standardized on 1/10 GbE using PoE capable switches

## Change windows
All configuration pushes ride through the automation pipeline on Wednesdays 20:00 CET.

## Monitoring
- Netflow export toward Elastic stack
- SNMP alerts bridged into Alertmanager
- Continuous tests from Smokeping and synthetic ICMP loops
