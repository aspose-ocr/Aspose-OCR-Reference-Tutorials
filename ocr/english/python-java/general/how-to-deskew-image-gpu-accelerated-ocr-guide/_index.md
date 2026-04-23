---
category: general
date: 2026-01-02
description: Learn how to deskew image and boost image contrast to get plain text
  fast. Includes step‑by‑step Python code and tips for extracting text.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: en
og_description: How to deskew image and boost contrast to get plain text. Full Python
  example with table extraction and GPU acceleration.
og_title: How to Deskew Image – Complete GPU OCR Tutorial
tags:
- OCR
- Python
- Image Processing
title: How to Deskew Image – GPU‑Accelerated OCR Guide
url: /python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image – GPU‑Accelerated OCR Guide

Ever wondered **how to deskew image** when your receipts come in at a funny angle? You're not alone; a skewed photo can turn a perfectly readable receipt into a jumbled mess. The good news is that with a few lines of Python you can auto‑deskew, boost the contrast, and pull out clean plain text—no manual Photoshop required.  

In this tutorial we'll walk through a complete, runnable example that not only **how to deskew image** but also shows **how to boost contrast**, how to **get plain text**, and even **how to extract text** from tables that the OCR engine discovers. By the end you’ll have a self‑contained script you can drop into any project.

## What You’ll Need

- Python 3.9+ installed (the code uses type hints, so a recent interpreter helps)
- The `ocr` library that provides `OcrEngine`, `EngineMode`, `ImageProcessingOptions`, and `OcrResult` (install via `pip install ocr‑sdk` – replace with the actual package name you use)
- A GPU with compatible drivers if you want the speed boost (optional but recommended)
- An image file that is slightly rotated or low‑contrast, e.g., `receipt_skewed.jpg`

> **Pro tip:** If you don’t have a GPU, just change `EngineMode.GPU` to `EngineMode.CPU` and the script still works—just a bit slower.

## Step‑by‑Step Implementation

Below we break the solution into logical chunks. Each chunk has a descriptive **H2** that either contains the primary keyword *how to deskew image* or one of the secondary keywords. The code is complete, commented, and ready to run.

### How to Deskew Image with GPU‑Accelerated OCR

The first thing we do is tell the OCR engine to run on the GPU and enable the auto‑deskew feature. Auto‑deskew analyses the image’s geometry and rotates it back to upright.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Why this matters:** GPU acceleration can cut processing time from seconds to milliseconds, which is crucial when you’re handling dozens of receipts per minute.

### Boost Image Contrast for Better Recognition

A low‑contrast receipt is a nightmare for any OCR system. By boosting the contrast we give the engine clearer edges to work with.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **How to boost contrast:** The `set_contrast_boost` method accepts a percentage; 30 % is a safe default that works for most scanned receipts. If your images are extremely dark, bump it up to 50 % or experiment.

### Get Plain Text from the Processed Image

Now that the image is straight and bright, we feed it to the engine and ask for the plain text result.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Expected output** (truncated for brevity):

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **How to get plain text:** The `get_text()` method strips away any layout information and returns a clean string, which you can then store in a database, send to an API, or feed into downstream analytics.

### How to Extract Text from Detected Tables

Often receipts contain tabular data (items, quantities, prices). The OCR SDK can detect tables and let you iterate over rows and cells.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Sample table output**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Why extract tables:** Structured data makes it trivial to calculate totals, generate reports, or feed into accounting software.

### Full Working Script

Putting everything together, here’s the script you can copy‑paste into `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Run it with:

```bash
python deskew_and_ocr.py
```

You should see the cleaned‑up text and any detected tables printed to the console.

## Common Edge Cases & How to Handle Them

| Situation | What to Do |
|-----------|------------|
| **Image is upside‑down** | Increase `set_auto_deskew(True)` confidence by also calling `set_rotation_correction(True)` if the SDK offers it. |
| **Contrast boost makes the image too bright** | Reduce the percentage passed to `set_contrast_boost` (e.g., 15 %). |
| **GPU not available** | Switch `EngineMode.GPU` to `EngineMode.CPU`; the rest of the pipeline remains unchanged. |
| **Tables are missed** | Try a higher resolution scan or enable `set_table_detection(True)` if the library provides it. |

## Next Steps: From Plain Text to Structured Data

Now that you know **how to deskew image**, **how to boost contrast**, and **how to get plain text**, you might want to:

- Parse the plain text with regular expressions to extract key‑value pairs (e.g., `total`, `date`).
- Store the results in a SQLite or PostgreSQL database for later reporting.
- Hook the script into a serverless function (AWS Lambda, Azure Functions) to process uploads automatically.

All of those extensions build on the same foundation we covered here.

## Conclusion

We’ve walked through **how to deskew image** using a GPU‑accelerated OCR engine, demonstrated **how to boost contrast** for sharper recognition, shown you exactly **how to get plain text**, and even covered **how to extract text** from tables. The complete, runnable script ties everything together, so you can drop it into any Python project and start pulling clean data from skewed, low‑contrast photos right away.

Give it a try with a few of your own receipts, tweak the contrast level, and let the OCR do the heavy lifting. If you run into quirks, revisit the edge‑case table above—most issues are just a tweak away.

Happy coding, and may your images always be straight and bright!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}