---
title: Backup Strategy
section: architecture
shelf_id: backup
category: Infrastructure
author: Vujca
summary: Retention tiers and media rotation for all managed services.
read_time: 4
date: 2025-04-19
tags:
  - backup
  - dr
---
## Scope
- VM snapshots nightly with 14 day retention
- Database PITR with 7 day history stored in object storage
- NAS incremental backup every 2 hours to secondary site

## Validation
1. Weekly restore test of one VM chosen at random
2. Monthly tabletop exercise that includes database recovery

## Media rotation
Tape copy is written every Friday and shipped off-site on Monday.
