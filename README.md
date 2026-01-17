# 📊 FBref Premier League Match Data Scraper

[![Python Version](https://img.shields.io/badge/python-3.8%2B-blue.svg)](https://www.python.org/)
[![Scraping Framework](https://img.shields.io/badge/library-Selenium%20%2B%20Cloudscraper-orange.svg)](https://github.com/VeNoMouS/cloudscraper)

A production-grade Python scraper engineered to extract match-level Premier League statistics.  
This tool specifically targets **FBref**, overcoming advanced anti-bot protections and non-standard HTML table structures through a multi-layered scraping strategy.

---

## 🔍 Project Overview

Scraping football data from FBref is a significant technical challenge.  
This project uses a **Hybrid Selenium–Cloudscraper Architecture** to solve common scraping blockers:

- **Cloudflare Bypassing:** Uses `cloudscraper` to handle V2/V3 challenges.
- **Dynamic Rendering:** Employs Selenium (headless Chrome) to process JavaScript-heavy standings pages.
- **Hidden Data Extraction:** Uses regex to reconstruct tables hidden inside HTML comments.
- **Schema Evolution:** Implements smart column mapping to handle renamed statistics across seasons.

---

## ⚙️ Key Engineering Features

- ✅ **Hybrid Driver Logic**  
  Selenium handles navigation and JavaScript rendering, while Cloudscraper handles high-volume requests.

- ✅ **Resilient Networking**  
  Exponential backoff retry logic and randomized User-Agent rotation reduce blocking risk.

- ✅ **Smart Column Matching**  
  Candidate-based matching system adapts automatically to renamed FBref columns.

- ✅ **Automated Data Pipeline**
  1. Scrapes league standings for team URLs  
  2. Navigates to individual team match logs  
  3. Merges standard match data with advanced shooting metrics  

- ✅ **Fail-Safe Mechanism**  
  Autosave updates a partial backup CSV after every team scrape.

---

## 🧠 Technical Highlights

### 1. Handling "Hidden" HTML

FBref wraps many performance tables inside HTML comments to block standard scraping.

This project reconstructs the DOM using a regex-based helper:

```python
def uncomment_tables(html_text):
    pattern = re.compile(r"<!--\s*(<table[\s\S]*?</table>)\s*-->")
    return pattern.sub(lambda m: m.group(1), html_text)
```

### 2. Defensive Measures
To ensure long-running stability, the scraper includes:

Headless Chrome Optimization: Configured with --no-sandbox and --disable-gpu for efficient server-side performance.

Request Throttling: Randomized sleep intervals to mimic human browsing behavior.

### 🧪 Tech Stack

| Category        | Tools                       |
| --------------- | --------------------------- |
| Language        | Python 3.x                  |
| Automation      | Selenium, WebDriver Manager |
| Bypass          | Cloudscraper                |
| Parsing         | BeautifulSoup4, LXML        |
| Data Processing | Pandas, NumPy               |

### ▶️ Getting Started
## 1. Installation

git clone https://github.com/yourusername/fbref-scraper.git
cd fbref-scraper
pip install -r requirements.txt

