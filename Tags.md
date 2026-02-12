## 1) What Are Tags in Web Scraping?

Web pages are written in **HTML (HyperText Markup Language)**.

HTML is made of **tags**, such as:
```
<h1>Title</h1>
<p>This is a paragraph.</p>
<a href="https://example.com">Click here</a>
<div class="product">Laptop</div>
```
Each tag:

- Has a **name** (`h1`, `p`, `a`, `div`)
    
- May contain **attributes** (`class`, `id`, `href`)
    
- Contains **content**
    

When scraping, we use these tags to locate and extract data.

---

## 2) Common HTML Tags Used in Scraping

Here are the most important tags you’ll encounter:

|Tag|Purpose|
|---|---|
|`<h1>–<h6>`|Headings|
|`<p>`|Paragraph text|
|`<a>`|Links|
|`<img>`|Images|
|`<div>`|Generic container|
|`<span>`|Inline container|
|`<table>`|Tables|
|`<tr>`|Table row|
|`<td>`|Table cell|
|`<ul>`, `<ol>`|Lists|
|`<li>`|List item|
|`<form>`|Forms|
|`<input>`|Input fields|

---
## 3) How Python Accesses Tags

In Python, the most common tool for working with tags is:

### BeautifulSoup (bs4)

Example setup:
```
import requests
from bs4 import BeautifulSoup

url = "https://example.com"
response = requests.get(url)
soup = BeautifulSoup(response.text, "html.parser")
```
Now `soup` contains all HTML tags from the page.

---

## 4) Finding Tags

### Find First Tag
```
soup.find("p")
```
Finds the first `<p>` tag.

---

### Find All Tags
```
soup.find_all("p")
```
Returns all paragraph tags.

---

### Find by Class
```
soup.find("div", class_="product")
```
Important:  
We use `class_` because `class` is a Python keyword.

---

### Find by ID
```
soup.find("div", id="main")
```
### Find Links
```
links = soup.find_all("a")

for link in links:
    print(link.get("href"))
```

---
## 5) Getting Data From Tags

Once you locate a tag, you can extract:

### Text
```
tag.text
```
or
```
tag.get_text()
```
### Attribute Values
```
tag["href"]
```
or safer:
```
tag.get("href")
```

---
## 6) Nested Tags (Parent–Child Structure)

HTML is hierarchical:
```
<div class="product">
    <h2>Laptop</h2>
    <p>Price: $1000</p>
</div>
```
You can navigate:
```
product = soup.find("div", class_="product")
title = product.find("h2").text
price = product.find("p").text
```

---
## 7) CSS Selectors (More Powerful)

`BeautifulSoup` also supports CSS selectors:
```
soup.select("div.product h2")
```

Examples:

| Selector     | Meaning         |
| ------------ | --------------- |
| `"div"`      | All divs        |
| `".product"` | Class = product |
| `"#main"`    | ID = main       |
| `"div > p"`  | Direct child    |
| `"div p"`    | Any nested p    |

---
## 8) Why Tags Matter in Scraping

When scraping, you:

1. Inspect the webpage (Right-click → Inspect)
    
2. Identify the tag that contains the data
    
3. Use Python to target that tag
    
4. Extract the content
    

The whole scraping process depends on correctly understanding the **HTML tag structure**.

---

## 9) Real Example

Suppose a website has:
```
<div class="item">
    <h3>Phone</h3>
    <span class="price">$500</span>
</div>
```
Python scraping:
```
items = soup.find_all("div", class_="item")

for item in items:
    name = item.find("h3").text
    price = item.find("span", class_="price").text
    print(name, price)
```
Output:
```
Phone $500
```

---
## 10) Summary

In web scraping, “tags” mean:

- HTML elements (`div`, `p`, `a`, etc.)
    
- They structure webpage data
    
- Python libraries like BeautifulSoup locate and extract data from them
    
- You can search by:
    
    - Tag name
        
    - Class
        
    - ID
        
    - Attributes
        
    - CSS selectors
