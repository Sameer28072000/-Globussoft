# 🛒 Amazon.in Laptop Scraper

A Python-based web scraper that extracts laptop listings from Amazon.in using **Selenium** and **BeautifulSoup**, and exports the results to a timestamped CSV file.

---

## 📦 Features

- Scrapes multiple pages of Amazon.in search results
- Extracts key product details: ASIN, title, price, rating, thumbnail image, and ad type
- Detects **Sponsored vs Organic** listings automatically
- Deduplicates results by ASIN across pages
- Saves output to a **timestamped CSV** in the `output/` folder
- Headless Chrome by default with anti-bot evasion settings
- Randomised sleep intervals to mimic human browsing behaviour
- Centralised CSS selector dictionary — easy to update when Amazon's layout changes

---

## 🗂️ Project Structure

```
Task_1_Webscraping/
├── amazon_scraper.py      ← Main scraper script
├── requirements.txt       ← Python dependencies
├── README.md              ← You're reading it
└── output/
    └── amazon_laptop_<timestamp>.csv
```

---

## 📋 Fields Extracted

| Field | Description |
|-------|-------------|
| `Title` | Full product name |
| `Price` | Listed price in ₹ |
| `Rating` | Star rating (e.g. `4.2`) |
| `Image` | Direct URL to the product thumbnail |
| `Ad_Type` | `Sponsored` or `Organic` |

---

## ⚙️ Installation

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd Task_1_Webscraping
```

### 2. Create and activate a virtual environment

```bash
# Create the virtual environment
python -m venv venv

# Activate it
# On Windows:
venv\Scripts\activate

# On macOS/Linux:
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

## 🚀 Usage

```bash
# Default — scrapes 3 pages for "laptop" in headless mode
python amazon_scraper.py

# Custom search query and page count
python amazon_scraper.py --query "gaming laptop" --pages 5

# Show the browser window (useful for debugging)
python amazon_scraper.py --no-headless
```

### Output

Results are saved to the `output/` folder with a timestamp:

```
output/amazon_laptop_20260604_125959.csv
```

---

## 🔧 How It Works

1. Launches Chrome (headless by default) with anti-bot configurations
2. Searches Amazon.in for the given query
3. For each page: scrolls to trigger lazy-loaded images → parses HTML with BeautifulSoup
4. Extracts title, price, rating, and image URL from each product card
5. Checks Amazon's sponsored badge labels to classify listings as `Sponsored` or `Organic`
6. Deduplicates entries by ASIN across all pages
7. Exports everything to a UTF-8 encoded, timestamped CSV

---

## 🛠️ Tech Stack

- **Python 3.x**
- [Selenium](https://selenium-python.readthedocs.io/) — browser automation
- [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/) — HTML parsing
- [webdriver-manager](https://github.com/SergeyPirogov/webdriver_manager) — automatic ChromeDriver management
- [pandas](https://pandas.pydata.org/) — CSV export

---

## 📝 Notes

- Amazon's HTML layout changes frequently. If selectors break, update SELECTORS in amazon_scraper.py — all selectors are centralised in one dictionary.
- Random sleep intervals are used between page loads to mimic human behaviour.
- Use --no-headless to visually debug what the browser is doing.

---
