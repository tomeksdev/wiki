---
title: Automation Platform
section: project-doc
shelf_id: automation-platform
category: Delivery
author: Vujca
summary: Documentation for the shared Ansible + Terraform automation stack.
read_time: 5
date: 2025-03-13
tags:
  - automation
---
## Stack
- Terraform with remote state in S3 compatible bucket
- Ansible execution via AWX with RBAC synced from LDAP

## Pipelines
1. Pull request -> Terraform plan posted as status check
2. Merge -> apply job triggered with manual approval step

## Support
PagerDuty service: `Platform-Automation`
