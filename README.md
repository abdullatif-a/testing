[![.github/workflows/smtp.yml](https://github.com/abdullatif-a/testing/actions/workflows/smtp.yml/badge.svg)](https://github.com/abdullatif-a/testing/actions/workflows/smtp.yml)

# GitHub Action: Email Notification via SMTP

This GitHub Action sends an email using the `dawidd6/action-send-mail` GitHub Action and Gmail's SMTP server.

## Features

- Sends email via SMTP
- Configurable using GitHub Secrets
- Can be triggered manually or on a schedule

---

## 📌 Setup Guide for Beginners

### 1. Fork or Clone This Repository

You can use this workflow in your own repository by creating a new file at:.github/workflows/email.yml

Then paste the workflow code below.

---

### 2. Create GitHub Secrets

To keep your email credentials and message secure, store them as GitHub Secrets.

Go to your repository:

**Settings > Secrets and variables > Actions > New repository secret**

Add the following secrets:

| Secret Name       | Example Value              | Description                         |
|-------------------|----------------------------|-------------------------------------|
| `EMAIL_USER`      | `yourname@gmail.com`       | Gmail address (sender)              |
| `EMAIL_PASS`      | `abcd efgh ijkl mnop`      | Gmail App Password (see below)      |
| `EMAIL_USER2`     | `recipient@example.com`    | Receiver's email address            |
| `SUBJECT`         | `Automated Notification`   | Email subject                       |
| `BODY`            | `Hello, this is a test.`   | Email body message                  |

🔐 Learn how to add secrets here:  
👉 [GitHub Docs: Encrypted secrets](https://docs.github.com/en/actions/security-guides/encrypted-secrets)

#### 📌 Gmail App Passwords

If you use Gmail with 2-Step Verification, you'll need to create an **App Password** instead of your actual password.

Steps:
1. Visit [https://myaccount.google.com/apppasswords](https://myaccount.google.com/apppasswords)
2. Select **Mail** as the app and **Other** as the device.
3. Copy the generated 16-character password.
4. Paste it into GitHub as the value for `EMAIL_PASS`.

---

### 3. Workflow Example

```yaml
on:
  workflow_dispatch:
  # schedule:
  #   - cron: '*/5 * * * *'  # Uncomment to run every 5 minutes

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: Send Email via SMTP
        uses: dawidd6/action-send-mail@v2
        with:
          server_address: smtp.gmail.com
          server_port: 465
          username: ${{ secrets.EMAIL_USER }}
          password: ${{ secrets.EMAIL_PASS }}
          subject: ${{ secrets.SUBJECT }}
          body: ${{ secrets.BODY }}
          to: ${{ secrets.EMAIL_USER2 }}
          from: ${{ secrets.EMAIL_USER }}


