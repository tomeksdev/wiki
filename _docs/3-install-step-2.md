---
title: Step 2 - How to Customize
parent_shelf: email-to-issue-inst
project_id: email-to-issue
category: Setup
summary: Update your config to send issues to a different GitHub repo.
author: Vujca
order: 2
date: 2025-05-15
---
### 1. Configure Label Map

   The script allows you to map keywords from email subjects to GitHub issue labels. You can configure the `LABEL_MAP` in the `.env` file or modify it directly in the script:

   ```env
   LABEL_MAP="[configure]:configure,[edit]:edit,[invalid]:invalid,[question]:question,[write post]:write-post"
   ```

   Each key-value pair in `LABEL_MAP` should be separated by commas. The key is the subject keyword (e.g., "[configure]") and the value is the corresponding GitHub label (e.g., "configure").

### 2. Configure Signature Cleaning Triggers
   The script supports cleaning email signatures. By default, it removes common signature patterns (like "Best regards," "Thanks," etc.). You can extend these patterns by adding custom triggers in the `signature_triggers.txt` file:

   ```signature_triggers.txt
   (?i)^best regards
   (?i)^kind regards
   (?i)^thanks
   (?i)^regards
   (?i)^sincerely
   (?i)^cheers
   (?i)^--$
   (?i)^sent from my
   (?i)^email:
   (?i)^internet:
   (?i)^[a-zA-Z\s]{2,30}$
   (?i)administrator|manager|engineer|director|coordinator|officer|developer|consultant
   ```