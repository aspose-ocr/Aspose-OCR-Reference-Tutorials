---
category: general
date: 2026-07-05
description: Create searchable PDF with Python. Learn how to OCR a scanned PNG, convert
  scanned image PDF, and get a searchable PDF in minutes.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: en
og_description: Create searchable PDF quickly. This guide shows how to OCR a PNG,
  convert scanned image PDF, and produce a searchable PDF using Python.
og_title: Create Searchable PDF from Scanned Image – Python OCR Tutorial
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Create Searchable PDF from Scanned Image – Full Python OCR Guide
url: /python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Searchable PDF from Scanned Image – Full Python OCR Guide

Ever wondered how to **create searchable PDF** from a scanned picture without paying for pricey software? You're not alone. In many offices, PDFs arrive as flat images—hard to search, impossible to copy‑paste, and a nightmare for compliance audits. The good news? With a few lines of Python you can turn that static PNG into a fully searchable PDF, and the process is easier than you might think.

In this tutorial we’ll walk through a complete **OCR recognition example**, covering everything from installing the right library to writing the final PDF file. By the end you’ll know exactly how to **convert scanned image PDF** files, how to **how to ocr pdf** programmatically, and you’ll have a reusable script you can drop into any project.

## What You’ll Learn

- Install and configure a Python OCR library (we’ll use `pytesseract` and `pdf2image`).
- Initialise the OCR engine and set the language.
- Load a scanned PNG (or any image) and run OCR on it.
- Convert the OCR result into a **searchable PDF** (byte array) and save it.
- Tips for handling multi‑page documents, different languages, and common pitfalls.

No prior experience with OCR is required—just a working Python 3 environment and a bit of curiosity.

---

## Create Searchable PDF – Overview

Below is a high‑level flowchart of the steps we’ll implement.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Alt text: Create searchable PDF workflow diagram showing engine init, image load, OCR recognition, PDF conversion, and file write.*

---

## Step 1: Initialise the OCR Engine (how to ocr pdf)

Why do we need to initialise anything at all? The OCR engine is the brain that interprets pixel patterns as characters. By creating an engine instance and explicitly setting the language, we tell the library what alphabet to expect, which dramatically improves accuracy.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** If you need to OCR documents in multiple languages, install the corresponding language packs for Tesseract and pass a list like `"eng+spa"` to `ocr_language`.

---

## Step 2: Load the Scanned Image (convert scanned image pdf)

The next piece of the puzzle is getting the image data into Python. Whether you have a single PNG or a multi‑page TIFF, the `PIL.Image` class can open it. If you’re starting from a PDF that already contains scanned images, `pdf2image` will convert each page to an image for us.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Why this matters:** Loading the image as a Pillow object gives us access to its raw pixel data, which the OCR engine needs. Skipping this step and feeding raw bytes directly would cause errors.

---

## Step 3: Perform OCR Recognition on the Image (ocr recognition example)

Now the fun part—letting the engine read the text. `pytesseract.image_to_pdf_or_hocr` returns a PDF byte stream that already contains an invisible text layer, which is exactly what we need for a **searchable PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** If your image is low‑contrast, consider applying a simple threshold before OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

This tiny preprocessing step can boost accuracy dramatically.

---

## Step 4: Write the PDF Bytes to a File (convert png searchable pdf)

The OCR library hands us a byte array—think of it as the raw contents of a PDF file. All we need to do now is write those bytes to disk.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** Open the resulting file in any PDF viewer and try searching for a word you know appears in the original image. The highlight should jump straight to the location, proving that the invisible text layer works.

---

## Step 5: Extending to Multi‑Page Documents (convert scanned image pdf)

Real‑world contracts often span multiple pages. To **convert scanned image pdf** files that contain several pages, loop through each page, OCR it, and concatenate the resulting PDFs.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Why merge?** Each call to `image_to_pdf_or_hocr` produces a standalone PDF. Merging them ensures the final document preserves the original page order.

---

## Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| No text searchable after opening the PDF | Tesseract not finding any characters (blank output) | Check image quality, increase DPI, or apply preprocessing (contrast, binarization). |
| garbled characters (e.g., �) | Wrong language pack or missing fonts | Install the correct language data (`tesseract‑lang‑eng`) and ensure `ocr_language` matches. |
| PDF file size huge (>10 MB for a one‑page image) | Using lossless PNG as source; OCR adds a full‑resolution image | Downscale the image before OCR (`image.thumbnail((1240, 1754))` for A4). |
| Script crashes on Windows with “tesseract.exe not found” | Tesseract binary not on PATH | Add `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (adjust path). |

---

## Full, Ready‑to‑Run Script

Putting it all together, here’s a single file you can copy‑paste and run:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Save this as `create_searchable_pdf.py`, replace the placeholders with real paths, and run:

```bash
python create_searchable_pdf.py
```

You should see a


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR Recognizing PDF Documents in Aspose.OCR for Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}