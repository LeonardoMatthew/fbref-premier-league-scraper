# 📊 FBref Premier League Match Data Scraper

A robust Python web-scraping project built to collect **Premier League match-level data across multiple seasons** from FBref — a website known for **Cloudflare protection, dynamic page loading, and hidden HTML tables**.

This project uses a **hybrid scraping approach** combining Selenium and Cloudsraper to reliably extract football statistics that cannot be accessed using simple request-based methods.

---

## 🔍 Project Overview

FBref is one of the most widely used football statistics platforms, but scraping data from it is difficult due to:

- Cloudflare anti-bot protection  
- JavaScript-rendered pages  
- Tables hidden inside HTML comments  
- Column names that change across seasons  

This scraper was designed to handle all of these issues automatically and produce a **clean, structured dataset** suitable for analysis, visualization, or machine learning.

---

## ⚙️ Features

- ✅ Multi-season scraping (automatic season navigation)
- ✅ Hybrid scraping system (Selenium + Cloudsraper)
- ✅ Bypasses request blocking and rate limiting
- ✅ Extracts teams dynamically from standings tables
- ✅ Parses hidden HTML tables inside comments
- ✅ Handles renamed statistical columns across seasons
- ✅ Robust retry and timeout logic
- ✅ Randomized user agents and request delays
- ✅ Automatic backup saving during execution
- ✅ Final merged dataset exported as CSV

---

## 🧠 Why This Project Is Difficult

This is **not a basic scraping script**.

Several real-world problems had to be solved.

### 1. Anti-Bot & DDoS Protection

FBref limits repeated requests and uses Cloudflare protection.

To reduce blocking, this project uses:

- Multiple request methods  
  - Selenium (browser-based simulation)  
  - Cloudsraper (Cloudflare-aware requests)  
- Random user-agent rotation  
- Random sleep delays between requests  
- Retry logic with exponential backoff  

This allows the scraper to continue running even when some requests fail.

---

### 2. Loop-Based Crawling Logic

The scraper relies heavily on **for-loop based crawling**, similar to real data-collection pipelines:

- Loop through multiple seasons  
- Loop through all teams per season  
- Loop through match and shooting data  
- Merge statistics per team and season  

Each loop includes error handling so the program does not stop when a single page fails.

---

### 3. Hidden HTML Tables

FBref hides many important tables inside HTML comments:

```html
<!-- <table> ... </table> -->
