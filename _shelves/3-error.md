---
title: Troubleshooting
shelf_id: email-to-issue-error
nav_id: email-to-issue-error
nav_title: Troubleshooting
nav_icon: fa-solid fa-shield-halved
category: Scripts
summary: Follow these steps to get the project set up locally
author: Vujca
order: 2
project_id: email-to-issue
date: 2025-05-15
---
### 📍 Problem: No issues are being created
- Verify your GitHub token has permissions to create issues  
- Ensure the script actually sees new emails in the inbox  
- Check the logs for traceback detail

### 📍 Problem: Script crashes immediately
- Check syntax errors or missing packages  
- Run in debug mode or with elevated verbosity  
- Test importing modules manually

### 📍 Problem: Issues are created but empty
- Check the parsing logic — you may need to adapt it to how your emails are formatted  
- Print email parts before sending to GitHub to confirm content