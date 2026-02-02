MN Domain AI Generator (Gemini + WHOIS)

A PHP web page that:

Generates exactly 20 .mn domain name ideas using Google Gemini

Checks each domain’s status using WHOIS

Displays per-domain status:

Available

Not available

Unknown (if WHOIS port is blocked by hosting)

Repository Structure
mn-domain-ai/
├── public_html/
│   └── domain_ai.php          # MAIN APP FILE
├── gemini_secrets.sample.php  # sample (commit this)
├── README.md
├── .gitignore

Where is domain_ai.php?

In GitHub: public_html/domain_ai.php

On your hosting server (shared hosting/cPanel): upload into your web root:

/home/USERNAME/public_html/domain_ai.php

Open in browser:

https://your-domain.com/domain_ai.php

Requirements

PHP 7.4+ (PHP 8.0+ recommended)

PHP extensions: curl, json

Outbound connection to WHOIS port 43

If port 43 is blocked by hosting, the app may show Unknown status

Installation (Shared Hosting / cPanel)
Step 1 — Upload the app

Upload:

public_html/domain_ai.php


to your hosting:

public_html/domain_ai.php

Step 2 — Add Gemini API key (IMPORTANT)

Do NOT store your API key inside public_html.

Create a file one level above public_html:

Example path:

/home/USERNAME/gemini_secrets.php


Content:

<?php
define('GEMINI_API_KEY', 'YOUR_GEMINI_API_KEY_HERE');


You can copy gemini_secrets.sample.php and rename it to gemini_secrets.php.

Step 3 — Open the app
https://your-domain.com/domain_ai.php


Enter a Mongolian case like:

машин зарын сайт

хувцасны дэлгүүр

барилгын компани

Then click Generate + Check WHOIS.

.mn WHOIS Configuration

This project is configured for .mn only.

Inside domain_ai.php, you will see something like:

const WHOIS_SERVER = 'whois.nic.mn';
const WHOIS_PORT = 43;


You can also tune:

const WHOIS_TIMEOUT_SEC = 4;
const WHOIS_CACHE_TTL = 600; // cache seconds (10 minutes)

Troubleshooting
Many domains show “Unknown”

Your hosting provider likely blocks outbound port 43 (WHOIS).
In that case the app cannot query WHOIS reliably.

Solutions:

Use a hosting/VPS that allows outbound port 43

Build a small proxy endpoint on a server where port 43 is open

Gemini API errors

401/403 → API key invalid or lacks permissions

404 → model name not available

429 → quota exceeded

Security Notes

Never commit gemini_secrets.php to GitHub

Rotate your API key if it was ever exposed

Keep WHOIS caching enabled to avoid rate-limits

GitHub Publish Steps
git init
git add .
git commit -m "Initial commit: .mn domain generator (Gemini + WHOIS)"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/mn-domain-ai.git
git push -u origin main
