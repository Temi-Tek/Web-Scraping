# FramesDirect Product Data Exporter

A lightweight utility script that saves scraped eyeglasses product data from FramesDirect to both JSON and CSV formats.

---

## Overview

This script takes a `product` list (typically produced by a web scraper) and exports it to two output files:

- `framesdirect_products.json` — structured, human-readable JSON
- `framesdirect_products.csv` — flat tabular format, ready for spreadsheet tools or further analysis

---

## Output Files

| File | Format | Description |
|------|--------|-------------|
| `framesdirect_products.json` | JSON | Full product data with 4-space indentation |
| `framesdirect_products.csv` | CSV | Tabular data with headers; UTF-8 encoded |

---

## CSV Schema

The CSV file contains the following columns:

| Column | Description |
|--------|-------------|
| `brand` | The eyeglasses brand name |
| `name` | Product name or model |
| `current_price` | Current listed price |
| `former_price` | Original or sale price before discount |

---

## Requirements

- Python 3.x (standard library only — no external dependencies)
- A `product` variable in scope: a **list of dictionaries**, each containing the keys `brand`, `name`, `current_price`, and `former_price`

---

## Usage

Ensure your scraping script populates the `product` list before running this export block:

```python
import csv
import json

# Save to JSON
with open('framesdirect_products.json', 'w') as json_file:
    json.dump(product, json_file, indent=4)
print("Data saved to framesdirect_products.json")

# Save to CSV
with open('framesdirect_products.csv', 'w', newline='', encoding='utf-8') as csv_file:
    writer = csv.DictWriter(csv_file, fieldnames=["brand", "name", "current_price", "former_price"])
    writer.writeheader()
    writer.writerows(product)
print("Data saved to framesdirect_products.csv")
```

---

## Notes

- The `newline=''` parameter in the CSV writer prevents blank rows on Windows systems.
- If `product` contains keys beyond the four defined `fieldnames`, they will be silently ignored by `DictWriter`.
- Both files are overwritten on each run — rename or move previous outputs before re-running if you need to preserve them.
