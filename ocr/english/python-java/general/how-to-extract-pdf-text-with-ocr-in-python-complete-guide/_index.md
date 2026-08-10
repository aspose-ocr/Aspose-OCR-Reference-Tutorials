---
category: general
date: 2026-06-19
description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
  extract text from PDF, recognize text from image, and an OCR Python example.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: en
og_description: How to extract PDF using OCR in Python. Learn to extract text from
  PDF, recognize text from image, and see a complete OCR Python example.
og_title: How to Extract PDF Text with OCR in Python – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: How to Extract PDF Text with OCR in Python – Complete Guide
url: /python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Extract PDF Text with OCR in Python – Complete Guide

Ever wondered **how to extract PDF** contents when the file is just a scanned image? You're not the only one. In many real‑world projects—think contracts, invoices, or historic archives—the PDF you receive has no selectable text. The good news? A few lines of Python can turn those image‑only pages into searchable, editable text.

In this tutorial we’ll walk through a practical **OCR Python example** that reads a PDF, renders its first page as an image, and then **extracts text from PDF** using an OCR engine. By the end you’ll know exactly how to **read PDF with OCR**, why each step matters, and how to adapt the code for multi‑page documents or different languages.

## What You’ll Learn

- Install and set up a reliable OCR library for Python.  
- Convert PDF pages to images suitable for OCR.  
- **Recognize text from image** and retrieve clean Unicode strings.  
- Common pitfalls (low‑resolution PDFs, rotated pages) and how to avoid them.  
- Extending the script to handle multiple pages or batch processing.

**Prerequisites**: Python 3.8+, pip, and a basic understanding of virtual environments. No prior OCR experience required—just follow along.

---

## ## How to Extract PDF Text with OCR in Python

This H2 header contains our primary keyword right where search engines love to see it. Let’s dive straight into the code.

### Step 1 – Install the Required Packages

First, we need an OCR engine. The example below uses the popular **ocr** package (a thin wrapper around Tesseract). If you prefer a different backend, the concepts stay the same.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Pro tip:** On Linux, you’ll also need the Tesseract binary: `sudo apt-get install tesseract-ocr`. macOS users can grab it via Homebrew: `brew install tesseract`.

### Step 2 – Initialize the OCR Engine and Set Language

Now we spin up the engine and tell it to look for English characters. You can swap `ocr.Language.English` for any supported language code.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Why this matters:** Specifying the language dramatically improves accuracy because the engine can apply language‑specific dictionaries and character models.

### Step 3 – Load a PDF Page as an Image

OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based indexing).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Edge case:** If the PDF contains vector graphics rather than scanned images, you might get a crisp rendering. For low‑resolution scans, consider increasing the DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Step 4 – Recognize Text from the Rendered Image

Here’s the heart of the **ocr python example**. The engine processes the bitmap and returns an object containing the extracted string.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

The `ocr_result.text` attribute holds the plain‑text output, preserving line breaks where possible.

### Step 5 – Print or Store the Extracted Text

Finally, we output the result. In a real application you’d probably write to a file or a database.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Running the script should display something like:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

That’s a complete **extract text from pdf** workflow using OCR.

---

## ## Recognize Text from Image – Tweaking Accuracy

If you’re only interested in **recognize text from image** (say, a JPEG of a receipt), you can skip the PDF conversion step:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Tips for better results:**

- **Pre‑process** the image: convert to grayscale, apply thresholding, or deskew. Pillow makes this easy.
- **Increase DPI** during PDF rendering: higher resolution gives the OCR engine more detail.
- **Enable OCR engine’s config** for page segmentation (`ocr_engine.config = "--psm 6"` for uniform blocks).

---

## ## Read PDF with OCR – Handling Multiple Pages

Most contracts span several pages. Looping over each page is straightforward:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

This function **reads PDF with OCR**, concatenates the output, and inserts a clear page break marker. You can then feed `full_text` into a search index or store it as a `.txt` file.

---

## ## Common Pitfalls and How to Fix Them

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Garbled characters, lots of `?` | Wrong language or missing language data files | Install the correct Tesseract language pack (`tesseract-ocr-<lang>`) and set `ocr_engine.language`. |
| Missing lines or truncated words | Low DPI (under 150) | Render PDF at 300 DPI or higher (`dpi=300`). |
| Text is rotated or upside‑down | Scanned page not upright | Use `ocr.Image.deskew(page_image)` before recognition. |
| Slow processing on large PDFs | Processing pages sequentially on a single thread | Parallelize with `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Extending the OCR Python Example

- **Export to PDF/A**: After extraction, you can embed the text back into a searchable PDF using `reportlab` or `pypdf2`.
- **Language detection**: Use `langdetect` on the OCR output to switch `ocr_engine.language` dynamically.
- **Batch processing**: Walk a directory with `os.listdir` and apply `extract_all_pages` to every file.

---

## ## Expected Output and Verification

When you run the script against a clear, English‑language scan, you should see a clean block of text with proper punctuation. Verify by:

1. Comparing a few lines to the original scanned image.  
2. Running a simple word count (`len(ocr_result.text.split())`) to ensure the output isn’t empty.  
3. Optionally, feeding the result into a spell‑checker like `pyspellchecker` to spot OCR errors.

---

## Conclusion

We’ve covered **how to extract PDF** content when traditional parsing fails, demonstrated a full **ocr python example**, and explained how to **recognize text from image** and **read PDF with OCR** for both single‑page and multi‑page scenarios. With the code snippets above you can now turn any scanned PDF into searchable, editable text—no more manual re‑typing.

Next steps? Try swapping the language to Spanish (`ocr.Language.Spanish`) or experiment with image pre‑processing techniques to boost accuracy. If you’re building a document‑management system, consider indexing the extracted text with Elasticsearch for lightning‑fast search.

Got questions or run into a quirky PDF? Drop a comment, and happy coding!  

![How to extract PDF using OCR in Python](image.png "How to extract PDF using OCR in Python")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}