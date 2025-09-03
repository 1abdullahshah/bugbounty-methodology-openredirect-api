# bugbounty-methodology-openredirect-api
My bug bounty automation project: testing open redirects &amp; API endpoints with bash + curl

# Starbucks Bug Bounty Methodology — Open Redirect & API Testing

**Purpose.**  
This repository documents an educational bug-bounty project where I built automation and testing scripts to explore open redirect behavior and API endpoint handling (500 / 401 responses). The goal is to show methodology, tooling, and lessons learned — not to publish or exploit sensitive data.

---

## 🔎 Summary
- Focus: automation for **open redirect detection** and **API behavior testing** (example endpoints: `/v1/login`, `/v1/me`).
- Key findings (example, responsibly disclosed to Starbucks via HackerOne):  
  - Open Redirect patterns found in `app.starbucks.com` (parameter: `returnUrl`).  
  - `openapi.starbucks.com` returned `500` for malformed login requests and `401` for unauthenticated requests — useful for learning input-validation and API-hardening topics.

---

## 📁 Files in this repo
- `starbucks_poc.txt` — example PoC output (curl results; sanitized).  
- `bounty_auto_filtered.sh` — filtered automation script (detects 500/401 on `openapi*` and checks redirects).  
- `starbucks_api_test.sh` — smaller script to test `/v1/login` and `/v1/me`.  
- `README.md` — this file.

---

## ▶️ How to run (local)
> Run these from a safe, authorized environment and only against in-scope targets.

```bash
# make scripts executable (one-time)
chmod +x bounty_auto_filtered.sh starbucks_api_test.sh

# run the main filtered scanner (saves findings to a results file)
./bounty_auto_filtered.sh

# run the single-endpoint tester and capture output
./starbucks_api_test.sh | tee starbucks_poc.txt

