---
title: Security Controls
section: architecture
shelf_id: security-controls
category: Infrastructure
author: Vujca
summary: Network segmentation, secrets storage, and baseline hardening steps.
read_time: 7
date: 2025-02-15
tags:
  - security
---
## Segmentation
- Tier 0 admin ranges separated via VRF guard rails
- Prod workloads require mutual TLS with platform CA

## Secrets
- Vault cluster with auto-unseal
- Rotation policies: DB creds 7 days, API tokens 30 days

## Hardening
- CIS compliance scanner runs nightly
- Auditd shipped to Elastic via Filebeat
- EDR agent required before onboarding
