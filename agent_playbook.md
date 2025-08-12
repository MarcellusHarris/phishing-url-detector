# Agent Playbook for Phishing URL Detector & Incident Tracker

Use this guide to build the **Phishing URL Detector** workflow in n8n.

## Prerequisites

- An n8n instance.
- Access to an email account or webhook to receive messages.
- A VirusTotal API key.
- Slack and Google Sheets credentials.

## Steps

1. **Create a new workflow** named `Phishing URL Detector`.
2. **Trigger**:
   - Use a **Webhook node** if you plan to send emails into n8n via HTTP POST.
   - Or use an **IMAP Email Read node** configured with your email credentials to fetch incoming emails periodically.
3. **Extract URLs**:
   - Add a **Function node** that parses the email body (plain text and HTML) and extracts all URLs using a regular expression.
   - Output an array of URLs for further processing.
4. **Scan URLs**:
   - Use an **HTTP Request node** to call `https://www.virustotal.com/api/v3/urls` with your `VIRUSTOTAL_API_KEY`.
   - For each URL, obtain the scan results (number of detections, last analysis date, etc.).
5. **Categorize**:
   - Add a **Function node** to categorize each URL as *clean* (0 detections), *suspicious* (1‑2 detections), or *malicious* (3 or more detections).
6. **Log incidents**:
   - For URLs categorized as *malicious*, add a **Google Sheets node** to append a row to an incident tracker sheet with columns such as `URL`, `Category`, `Detections`, and `Timestamp`.
7. **Send alerts**:
   - Also for malicious URLs, configure a **Slack node** to post an alert message to your security channel.
8. **Optional blocklist**:
   - If you use an external blocklist or firewall, add an HTTP or custom node to update that list with the malicious URLs.
9. **Export** the workflow to `workflow.json` once you have tested it successfully.
10. **Commit and push** all files in this directory to your GitHub repository.

## Notes

- Ensure your email trigger is secured (e.g. using authentication for webhooks).
- Adjust detection thresholds as appropriate for your organisation.
- See `diagram.md` for a high‑level diagram of the workflow.
