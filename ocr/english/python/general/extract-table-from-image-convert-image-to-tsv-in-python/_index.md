---
category: general
date: 2026-07-05
description: Extract table from image using Python OCR. Learn how to extract table,
  convert image to TSV, and master ocr table image python techniques.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: en
og_description: Extract table from image with Python OCR. This guide shows how to
  extract table, convert image to TSV, and use ocr table image python tools.
og_title: Extract Table from Image – Convert Image to TSV in Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Extract Table from Image – Convert Image to TSV in Python
url: /python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Table from Image – Convert Image to TSV in Python

Ever wondered how to extract table from image without pulling your hair out? In this tutorial we’ll walk through **how to extract table** data from a picture using the `aocr` library, then turn that data into a tidy TSV file. No magic, just a few lines of Python and a bit of AI‑powered post‑processing.

If you’ve ever tried to copy‑paste a table from a scanned invoice or a screenshot and ended up with a jumbled mess, you’ll appreciate why an OCR‑driven approach is worth mastering. By the end, you’ll be able to feed any image of a table into Python and get clean, tab‑separated values ready for spreadsheets or databases.

---

## What You’ll Need

Before we dive in, make sure you have the following on your machine:

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.9+ | The `aocr` package targets modern Python runtimes. |
| `aocr` library (`pip install aocr`) | Provides the OCR engine and the AI post‑processor we’ll use. |
| An image file containing a table (PNG, JPG, etc.) | The source data we’ll extract. |
| Optional: a virtual environment | Keeps dependencies isolated—highly recommended. |

Having these ready saves you from interruptions halfway through the guide.

---

## Install the Dependencies

First, let’s get the OCR tooling installed. Open a terminal and run:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** If you hit permission errors, add `--user` to the `pip install` command or use `pipx` for a global install.

---

## Step 1 – Initialise the OCR Engine

The engine is the heart of the process. Think of it as the “brain” that looks at each pixel and decides what character belongs where.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Why do we instantiate an engine instead of calling a single function? The engine object lets us attach custom post‑processors later, giving us fine‑grained control over the output—essential when you need **ocr table image python** accuracy.

---

## Step 2 – Attach the AI Post‑Processor

`aocr` ships with a lightweight AI post‑processor that cleans up raw OCR results while preserving cell borders. No extra arguments are required, which keeps the code tidy.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

If you skip this step, you’ll still get raw text, but the table structure will be noisy—think of a spreadsheet where every cell is a mystery. The post‑processor does the heavy lifting of aligning text to its original grid.

---

## Step 3 – Load Your Table Image

You can load an image from any path, but for clarity we’ll reference a placeholder directory. Replace `"YOUR_DIRECTORY/invoice_table.png"` with the actual path to your file.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note:** `aocr.Image` automatically detects the image format and normalises colour channels, so you don’t need to pre‑process the file unless it’s severely degraded.

---

## Step 4 – Perform Structured OCR

Now the engine scans the image and returns a raw table object. This object contains rows, columns, and the raw text for each cell.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Why use `recognize_structured` instead of a generic `recognize` call? The structured variant attempts to infer row/column boundaries, giving you a matrix‑like result that’s far easier to convert to TSV later.

---

## Step 5 – Clean the Data with the AI Post‑Processor

Running the post‑processor refines the raw output: it removes stray characters, merges split fragments, and ensures each cell’s text is correctly aligned.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

If you inspect `processed_table.table`, you’ll see a list of rows, each row being a list of `Cell` objects. Each `Cell` has a `.text` attribute that holds the cleaned string.

---

## Step 6 – Export the Table as TSV

The final step is to turn the processed data into a tab‑separated values (TSV) file—exactly what you need when you want to **convert image to TSV** for Excel or Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Running the script prints each row to the console (if you prefer) and writes a clean TSV file you can open in any spreadsheet program.

### Quick verification

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

You should see neatly aligned columns, like:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

If the output looks scrambled, double‑check the image quality (sharpness, contrast) and consider tweaking the OCR engine’s settings—`engine.set_config(...)` lets you adjust language models and confidence thresholds.

---

## Handling Common Edge Cases

| Situation | Suggested Fix |
|-----------|---------------|
| **Skewed image** | Pre‑rotate using `Pillow` (`Image.rotate`) before feeding it to `aocr`. |
| **Low contrast** | Apply histogram equalisation (`cv2.equalizeHist`) to boost readability. |
| **Merged cells** | Post‑process the TSV to split cells based on known delimiters or use the `merge_cells=False` flag if available. |
| **Multi‑page PDFs** | Convert each page to an image first (`pdf2image`) and run the pipeline in a loop. |

These tweaks keep your **ocr table image python** workflow robust across varied source material.

---

## Full Script – One‑Stop Solution

Below is the complete, ready‑to‑run script that bundles every step discussed. Save it as `extract_table.py` and execute `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}