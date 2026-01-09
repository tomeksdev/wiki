---
title: Step 1 - Installation
parent_shelf: email-to-issue-inst
project_id: email-to-issue
category: Setup
summary: Follow these steps to get the project set up locally
author: Vujca
order: 1
date: 2025-05-15
---
### 1. **Clone the Repo**
   ```bash
   git clone https://github.com/tomeksdev/Emails-To-Issue.git
   cd Emails-To-Issue
   ```

### 2. **Install Python (if not installed)**
   Make sure you’re running Python 3.8+.

   **Debian / Ubuntu**
   ```bash
   sudo apt update
   sudo apt install -y python3 python3-pip
   ```

   **RHEL / CentOS / Rocky / AlmaLinux**
   ```bash
   sudo dnf install -y python3 python3-pip
   ```

   **Arch Linux**
   ```bash
   sudo pacman -S python python-pip
   ```

### 3. **Create a Virtual Environment (optional but recommended)**
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # macOS/Linux
   venv\Scripts\activate     # Windows
   ```

### 4. **Install Dependencies**
   ```bash
   pip install -r requirements.txt
   ```
   Dependencies:
   - `requests`
   - `python-dotenv`
   - `imaplib`
   - `email`
   - `re`
   - `talon` (for signature extraction, optional)
   - `logging`

### 5. **Configure Environment Variables**
   Typically you will need:
   - GitHub personal access token  
   - Mailbox credentials (IMAP or API)  
   - GitHub repository to create issues in

   These go into a `.env` file or environment variables based on the script’s instructions.

   ```env
   IMAP_SERVER=your.imap.server.com
   EMAIL_ACCOUNT=your-email@example.com
   EMAIL_PASSWORD=your-email-password
   GITHUB_REPO=your-username/your-repository
   GITHUB_TOKEN=your-github-personal-access-token
   ```

### 6. **Save and verify the config file**
   Double-check that your keys, passwords, and repo names are correct.