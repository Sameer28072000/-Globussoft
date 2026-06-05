# 🐍 Python Projects Collection

A collection of Python mini-projects covering web scraping and computer vision.

---

## 📁 Repository Structure

```
├── Task_1_AmazonScraper/
│   ├── amazon_scraper.py
│   ├── requirements.txt
│   └── output/
│       └── amazon_laptop_<timestamp>.csv
│
└── Task_2_FaceAuthentication/
    ├── image_samples/
    ├── models/
    │   └── face_model.pkl
    ├── uploads/
    ├── venv/
    ├── .gitignore
    ├── app.py
    ├── predict.py
    ├── requirements.txt
    └── train.py
```

---

## 📌 Table of Contents

- [Task 1 — Amazon.in Laptop Scraper](#task-1--amazonin-laptop-scraper)
- [Task 2 — Face Authentication](#task-2--face-authentication)

---

## Task 1 — Amazon.in Laptop Scraper

A Python-based web scraper that extracts laptop listings from Amazon.in using **Selenium** and **BeautifulSoup**, and exports the results to a timestamped CSV file.

### 📦 Features

- Scrapes multiple pages of Amazon.in search results
- Extracts key product details: ASIN, title, price, rating, thumbnail image, and ad type
- Detects **Sponsored vs Organic** listings automatically
- Deduplicates results by ASIN across pages
- Saves output to a **timestamped CSV** in the `output/` folder
- Headless Chrome by default with anti-bot evasion settings
- Randomised sleep intervals to mimic human browsing behaviour
- Centralised CSS selector dictionary — easy to update when Amazon's layout changes

### 📋 Fields Extracted

| Field | Description |
|-------|-------------|
| `Title` | Full product name |
| `Price` | Listed price in ₹ |
| `Rating` | Star rating (e.g. `4.2`) |
| `Image` | Direct URL to the product thumbnail |
| `Ad_Type` | `Sponsored` or `Organic` |

### ⚙️ Setup

```bash
cd Task_1_AmazonScraper

# Create and activate virtual environment
python -m venv venv

# On Windows:
venv\Scripts\activate

pip install -r requirements.txt
```

> **Note:** Google Chrome must be installed on your system.
> ChromeDriver is managed automatically via `webdriver-manager`, or download manually from [chromedriver.chromium.org](https://chromedriver.chromium.org) — ensure it matches your Chrome version.

### 🚀 Usage

```bash
# Default — scrapes 3 pages for "laptop" in headless mode
python amazon_scraper.py

# Custom search query and page count
python amazon_scraper.py --query "gaming laptop" --pages 5

# Show the browser window (useful for debugging)
python amazon_scraper.py --no-headless
```

**Output** is saved to the `output/` folder with a timestamp:

```
output/amazon_laptop_20260527_143022.csv
```

### 🔧 How It Works

1. Launches Chrome (headless by default) with anti-bot configurations
2. Searches Amazon.in for the given query
3. For each page: scrolls to trigger lazy-loaded images → parses HTML with BeautifulSoup
4. Extracts title, price, rating, and image URL from each product card
5. Checks Amazon's sponsored badge labels to classify listings as `Sponsored` or `Organic`
6. Deduplicates entries by ASIN across all pages
7. Exports everything to a UTF-8 encoded, timestamped CSV

### 🛠️ Tech Stack

- **Python 3.x**
- [Selenium](https://selenium-python.readthedocs.io/) — browser automation
- [BeautifulSoup4](https://www.crummy.com/software/BeautifulSoup/) — HTML parsing
- [webdriver-manager](https://github.com/SergeyPirogov/webdriver_manager) — automatic ChromeDriver management
- [pandas](https://pandas.pydata.org/) — CSV export

### 📝 Notes

- Amazon's HTML layout changes frequently. If selectors break, update the `SELECTORS` dictionary in `amazon_scraper.py` — all selectors are centralised there for easy maintenance.
- Use `--no-headless` to visually debug what the browser is seeing during a scrape.

---

## Task 2 — Face Authentication

A **FastAPI** service that compares two face images using deep embedding similarity to verify whether they belong to the same person.

### 📦 Features

- REST API endpoint accepting two face images via a POST request
- Face detection and deep embedding extraction using **InsightFace**
- Cosine similarity comparison between the two embeddings
- Returns a verification result, similarity score, and bounding boxes for both images
- Interactive API explorer available at `/docs`

### 🔗 API Endpoint

**`POST /verify`**

**Sample Response:**

```json
{
  "verification_result": "same person",
  "similarity_score": 0.70,
  "bounding_box_image1": [x1, y1, x2, y2],
  "bounding_box_image2": [x1, y1, x2, y2]
}
```

### ⚙️ Setup

```bash
cd Task_2_FaceAuthentication

# Create and activate virtual environment
python -m venv venv

# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

pip install -r requirements.txt
```

### 🚀 Usage

```bash
# Train / initialise the face model
python train.py

# Start the FastAPI server
uvicorn app:app --reload
```

Then open the interactive API explorer in your browser:

```
http://127.0.0.1:8000/docs
```

### 🔧 How It Works

1. Two face images are submitted via `POST /verify`
2. **InsightFace** detects faces and extracts deep embeddings from each image
3. Cosine similarity is computed between the two embedding vectors
4. The API returns the verification result (`same person` / `different person`), the similarity score, and bounding boxes for both detected faces

### 🛠️ Tech Stack

- **Python 3.x**
- [FastAPI](https://fastapi.tiangolo.com/) — REST API framework
- [InsightFace](https://github.com/deepinsight/insightface) — face detection & embedding extraction
- [OpenCV](https://opencv.org/) — image processing
- [NumPy](https://numpy.org/) — numerical operations
- [ONNX Runtime](https://onnxruntime.ai/) — model inference

---

## ⚙️ General Setup

Both projects use isolated virtual environments. It is recommended to set up each task's `venv` separately as described in respective setup sections above, to avoid dependency conflicts between the two projects.

---
