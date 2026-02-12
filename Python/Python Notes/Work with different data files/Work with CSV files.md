## What Is a CSV File?

**CSV** stands for **Comma-Separated Values**.

It is a simple file format used to store **tabular data** (data arranged in rows and columns), like a spreadsheet or database table.

CSV files are plain text files — which means you can open them with:

- Notepad
    
- Excel
    
- Google Sheets
    
- Python
    
- R
    
- Database software
    

---

## Structure of a CSV File

A CSV file contains:

- Each **row** on a new line
    
- Each **column** separated by a comma
    

Example:
```
Name,Age,Country
Milad,22,Iran
Faraz,22,Germany
Mehrdad,27,UK
```
### Explanation:

- First row = column headers
    
- Each next row = one record (one person)
    
- Commas separate the values
    

---

## Key Characteristics

### 1) Plain Text Format

CSV files are not formatted like Excel (.xlsx).  
They do NOT store:

- Colors
    
- Fonts
    
- Formulas
    
- Charts
    

Only raw data.
### 2) Lightweight and Universal

- Very small file size
    
- Works on almost all systems
    
- Commonly used for data exchange
    

That’s why CSV is widely used in:

- Data science
    
- Machine learning
    
- Database imports/exports
    
- Business reporting
    

---

## Other Possible Separators

Although it means “Comma-Separated,” sometimes other separators are used:

|Separator|Example|
|---|---|
|Comma `,`|Standard CSV|
|Semicolon `;`|Common in Europe|
|Tab `\t`|Called TSV (Tab-Separated Values)|

Example (semicolon version):
```
Name;Age;Country
Milad;22;Iran
```

---
## File Extension

CSV files usually end with:
```
filename.csv
```

---
##  How CSV Files Handle Special Cases

### 1) Values With Commas

If a value contains a comma, it must be wrapped in double quotes:
```
Name,Address
Milad,"123 Main Street, Tehran"
```
### 2) Text Values

Text is sometimes enclosed in double quotes:
```
"Name","Age","Country"
"Milad","22","Iran"
```
### 3) Missing Data

Empty values are allowed:
```
Name,Age,Country
Milad,22,
Faraz,,Germany
```

---
## How to Open CSV Files

You can open CSV files with:

- Microsoft Excel
    
- Google Sheets
    
- LibreOffice Calc
    
- Notepad
    
- Python (pandas library)
    

---

## Example in Python
```
import pandas as pd

data = pd.read_csv("file.csv")
print(data.head())
```
This loads the CSV file into a table format.

---

## Why CSV Is Important

CSV is heavily used in:

- Data analysis
    
- Statistics
    
- Machine learning datasets
    
- Government open data
    
- Business data transfer
    
- Research projects
    

It is one of the most important data formats in data science.

---

## CSV vs Excel (.xlsx)

|Feature|CSV|Excel|
|---|---|---|
|Stores formatting|❌ No|✅ Yes|
|Stores formulas|❌ No|✅ Yes|
|File size|Small|Larger|
|Universal compatibility|Very high|Medium|
|Human-readable|Yes|Not easily|

---

## When Should You Use CSV?

Use CSV when:

- You only need raw data
    
- You want compatibility across systems
    
- You are importing/exporting data
    
- You are working with programming tools
    

Do NOT use CSV if:

- You need formatting
    
- You need multiple sheets
    
- You need formulas saved
    

---

## In Simple Terms

A CSV file is like:

> A very simple spreadsheet saved as text.

