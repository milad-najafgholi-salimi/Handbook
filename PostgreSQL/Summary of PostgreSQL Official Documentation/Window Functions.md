### The Big Idea: GROUP BY vs. WINDOW

- **GROUP BY** takes many rows and squashes them into **one** summary row per group. You lose the detail.
    
- **WINDOW** takes many rows and keeps **all** of them, but adds an extra column with the summary value calculated from that row's "window" (group).
    

**Example:**  
Imagine a `sales` table.

|year|product|amount|
|---|---|---|
|2023|A|100|
|2023|B|150|
|2024|A|200|

- **GROUP BY** `year` → returns 2 rows (2023 total 250, 2024 total 200).
    
- **WINDOW** `year` → returns all 3 rows, but with a `yearly_total` column showing 250 for both 2023 rows, and 200 for the 2024 row.

---
![pic-37](37.png)

