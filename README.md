# Phishing URL Detector & Incident Tracker

This repository hosts an **n8n workflow** that detects malicious or suspicious URLs from incoming emails and tracks incidents. The workflow receives emails (via webhook or IMAP), extracts URLs from the message content, scans them using the VirusTotal URL API, categorizes each URL, and updates a Google Sheets incident tracker. High‑risk URLs trigger a notification to Slack (or Microsoft Teams), and optionally you can feed the result into a blocklist service.

## Features

- Accepts inbound emails through a Webhook or email trigger
- Parses email content to extract all embedded URLs
- Scans each URL with the VirusTotal URL Scan API
- Categorizes URLs as **clean**, **suspicious**, or **malicious** based on detections
- Appends details of malicious URLs to a Google Sheets incident log
- Sends a real‑time alert to a Slack channel for high severity detections
- Modular and extensible for additional actions (e.g. automatic blocklist updates)

## Getting Started

1. Copy `.env.sample` to `.env` and populate it with your API keys and credentials.
2. Follow `agent_playbook.md` to construct the workflow in n8n.
3. Connect your email provider, Slack workspace, and Google Sheets account in n8n.
4. Test with sample phishing emails and verify logs and notifications.

## Files

- **agent_playbook.md** – a detailed guide for building the workflow in n8n.
- **.env.sample** – environment variable definitions.
- **diagram.md** – Mermaid diagram of the workflow.
- **samples.json** – example input email and classification output.
- **LICENSE** – MIT License.
