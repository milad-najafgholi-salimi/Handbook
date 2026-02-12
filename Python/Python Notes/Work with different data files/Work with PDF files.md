## 1) Reading and Extracting Text from PDFs

### Library: `PyPDF2` (or `pypdf`, modern version)

Install:
```
pip install pypdf
```
Example:
```
from pypdf import PdfReader

reader = PdfReader("sample.pdf")

for page in reader.pages:
    text = page.extract_text()
    print(text)
```
### Good for:

- Extracting simple text
    
- Getting page count
    
- Basic metadata
    

### ⚠️ Limitation:

Not very accurate with complex layouts or scanned PDFs.

---

## 2) Extracting Text More Accurately

### Library: `pdfplumber`

Install:
```
pip install pdfplumber
```
Example:
```
import pdfplumber

with pdfplumber.open("sample.pdf") as pdf:
    for page in pdf.pages:
        text = page.extract_text()
        print(text)
```
### Better for:

- Structured text
    
- Tables
    
- More precise extraction
    

---

## 3) Extracting Tables from PDF

Using `pdfplumber`:
```
import pdfplumber

with pdfplumber.open("file.pdf") as pdf:
    page = pdf.pages[0]
    table = page.extract_table()
    print(table)
```
Or use:

- `camelot`
    
- `tabula-py`
    

These are very useful in data analysis projects.

---

## 4) Creating PDF Files in Python

### Library: `reportlab`

Install:
```
pip install reportlab
```
Simple example:
```
from reportlab.platypus import SimpleDocTemplate, Paragraph
from reportlab.lib.styles import getSampleStyleSheet

doc = SimpleDocTemplate("output.pdf")
styles = getSampleStyleSheet()
elements = []

elements.append(Paragraph("Hello, this is a PDF file!", styles["Normal"]))

doc.build(elements)
```
### Used for:

- Reports
    
- Certificates
    
- Automated invoices
    
- Academic documents
    

---

## 5) Merging PDF Files

Using `pypdf`:
```
from pypdf import PdfMerger

merger = PdfMerger()

merger.append("file1.pdf")
merger.append("file2.pdf")

merger.write("merged.pdf")
merger.close()
```

---
## 6) Splitting a PDF
```
from pypdf import PdfReader, PdfWriter

reader = PdfReader("input.pdf")

for i, page in enumerate(reader.pages):
    writer = PdfWriter()
    writer.add_page(page)

    with open(f"page_{i+1}.pdf", "wb") as output:
        writer.write(output)
```

---
## 7) Working with Scanned PDFs (OCR)

If the PDF is scanned (image-based), normal text extraction won’t work.

You need OCR:

### Libraries:

- `pytesseract`
    
- `pdf2image`
    

Example process:

1. Convert PDF to image
    
2. Apply OCR to extract text
    

---

## 8) Reading PDF Metadata
```
from pypdf import PdfReader

reader = PdfReader("file.pdf")
print(reader.metadata)
```
This can give:

- Author
    
- Creation date
    
- Title
    

---

## Common Challenges with PDFs

PDF is not designed for easy text extraction. Problems include:

- Broken sentence formatting
    
- Columns mixed together
    
- Tables not aligned
    
- Special characters issues
    

Because PDF stores content as positioned objects, not logical paragraphs.

---

## Which Library Should You Use?

|Task|Best Tool|
|---|---|
|Simple text extraction|pypdf|
|Better text extraction|pdfplumber|
|Table extraction|camelot / tabula|
|Create PDFs|reportlab|
|OCR scanned PDFs|pytesseract|
|Merge/split PDFs|pypdf|

---
## Example Workflow (Practical Scenario)

Suppose you want to:

1. Extract student names from PDF result sheets
    
2. Save them into CSV
    
3. Analyze them
    

You would:

- Use `pdfplumber` to extract text
    
- Parse the text
    
- Save results using `pandas`
    

---

## Summary

Working with PDFs in Python involves:

- Reading and extracting content
    
- Manipulating document structure
    
- Creating professional documents
    
- Handling scanned documents with OCR