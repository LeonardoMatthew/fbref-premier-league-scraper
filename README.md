# 📊 FBref Premier League Match Data Scraper

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![Scraping Framework](https://img.shields.io/badge/library-Selenium%20%2B%20Cloudscraper-orange.svg)](https://github.com/VeNoMouS/cloudscraper)

A production-grade Python scraper engineered to extract match-level Premier League statistics. This tool specifically targets **FBref**, overcoming advanced anti-bot protections and non-standard HTML table structures through a multi-layered scraping strategy.

---

## 🔍 Project Overview

Scraping football data from FBref is a significant technical challenge. This project uses a **Hybrid Selenium-Cloudscraper Architecture** to solve common scraping blockers:

* **Cloudflare Bypassing:** Uses `cloudscraper` to handle V2/V3 challenges.
* **Dynamic Rendering:** Employs Selenium (headless Chrome) to process JavaScript-heavy standings pages.
* **Hidden Data Extraction:** Uses Regex to "uncomment" tables hidden within HTML comments (``).
* **Schema Evolution:** Implements a "Smart Mapping" system to handle column names that change between seasons (e.g., "Shots" vs "Sh").



---

## ⚙️ Key Engineering Features

* ✅ **Hybrid Driver Logic:** Selenium handles the navigation and JavaScript rendering, while Cloudscraper handles the high-volume data requests.
* ✅ **Resilient Networking:** Features exponential backoff retry logic and randomized User-Agent rotation to prevent IP blacklisting.
* ✅ **Smart Column Matching:** A candidate-based matching system ensures that data is captured even if FBref renames table headers.
* ✅ **Automated Data Pipeline:** 1. Scrapes league standings for team URLs.
    2. Navigates to individual team match logs.
    3. Merges standard match data with advanced shooting metrics.
* ✅ **Fail-Safe Mechanism:** Includes an **Autosave** feature that updates a partial backup CSV after every team is scraped.

---

## 🧠 Technical Highlights

### 1. Handling "Hidden" HTML
FBref wraps many performance tables in comments to prevent standard scraping. This project uses a regex-based helper to reconstruct the DOM:
```python
def uncomment_tables(html_text):
    pattern = re.compile(r"")
    return pattern.sub(lambda m: m.group(1), html_text)

