# Phishing URL Analyzer in Python

This project provides a simple Python script that scans email text for URLs, checks each URL with the VirusTotal API, and prints a JSON report to the terminal. It also saves the report to a file for later review.

---

## What Is It?

Phishing emails often hide links to malicious sites. This script reads an email from a text file, finds all URLs, and asks VirusTotal whether any security vendors flag those links as malicious. It’s a quick way to triage suspicious messages.

---

## How It Works

The script:

1. Reads email content from `emails.txt`  
2. Uses a regex to extract all URLs  
3. Submits each URL to VirusTotal (v3 API) and retrieves an analysis result  
4. Counts how many engines flagged the URL as malicious  
5. Prints a report and saves it to `phishing_report.json`  
6. Logs actions and errors to `script.log`

**Output example (trimmed):**
```json
{
  "Scanned URLs": [
    { "url": "http://example.com/login", "malicious_detections": 3 }
  ],
  "Timestamp": "2025-08-11 14:20:31"
}
```

---

## Getting Started

### Requirements

- Python 3  
- `requests` library

Install dependencies:
```bash
pip install requests
```

---

## Setup

1. **Add your VirusTotal API key**  
   Open the script and set:
   ```python
   VIRUSTOTAL_API_KEY = "YOUR_API_KEY_HERE"
   ```

2. **Create the email input file**  
   Put the raw email text (or paste the body) into `emails.txt`.  
   Example:
   ```
   Subject: Invoice

   Please review your invoice:
   http://example.com/invoice?id=123
   ```

---

## Running the Program

From the project directory:
```bash
python phishing_url_analyzer.py
```

You’ll see the report in the terminal and a saved file:
- `phishing_report.json` – the JSON report  
- `script.log` – log details and errors

---

## Files

- `phishing_url_analyzer.py` – main script  
- `emails.txt` – input email text (you create this)  
- `phishing_report.json` – generated report  
- `script.log` – run logs

---

## Notes and Limits

- **VirusTotal rate limits** apply to your API key  
- Results depend on available analysis data; a clean result doesn’t guarantee safety  
- The script sends URLs to VirusTotal; review your organization’s data handling policy before use  
- For large mailboxes or multi-email scans, extend the script to loop over files or directories  
- The script performs a single analysis fetch per URL; adding a short poll/retry loop can improve freshness of results

---
