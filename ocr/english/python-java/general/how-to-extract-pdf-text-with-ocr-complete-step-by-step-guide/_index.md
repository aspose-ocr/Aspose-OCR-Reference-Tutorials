---
category: general
date: 2026-03-26
description: How to extract PDF text using OCR. Learn to load PDF as image, recognize
  PDF text and extract text from PDF with a simple Python example.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: en
og_description: How to extract PDF text using OCR. This guide shows you how to load
  PDF as image, recognize PDF text and extract text from PDF in Python.
og_title: How to Extract PDF Text with OCR – Full Tutorial
tags:
- OCR
- Python
- PDF processing
title: How to Extract PDF Text with OCR – Complete Step‑by‑Step Guide
url: /python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Extract PDF Text with OCR – Complete Step‑by‑Step Guide

Ever wondered **how to extract PDF** files that are actually just scanned images? You’re not alone—many developers hit this wall when they need searchable content but only have image‑only PDFs. The good news? A few lines of code and a solid OCR library can turn those picture‑PDFs into plain text in a flash.  

In this tutorial we’ll walk through **how to use OCR** to load a PDF as an image, recognize PDF text, and finally **extract text from PDF** documents of any length. By the end you’ll have a runnable script, a clear explanation of each step, and a handful of tips to avoid the usual pitfalls.

## What You’ll Need

- Python 3.9 or newer (the code works on 3.10+ as well)  
- The `ocr` Python package (or any compatible OCR library that exposes `OcrEngine`, `OcrEngineMode`, and `Imaging.Image`)  
- A multi‑page PDF you want to process (for demo we’ll call it `multi_page.pdf`)  
- Basic familiarity with virtual environments (optional but recommended)

> **Pro tip:** If you’re on Windows, consider using the Anaconda Prompt; on macOS/Linux, a simple `python -m venv venv && source venv/bin/activate` does the trick.

## Step 1: Install the OCR Library

First, grab the OCR package from PyPI. The example below uses a fictional `ocr` package that mirrors the API shown in the code snippet, but most real‑world libraries (like `pytesseract` + `pdf2image`) follow the same pattern.

```bash
pip install ocr
```

If you’re using a different engine, replace `ocr` with the appropriate name (e.g., `pip install pytesseract pdf2image`).

## Step 2: Initialize the OCR Engine

Creating an engine instance is the foundation of **how to extract PDF** text. Think of the engine as the brain that will interpret the pixels inside each PDF page.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Why this matters:** `set_engine_mode` lets you trade speed for accuracy. `DEFAULT` is a balanced choice; if you need higher precision, switch to `HIGH_ACCURACY` (if the library supports it).

## Step 3: Load the PDF as an Image Object

OCR works on images, not PDF containers, so we must convert the PDF into an image representation first. The `Imaging.Image.load` method handles multi‑page PDFs automatically.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Edge case:** Some libraries only accept a single‑page image. In that scenario, you’d loop through each page using `pdf2image.convert_from_path`. Our `load` call abstracts that away, making **load pdf as image** a one‑liner.

## Step 4: Recognize Text on All Pages

Now comes the core of **recognize PDF text**. The engine scans every page, returning a list of result objects—one per page.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Each `page_result` contains methods like `get_text()` (plain text) and `get_confidence()` (optional quality metric).  

> **Tip:** If you only need the first page, call `recognize(pdf_image[0])` instead of the multi‑page helper.

## Step 5: Iterate Through Results and Output the Extracted Text

Finally, we loop over the results, printing each page’s text. This completes the **extract text from PDF** workflow.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Expected Output

If `multi_page.pdf` contains three pages with the words “Hello”, “World”, and “Python”, you’ll see:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

That’s it—your PDF is now fully searchable and the text is ready for downstream processing (indexing, sentiment analysis, you name it).

## Step 6: Handling Common Pitfalls

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blank output** | PDF pages are scanned at low DPI, making characters indistinguishable. | Upscale the image before OCR: `pdf_image = pdf_image.resize(300)` (300 DPI is a sweet spot). |
| **Garbage characters** | Non‑Latin alphabets need language packs. | Load the appropriate language model: `ocr_engine.load_language('spa')` for Spanish, etc. |
| **Memory blow‑up on huge PDFs** | Loading all pages at once consumes RAM. | Process pages in chunks: `for img in pdf_image.split(batch=10): …` (pseudo‑code). |
| **Slow performance** | Using `DEFAULT` on a massive document can be sluggish. | Switch to `FAST` mode or run OCR in parallel using `concurrent.futures`. |

## Bonus: Saving Extracted Text to a File

Most real‑world pipelines need the text persisted. Here’s a tiny helper that writes everything to `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Now you can feed `output.txt` into a search engine, a database, or any NLP model.

## Putting It All Together – Full Script

Below is the complete, ready‑to‑run program. Copy‑paste, adjust the file paths, and you’re good to go.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Run it:

```bash
python extract_pdf_ocr.py
```

You should see each page’s content printed to the console, followed by a confirmation that the file `extracted_text.txt` was created.

## Conclusion

We’ve covered **how to extract PDF** text from image‑only documents using an OCR engine, from installing the library to handling multi‑page results and saving the output. You now know **how to use OCR**, how to **load PDF as image**, and how to **recognize PDF text** reliably.  

Next steps? Try swapping the default engine mode for a high‑accuracy setting, experiment with language packs for multilingual PDFs, or pipe the extracted text into a full‑text search index like Elasticsearch. The sky’s the limit once you’ve mastered the basics of extracting text from PDF files.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="how to extract pdf workflow diagram"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}