---
category: general
date: 2026-06-19
description: Perform OCR on image using Python's ocr library. Learn how to detect
  text from image, recognize text from jpeg, and extract text from scanned image efficiently.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: en
og_description: Perform OCR on image with Python and extract text from scanned files.
  This guide walks you through loading images, deskewing, and recognizing text step‑by‑step.
og_title: Perform OCR on Image in Python – Full Text Extraction Guide
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Perform OCR on Image in Python – Full Text Extraction Guide
url: /python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image in Python – Full Text Extraction Guide

Ever needed to **perform OCR on image** files but kept hitting a wall because the code looked cryptic? You're not the only one. Whether you're turning a pile of scanned receipts into searchable PDFs or pulling captions from a JPEG for a data‑science project, the ability to recognize text from JPEGs and other formats is a must‑have skill for any developer today.

In this tutorial we'll walk through a complete, runnable example that shows you how to **detect text from image** files, **extract text from scanned image** documents, and even **load image for OCR** in just a handful of lines. By the end, you’ll have a solid, production‑ready snippet you can drop into your own projects—no missing imports, no vague “see docs” shortcuts.

## What You’ll Build

- A tiny Python script that creates an OCR engine, enables auto‑deskew, loads a JPEG (or any supported format), and prints the recognized text.
- Explanations of **why** each setting matters, not just **how** to type it.
- Tips for handling multi‑page PDFs, non‑English languages, and common pitfalls like blurry scans.

### Prerequisites

- Python 3.8+ installed (the example uses the `ocr` package available via `pip install ocr-lib` – replace with your actual library name).
- Basic familiarity with Python functions and virtual environments.
- An image file (JPEG, PNG, TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeholder.

> **Pro tip:** If you’re on Windows, run your terminal as Administrator when installing the OCR library to avoid permission headaches.

---

## Perform OCR on Image – Setup and Configuration

The first thing you need is a clean OCR engine instance. Think of it as the brain behind the operation; without proper configuration, even the sharpest image will return gibberish.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Why this matters:**  
Setting `engine.language` narrows the character set the OCR engine expects, dramatically boosting accuracy. If you skip this, the engine will try to guess, often misreading simple words.

---

## Enable Automatic Deskew – Fix Tilted Scans

Scanned pages are rarely perfectly flat. A slight tilt can throw off character segmentation, turning “Hello” into “H3llo”. The `auto_deskew` flag does the heavy lifting for you.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Edge case:** If you know your images are already straight, disabling deskew can shave a few milliseconds off processing time—useful when handling thousands of pages in a batch job.

---

## Load Image for OCR – Supporting JPEG, PNG, TIFF

Now we actually **load image for OCR**. The `ocr.Image.load` method is flexible; it accepts a path to any supported raster format.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Why this step is crucial:** The library reads the file into an internal bitmap, applying any necessary color space conversion. Skipping this and passing a raw byte stream would raise a `FileNotFoundError` or, worse, silently produce empty results.

If you need to **recognize text from JPEG** files specifically, just ensure the file extension is `.jpeg` or `.jpg`. The same call works for PNG (`.png`) or TIFF (`.tif`) without modification.

---

## Perform OCR on Image – Running the Engine

With the engine primed and the image in memory, it’s time to **perform OCR on image** data. This single line does the heavy lifting: pre‑processing, segmentation, classification, and text assembly.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**What happens under the hood?**  
- The engine applies the deskew transformation (if enabled).  
- It runs a neural network or Tesseract backend to identify characters.  
- Finally, it stitches characters into words and lines, returning a rich `result` object.

---

## Extract Text from Scanned Image – Output the Results

The final step is to **extract text from scanned image** and display it. The `result.text` attribute contains the plain‑text representation.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Typical output looks like:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

If the OCR engine fails to find any characters, `result.text` will be an empty string. In that case, double‑check the image quality or consider adjusting the `engine.confidence_threshold` property (if your library supports it).

---

## Handling Common Variations

### Recognize Text from JPEG vs PNG

Both formats are supported, but JPEG compression can introduce artifacts that confuse the engine. If you notice frequent mis‑recognitions, try converting the JPEG to PNG first:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Detect Text from Image with Multiple Languages

If your document mixes English and Spanish, set a multilingual mode:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

The engine will then consider both alphabets during recognition.

### Extract Text from Scanned PDFs

For PDFs, you need to rasterize each page into an image first. Libraries like `pdf2image` make this painless:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Full Working Example

Below is the complete script you can copy‑paste into a `ocr_demo.py` file. It includes error handling and a small helper to measure execution time.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Expected output** (assuming a clear scan):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Frequently Asked Questions

**Q: Can I run this on a headless server?**  
A: Absolutely. The library works without a GUI; just ensure the necessary native binaries (e.g., Tesseract) are installed on the server.

**Q: What if the image is blurry?**  
A: Consider adding a sharpening filter before `engine.recognize`. Many OCR libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s `cv2.GaussianBlur` in reverse.

**Q: Does the script support batch processing?**  
A: Yes. Wrap `perform_ocr` in a loop over a list of file paths,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}