---
title: Network Segmentation Model
section: architecture
parent_shelf: security-controls
category: Security Pattern
author: Vujca
summary: Zones, trust levels, and enforcement tooling for the core infrastructure network.
read_time: 10
date: 2025-04-25
---
## Zones
- Tier 0: identity, secrets, and hypervisor services
- Tier 1: control plane tooling (CI/CD, Git, automation)
- Tier 2: workloads and supporting databases

## Enforcement
1. VXLAN EVPN fabric extends VRFs down to the access layer.
2. Firewalls publish policy via Infra-as-Code repo and compile to Panorama.
3. Network ACLs mirrored into AWS/GCP security groups for hybrid workloads.

## Change management
- Pull request template requires business justification.
- Automated policy simulation runs with Batfish before a commit merges.
