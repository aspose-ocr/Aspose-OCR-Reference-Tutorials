---
category: general
date: 2026-03-26
description: Extract tables from image and convert image to spreadsheet using Python
  OCR. Learn how to load image for OCR, read tables and extract table data.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: en
og_description: Extract tables from image with Python OCR. This guide shows how to
  load image for OCR, read tables, and convert them to a spreadsheet.
og_title: Extract Tables from Image – Complete OCR Tutorial
tags:
- OCR
- Python
- Data Extraction
title: Extract Tables from Image – Step‑by‑Step OCR Guide
url: /python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Tables from Image – Complete OCR Tutorial

Ever needed to **extract tables from image** but weren’t sure where to start? You’re not alone. Many developers hit a wall when a PDF or screenshot contains tabular data that must become editable rows and columns. The good news? A few lines of Python code, paired with a solid OCR engine, can turn that picture into a usable spreadsheet in seconds.

In this tutorial we’ll walk through loading an image for OCR, running the recognition engine, and pulling out each table row‑by‑row. By the end you’ll be able to **convert image to spreadsheet**, and you’ll also see how to **ocr read tables** and **ocr extract table data** for downstream processing. No hidden magic, just clear, runnable code you can drop into your project today.

---

## What You’ll Need

Before we dive in, make sure you have the following on hand:

- **Python 3.9+** – the latest stable release works best.
- The **`ocr`** library (or any compatible OCR SDK that exposes `OcrEngine`, `Image`, and table‑related methods). Install it with `pip install ocr‑sdk` (replace with the actual package name).
- An image file (`.png`, `.jpg`, etc.) that contains a clearly printed table.  
- Optional: **pandas** if you want to write the extracted data straight to a CSV or Excel file (`pip install pandas`).

Got everything? Great—let’s get started.

---

## Step 1: Import the OCR SDK and Prepare Your Environment

First things first: we need to bring the OCR classes into our script and set up a tiny helper that will later turn the raw table data into a DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Why this matters:** Importing `ocr` gives us access to `OcrEngine`, `Imaging.Image`, and the table objects we’ll be iterating over. `pandas` isn’t required for extraction, but it makes the “convert image to spreadsheet” part trivial.

---

## Step 2: Load the Image You Want to Process

Now we actually **load image for OCR**. The SDK expects an `Image` object, so we’ll wrap our file path with the helper method `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Pro tip:** Keep your image files in a dedicated folder (`assets/` or `data/`) and use relative paths. That way the script stays portable across machines.

---

## Step 3: Run the Recognition Process

With the image attached, we can finally tell the engine to **ocr read tables**. The `recognize()` call returns a result object that holds everything the engine discovered—text blocks, lines, and, most importantly for us, tables.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Why we check:** Some images might be noisy or the table borders faint, causing the engine to miss them. Logging a warning gives you early feedback without breaking the script.

---

## Step 4: Extract Each Table’s Rows and Cells

Here’s where the real magic happens. We’ll iterate over every detected table, pull out each row, then each cell’s text. The inner list comprehension makes the code concise, yet we’ll still explain the flow.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**What’s going on?**  

- `enumerate(..., start=1)` gives us a friendly table number for logging.  
- `row_obj.get_cells()` returns each cell object; `cell.get_text()` fetches the OCR‑decoded string.  
- We store rows in `rows_data`, then hand them to `pandas.DataFrame` which automatically aligns columns.  
- The `print` block mirrors the **essential output** shown in the original snippet, so you can verify results instantly.

**Edge case handling:** If a row has a different number of cells than the others, `pandas` will fill missing spots with `NaN`. You can later clean the DataFrame with `df.fillna('')` if you prefer empty strings.

---

## Step 5: Save the Extracted Tables to a Spreadsheet

Now that we have a list of DataFrames, turning them into an Excel workbook (or CSV files) is a breeze. This satisfies the “convert image to spreadsheet” goal.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Why Excel?** Most business users love `.xlsx`. If you prefer CSV, replace the loop with `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Full, Ready‑to‑Run Script

Putting everything together, here’s the complete program you can copy‑paste and execute.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Expected console output** (assuming a simple 2×3 table):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

And you’ll find `extracted_tables.xlsx` in the script’s folder, each table on its own sheet.

---

## Frequently Asked Questions & Tips

| Question | Answer |
|----------|--------|
| **Can I use a different OCR library?** | Absolutely. The pattern stays the same: load image → recognize → iterate over `get_tables()`. Just replace the import and object names. |
| **What if my image is noisy?** | Pre‑process with OpenCV (thresholding, deskew) before feeding it to the OCR engine. Noise reduction often improves **ocr extract table data** accuracy. |
| **Do I need to install `openpyxl`?** | Yes, `pandas` uses it under the hood for Excel output. Install with `pip install openpyxl`. |
| **How do I handle merged cells?** | Some SDKs expose `cell.is_merged()`; you can detect and propagate the value across the merged range manually. |
| **Is there a way to extract only specific tables?** | Filter by `table_obj.get_confidence()` or by checking header keywords before processing. |

---

## Wrapping Up

You now have a complete, end‑to‑end solution for **extract tables from image**, convert the result into a tidy spreadsheet, and even handle multiple tables in a single picture. The script demonstrates how to **load image for OCR**, **ocr read tables**, and **ocr extract table data** while staying flexible enough for real‑world variations.

What’s next? Try feeding the OCR engine a PDF page rendered as an image, or experiment with different languages and fonts. You could also pipe the DataFrames straight into a database or a reporting tool—your imagination is the limit.

If you found this guide helpful, feel free to share it, star the repository that hosts the SDK, or drop a comment with your own tricks. Happy coding, and may your tables always be perfectly parsed!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}