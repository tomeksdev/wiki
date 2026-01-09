---
title: Step 3 - Run the Script
parent_shelf: email-to-issue-inst
project_id: email-to-issue
category: Setup
summary: Update your config to send issues to a different GitHub repo.
author: Vujca
order: 3
date: 2025-05-15
---
### 1. Run the Script

   Execute the script using Python:

   ```bash
   python email-to-issue.py
   ```

   The script will:
   - Fetch unread emails from the configured inbox.
   - Process the subject and body to clean up signatures and extract relevant information.
   - Create GitHub issues using the GitHub API and attach files from the email (if any).

### 2. Monitor the Log File

   Check the `email_to_issue.log` file for logs related to issue creation, including any errors or issues that might have occurred during execution.

### Optional:

   - Use **cron** for simple, scheduled execution
   - Use **systemd** for long-running, resilient services

1. Crontab:

   Open your user’s crontab editor

   ```bash
   crontab -e
   ```

   The following example runs the script every 5 minutes

   ```bash
   */5 * * * * /usr/bin/python3 /full/path/email-to-issue.py >> /var/log/email-to-issue.log 2>&1
   ```

   Explanation:
   - */5 * * * * → run every 5 minutes
   - /usr/bin/python3 → full path to the Python interpreter
   - /full/path/email-to-issue.py → full path to the script
   - >> /var/log/email-to-issue.log → append output to a log file
   - 2>&1 → redirect errors to the same log file

2. Systemd:

   Create a systemd service file

   ```bash
   sudo nano /etc/systemd/system/email-to-issue.service
   ```

   Add the following configuration

   ```ini
   [Unit]
   Description=Email to GitHub Issue Service
   After=network.target

   [Service]
   ExecStart=/usr/bin/python3 /full/path/email-to-issue.py
   WorkingDirectory=/full/path
   Restart=always
   User=yourusername
   EnvironmentFile=/full/path/.env

   [Install]
   WantedBy=multi-user.target
   ```
   
   Reload systemd and enable the service

   ```bash
   sudo systemctl daemon-reload
   sudo systemctl enable email-to-issue
   sudo systemctl start email-to-issue
   ```

   View logs

   ```bash
   journalctl -u email-to-issue -f
   ```