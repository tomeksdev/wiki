---
title: SSH Hardening Snippets
section: snippets
shelf_id: ssh-hardening
category: Utilities
author: Vujca
summary: Collection of go-to snippets for SSH daemon lockdown and troubleshooting.
read_time: 3
date: 2025-04-30
tags:
  - snippets
  - ssh
---
## Disable legacy algorithms
```bash
KexAlgorithms curve25519-sha256@libssh.org,diffie-hellman-group16-sha512
Ciphers chacha20-poly1305@openssh.com,aes256-gcm@openssh.com
MACs hmac-sha2-512-etm@openssh.com,hmac-sha2-256-etm@openssh.com
```

## Troubleshooting slow logins
- `sshd -T | grep banner`
- `journalctl -u sshd -b`
- `sudo ssh -vvv user@host` to inspect handshake
