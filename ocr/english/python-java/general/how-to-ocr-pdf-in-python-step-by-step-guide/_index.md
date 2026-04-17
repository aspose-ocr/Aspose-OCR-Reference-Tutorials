---
category: general
date: 2026-03-28
description: Learn how to OCR PDF with Python quickly. This guide shows you how to
  extract text from PDF, recognize text from PDF, and convert scanned PDF to text
  using Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: en
og_description: Master how to OCR PDF with Python. Extract text from PDF, recognize
  text from PDF, and convert scanned PDF to text in minutes.
og_title: How to OCR PDF in Python – Complete Guide
tags:
- PDF
- OCR
- Python
- Aspose
title: How to OCR PDF in Python – Step‑by‑Step Guide
url: /python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to OCR PDF in Python – Step‑by‑Step Guide

Ever wondered **how to OCR PDF** when the file is just a picture of a page? You're not the only one. In this tutorial we'll walk through the exact steps to OCR PDF files, extract text from PDF, and turn a scanned PDF into searchable text—all with plain Python code.

We'll cover everything from installing the Aspose OCR library to pulling the recognized text out of each page. By the end you’ll be able to **OCR PDF with Python**, **extract text from PDF**, and **convert scanned PDF to text** without hunting through scattered docs. No fluff, just a practical, runnable example you can copy‑paste.

## What You’ll Need

Before we dive in, make sure you have:

* Python 3.8+ (the latest stable release works best)  
* An Aspose OCR for Python license or a free trial key – you can grab it from the Aspose website.  
* A scanned PDF you want to process (we’ll call it `input.pdf`).  

If you’ve already got those, great—let’s get started. If not, installing the package is a breeze and we’ll show you how.

## How to OCR PDF – Setting Up the Environment

The first thing you have to do is get the Aspose OCR module onto your machine. The package is called `aspose-ocr`, and you can install it via pip:

```bash
pip install aspose-ocr
```

> **Pro tip:** Use a virtual environment (`python -m venv venv`) so your dependencies stay tidy.

Once the package is installed, you’re ready to import it and start the OCR engine. This is the foundation for every **ocr pdf with python** workflow you’ll build later.

## OCR PDF with Python – Importing Aspose OCR

Now that the library is available, let’s bring it into our script. We’ll also set the engine to work in *direct PDF mode*, which tells Aspose to read the PDF bytes straight from the file instead of converting each page to an image first.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Why use `PdfMode.DIRECT`? Because it skips an extra rasterization step, making the process faster and preserving the original layout—especially handy when you need **recognize text from PDF** accurately.

## Recognize Text from PDF – Running the Engine

With the engine ready, point it at your scanned file. The `recognize_from_pdf` method does all the heavy lifting: it parses every page, runs the OCR algorithm, and returns an `OcrResult` object that contains a collection of `Page` objects.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

If you’re wondering whether this works with encrypted PDFs—yes, as long as you supply the password via `ocr_engine.password = "secret"` before calling `recognize_from_pdf`. That’s an edge case many tutorials skip, but it’s useful in real‑world pipelines.

## Extract Text from PDF – Accessing Page Results

The `ocr_result.pages` list holds one entry per page. Each `Page` object has a `.text` attribute that contains the plain‑text representation of the scanned page. Let’s loop through and print the results so you can see exactly what was extracted.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Running the script will output something like:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

That output proves you’ve successfully **extract text from PDF** and **recognize text from PDF** using Aspose OCR. You can now pipe the strings into a database, a search index, or any downstream NLP pipeline.

![how to ocr pdf example](placeholder-image.png "how to ocr pdf example")

*Image alt text:* **how to ocr pdf example** – shows console output of recognized text per page.

## Convert Scanned PDF to Text – Saving the Output

Most developers don’t just want to see the text on the console; they need a persistent file. Below is a tiny helper that writes each page’s text to a separate `.txt` file, effectively **convert scanned PDF to text** in a folder called `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

After the script finishes you’ll have a tidy directory:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Now you’ve fully **convert scanned PDF to text** and can feed those files into any downstream process—search, analytics, or even a simple `grep`.

## Common Questions & Edge Cases

**What if my PDF contains images mixed with real text?**  
Aspose OCR will try to recognize everything, but you can speed things up by disabling OCR for pages that already contain selectable text. Set `ocr_engine.auto_detect_page_orientation = True` and then call `ocr_engine.recognize_from_pdf(..., detect_text=False)` for known-good pages.

**Can I control the language model?**  
Absolutely. Set `ocr_engine.language = aocr.Language.English` (or any supported language) before calling `recognize_from_pdf`. This improves accuracy for non‑English documents.

**How do I handle very large PDFs (100+ pages)?**  
Process them in chunks. The `recognize_from_pdf` method accepts a `page_range` argument, e.g., `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Loop over ranges to keep memory usage low.

## Full Working Example

Putting it all together, here’s a single script you can drop into a file called `ocr_pdf.py` and run:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Run it with:

```bash
python ocr_pdf.py
```

You should see console output confirming each page’s text and the location of the saved `.txt` files.

## Conclusion

We’ve covered **how to OCR PDF** using Python, demonstrated a clean way to **ocr pdf with python**, showed you how to **extract text from PDF**, explained the mechanics behind **recognize text from PDF**, and finally gave a ready‑to‑use snippet that **convert scanned PDF to text**. The whole process is wrapped

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}