[![.github/workflows/smtp.yml](https://github.com/abdullatif-a/testing/actions/workflows/smtp.yml/badge.svg)](https://github.com/abdullatif-a/testing/actions/workflows/smtp.yml)

# GitHub Action: Email Notification via SMTP

This GitHub Action sends an email notification using the `dawidd6/action-send-mail` action.

## Features

- Sends email using SMTP (Gmail in this example)
- Configurable via GitHub Secrets
- Can be triggered manually or scheduled

## Usage

### 1. Secrets Required

Add the following secrets to your repository:

| Secret Name       | Description                         |
|-------------------|-------------------------------------|
| `EMAIL_USER`      | Your Gmail address (sender)         |
| `EMAIL_PASS`      | App password for the sender email   |
| `EMAIL_USER2`     | Recipient email address             |
| `SUBJECT`         | Subject of the email                |
| `BODY`            | Body content of the email           |

> ⚠️ Note: Gmail requires you to use an [App Password](https://support.google.com/accounts/answer/185833) if 2FA is enabled.

### 2. Workflow Example

Save the following YAML as `.github/workflows/email.yml`:

```yaml
on:
  workflow_dispatch:
  # schedule:
  #   - cron: '*/5 * * * *'

jobs:
  notify:
    runs-on: ubuntu-latest
    steps:
      - name: testing github action smtp
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
