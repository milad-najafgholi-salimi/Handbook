Web scraping in Python is the process of automatically extracting data from websites using code instead of manually copying and pasting information. It’s widely used for data collection, research, automation, monitoring, and building datasets for analysis or machine learning.

---
## 1. What Is Web Scraping?

Web scraping involves:

1. Sending a request to a webpage
    
2. Receiving the HTML content
    
3. Parsing the HTML structure
    
4. Extracting specific data
    
5. Saving or processing the data
    

Websites are built using HTML (structure), CSS (style), and often JavaScript (dynamic behavior). Scraping focuses mainly on HTML.

---

## 2. Common Python Libraries for Web Scraping

### 2.1 `requests` – Fetching Web Pages

This library sends HTTP requests and retrieves webpage content.
```
import requests

url = "https://example.com"
response = requests.get(url)

print(response.status_code)  # 200 means success
print(response.text)         # HTML content
```
- `.get()` sends a GET request
    
- `.text` gives raw HTML
    
- `.status_code` tells if request succeeded
### 2.2 `BeautifulSoup` – Parsing HTML

`BeautifulSoup` makes it easy to navigate and extract data from HTML.

Install:
```
pip install beautifulsoup4
```
Example:
```
from bs4 import BeautifulSoup
import requests

url = "https://example.com"
response = requests.get(url)

soup = BeautifulSoup(response.text, "html.parser")

print(soup.title.text)
```
Key methods:

- `soup.find()` → finds first matching element
    
- `soup.find_all()` → finds all matching elements
    
- `.text` → extracts inner text
    
- `.get("href")` → extracts attribute
    

Example extracting links:
```
for link in soup.find_all("a"):
    print(link.get("href"))
```
### 2.3 `lxml` – Faster HTML/XML Parsing

More powerful and faster parser.
```
pip install lxml
```
Use with BeautifulSoup:
```
soup = BeautifulSoup(response.text, "lxml")
```
### 2.4 `Selenium` – For Dynamic Websites

Many modern sites use JavaScript to load content dynamically. `requests` cannot execute JavaScript — Selenium can.

Install:
```
pip install selenium
```
Example:
```
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://example.com")

html = driver.page_source
print(html)

driver.quit()
```
Selenium simulates a real browser and can:

- Click buttons
    
- Fill forms
    
- Scroll
    
- Wait for elements to load
    

---

## 3. How Web Scraping Works (Step-by-Step)

Let’s say we want to scrape product names from a site.

### Step 1: Inspect the page

Right-click → Inspect (Chrome DevTools)

Find:

- HTML tag
    
- Class name
    
- ID
    

Example:
```
<h2 class="product-title">Laptop</h2>
```
### Step 2: Write the scraper
```
import requests
from bs4 import BeautifulSoup

url = "https://example.com/products"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")

titles = soup.find_all("h2", class_="product-title")

for title in titles:
    print(title.text)
```

---
## 4. Handling Dynamic Content

If data loads after scrolling or clicking:

### Option 1: Use Selenium

### Option 2: Find API calls in Network tab

Often websites fetch data from hidden APIs (JSON endpoints).

In DevTools:

- Go to Network tab
    
- Filter by "XHR"
    
- Refresh page
    
- Look for JSON requests
    

Then scrape the API directly:
```
response = requests.get("https://example.com/api/products")
data = response.json()

for product in data:
    print(product["name"])
```
This is usually cleaner and faster than Selenium.

---

## 5. Common Challenges

### 5.1 Anti-Scraping Protection

Websites may block bots using:

- Rate limiting
    
- IP blocking
    
- Captchas
    
- User-Agent detection
    

You can change headers:
```
headers = {
    "User-Agent": "Mozilla/5.0"
}

response = requests.get(url, headers=headers)
```
### 5.2 Pagination

Many sites have multiple pages:

Example:
```
?page=1
?page=2
?page=3
```
You loop:
```
for page in range(1, 6):
    url = f"https://example.com/products?page={page}"
    response = requests.get(url)
```
### 5.3 Login Required Sites

Use `requests.Session()`:
```
session = requests.Session()

login_data = {
    "username": "your_username",
    "password": "your_password"
}

session.post("https://example.com/login", data=login_data)
response = session.get("https://example.com/dashboard")
```

---
## 6. Saving Scraped Data

### Save as CSV
```
import csv

with open("data.csv", "w", newline="") as file:
    writer = csv.writer(file)
    writer.writerow(["Title"])

    for title in titles:
        writer.writerow([title.text])
```
### Save as JSON
```
import json

data = [title.text for title in titles]

with open("data.json", "w") as f:
    json.dump(data, f)
```

---
## 7. Ethical & Legal Considerations (Very Important)

Before scraping:

1. Check `robots.txt`  
    Example:
```
https://example.com/robots.txt
```
1. Read the Terms of Service
    
2. Avoid overloading servers
    
3. Respect rate limits
    
4. Don’t scrape personal or protected data
    

Web scraping is legal in many contexts, but misuse can violate terms or laws.

---

## 8. Best Practices

- Add delays:
```
import time
time.sleep(2)
```
- Use try/except to handle errors
    
- Log your scraping process
    
- Cache responses
    
- Use proxies responsibly if necessary
    

---

## 9. When to Use What
| Situation             | Tool                     |
| --------------------- | ------------------------ |
| Static HTML           | requests + BeautifulSoup |
| Need speed            | requests + lxml          |
| JavaScript-heavy site | Selenium                 |
| Large-scale scraping  | Scrapy framework         |
| API available         | Direct API requests      |

---
## 10. Advanced: Scrapy Framework

Scrapy is a full scraping framework:
```
pip install scrapy
```
It supports:

- Pipelines
    
- Middleware
    
- Auto-throttling
    
- Built-in request management
    

Used for production-level scraping.

---

## 11. Real-World Applications

- Price monitoring
    
- Research data collection
    
- Job listing aggregation
    
- Real estate tracking
    
- Social media analytics (via APIs)
    
- Machine learning datasets
    

---

## 12. Simple Complete Example
```
import requests
from bs4 import BeautifulSoup

url = "https://news.ycombinator.com/"
headers = {"User-Agent": "Mozilla/5.0"}

response = requests.get(url, headers=headers)
soup = BeautifulSoup(response.text, "html.parser")

titles = soup.find_all("a", class_="storylink")

for i, title in enumerate(titles, 1):
    print(f"{i}. {title.text}")
```
