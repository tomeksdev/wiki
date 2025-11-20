---
title: Secrets Rotation Playbook
section: architecture
parent_shelf: server-platform
category: Runbook
author: Platform Team
summary: Hands-on runbook for rotating credentials managed in Vault.
read_time: 7
date: 2025-05-05
---
## Rotation cadence
| Secret | TTL | Owner |
| --- | --- | --- |
| Database credentials | 7d | DBA |
| API tokens | 30d | Platform |
| TLS certificates | 60d | Security |

## Procedure
1. Pause dependent jobs (documented in `ops/calendar.md`).
2. Trigger rotation workflow via Vault UI or `vault write` command.
3. Watch the automation pipeline update consuming services.
4. Confirm health checks pass for 10 minutes before closing the change.

## Rollback
- Restore the previous version from Vault version history.
- Redeploy affected workloads with the restored secret.
- File a retrospective if rollback is triggered.
