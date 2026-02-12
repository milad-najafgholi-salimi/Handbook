## Working with Excel Files in Python

Excel files usually come in these formats:

- `.xlsx` → Modern Excel format (most common)
    
- `.xls` → Older Excel format
    
- `.xlsm` → Excel file with macros

---
## 1) The Most Important Library: `pandas`

For data analysis, **pandas** is the most powerful and commonly used tool.

Install:
```
pip install pandas openpyxl
```
(`openpyxl` is needed for .xlsx files.)

### Reading an Excel File
```
import pandas as pd

df = pd.read_excel("file.xlsx")
print(df.head())
```
If the file has multiple sheets:
```
df = pd.read_excel("file.xlsx", sheet_name="Sheet1")
```
To read all sheets:
```
all_sheets = pd.read_excel("file.xlsx", sheet_name=None)
```
### Writing to Excel
```
df.to_excel("output.xlsx", index=False)
```
Writing multiple sheets:
```
with pd.ExcelWriter("output.xlsx") as writer:
    df1.to_excel(writer, sheet_name="Sheet1", index=False)
    df2.to_excel(writer, sheet_name="Sheet2", index=False)
```

---
## 2) Working Directly with Excel Structure: `openpyxl`

Use `openpyxl` if you want more control (formatting, formulas, styling).

Install:
```
pip install openpyxl
```
### Create a New Excel File
```
from openpyxl import Workbook

wb = Workbook()
ws = wb.active
ws.title = "Data"

ws["A1"] = "Name"
ws["B1"] = "Age"

ws.append(["Milad", 22])
ws.append(["Faraz", 22])

wb.save("example.xlsx")
```
### Add a Formula
```
ws["C1"] = "Total"
ws["C2"] = "=SUM(A2:B2)"
```
### Format a Cell
```
from openpyxl.styles import Font

ws["A1"].font = Font(bold=True)
```

---
## 3) Working with Existing Files
```
from openpyxl import load_workbook

wb = load_workbook("file.xlsx")
ws = wb["Sheet1"]

print(ws["A1"].value)

wb.save("file_updated.xlsx")
```

---
## 4) When to Use pandas vs openpyxl?
| Task             | Use pandas   | Use openpyxl |
| ---------------- | ------------ | ------------ |
| Data analysis    | ✅ Yes        | ❌ Not ideal  |
| Filtering data   | ✅ Yes        | ❌            |
| Formatting cells | ❌            | ✅            |
| Adding formulas  | ❌            | ✅            |
| Large datasets   | ✅ Excellent  | ⚠️ Slower    |
| Creating reports | ✅ + openpyxl | ✅            |
👉 Often professionals combine both:

- Use pandas for data processing
    
- Use openpyxl for formatting and final report styling
    

---

## 5) Advanced Excel Automation

You can automate:

- Monthly financial reports
    
- Student grade sheets
    
- Sales dashboards
    
- Attendance systems
    
- Research data summaries
    

Example workflow:

1. Load Excel file
    
2. Clean data with pandas
    
3. Calculate statistics
    
4. Export formatted report
    

---

## 6) Handling Large Excel Files

For large files:

- Use `usecols=` to select columns
    
- Use `nrows=` to limit rows
    
- Convert Excel → CSV for faster processing
    

Example:
```
df = pd.read_excel("big_file.xlsx", usecols=["Name", "Score"])
```

---
## 7) Other Useful Libraries
| Library    | Purpose                               |
| ---------- | ------------------------------------- |
| xlrd       | Read old .xls files                   |
| xlsxwriter | Create highly formatted Excel reports |
| pyxlsb     | Read binary Excel files (.xlsb)       |

---
## 8) Common Problems & Solutions

### ❌ Error: Missing engine

Install:
```
pip install openpyxl
```
### ❌ Dates formatted incorrectly

Use:
```
parse_dates=True
```
### ❌ NaN values

Use:
```
df.fillna(0)
```

---
## Summary

Working with Excel in Python involves:

- Reading data → `pandas`
    
- Writing data → `pandas`
    
- Formatting & styling → `openpyxl`
    
- Creating professional reports → combine both
    

Excel + Python is extremely powerful for:

- Education
    
- Business
    
- Research
    
- Data science
    
- Administration
