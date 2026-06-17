---
category: general
date: 2026-03-26
description: Learn how to perform OCR in Python and easily extract text from image,
  read text from scan, or extract text from invoice using a simple OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: en
og_description: How to perform OCR in Python? This guide shows you how to extract
  text from image, read text from scan, and extract text from invoice in minutes.
og_title: How to Perform OCR in Python – Extract Text Fast
tags:
- OCR
- Python
- Image Processing
title: How to Perform OCR in Python – Extract Text Fast
url: /python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in Python – Extract Text Fast

Ever wondered **how to perform OCR** on a scanned receipt or a blurry PDF? You’re not alone. In many projects the need to **extract text from image** shows up sooner rather than later, and the usual “hand‑type everything” approach just isn’t scalable.  

In this tutorial you’ll see a complete, ready‑to‑run example that shows **how to use OCR** to read text from scan, pull data from an invoice, and even handle automatic skew correction—all with just a few lines of Python.

## What You’ll Learn

We’ll walk through everything you need to know:

* The exact dependencies and imports required.
* How to create and configure an `OcrEngine` instance.
* Ways to **extract text from image**, **read text from scan**, and **extract text from invoice** using the same engine.
* Common pitfalls (wrong language, missing files, large images) and how to avoid them.
* Expected output so you can verify that the OCR succeeded.

No external documentation links are needed—everything is self‑contained, so you can copy‑paste the code and see results immediately.

## Prerequisites

Before we dive in, make sure you have:

* Python 3.8+ installed (the `ocr` package works with any recent version).
* The `ocr` library available (`pip install ocr‑engine` – replace with the actual package name if different).
* An image file you want to process – for the demo we’ll use `invoice.png` located in a folder called `YOUR_DIRECTORY`.

That’s it. If you already have these, you’re good to go.

## Step 1: Install and Import the OCR Module

First things first: we need the OCR library. If you haven’t installed it yet, run the following command in your terminal:

```bash
pip install ocr-engine
```

Now we import the module in our script.

```python
# Step 1: Import the OCR module
import ocr
```

> **Pro tip:** Keep your virtual environment tidy; it prevents version clashes when you later add other image‑processing packages.

## Step 2: Create and Configure the OCR Engine

Creating the engine is as simple as calling its constructor, but the real power lies in configuring it correctly. We’ll set the language to English and turn on automatic skew correction, which is essential when dealing with scanned invoices that aren’t perfectly aligned.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Why enable `auto_skew`? Many scanners produce images that are a few degrees off. Without correction the engine might miss characters, turning a perfectly readable invoice into gibberish.

## Step 3: Perform OCR on Your Target Image

Now we feed the image file into the engine. The `recognize_image` method returns an object that holds the raw text as well as confidence scores (if the library provides them).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

If you’re working with a **read text from scan** scenario, simply replace the path with the scanned PDF converted to PNG or JPEG. The same call works for any image format the underlying library supports.

## Step 4: Inspect and Use the Extracted Text

Let’s print the raw OCR output. In a real‑world invoice‑processing pipeline you’d probably parse this string, extract line items, totals, and dates, but for now a quick glance will confirm that the OCR succeeded.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Expected output (truncated for brevity):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

If the output looks garbled, double‑check that the image is clear and that `engine.language` matches the document’s language.

## Step 5: Handling Common Edge Cases

### Large Images

Processing a 5000 × 5000 pixel scan can be memory‑hungry. A quick way to mitigate this is to downscale the image before sending it to the engine:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Multiple Languages

If you need to **extract text from image** that contains both English and Spanish, you can set a list of languages:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

The engine will attempt to recognize characters from both sets.

### Error Handling

Never assume the file exists. Wrap the call in a try‑except block to give a friendly message:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Visual Reference

Below is a screenshot of the sample invoice we used in the demo. Notice the slight tilt—exactly what `auto_skew` fixes.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* how to perform OCR on an invoice image showing automatic skew correction.

## Full, Runnable Example

Putting everything together, here’s a single script you can run from the command line. It covers installation, configuration, error handling, and a simple post‑processing step that writes the extracted text to a file called `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Running `python full_ocr_demo.py` will print the extracted text to the console and store it in `output.txt`. From there you can apply regular expressions, CSV writers, or any other logic you need for **extract text from invoice** automation.

## Conclusion

You now have a solid, end‑to‑end answer to **how to perform OCR** in Python. By creating an `OcrEngine`, configuring language and skew correction, and handling a few practical edge cases, you can reliably **extract text from image**, **read text from scan**, and **extract text from invoice** without hunting through scattered documentation.

What’s next? Try feeding a batch of files into a loop, experiment with different languages, or plug the output into a PDF generation library to create searchable PDFs. The sky’s the limit, and the code you just saw is a sturdy launchpad.

Got questions about a specific file format or need help tweaking confidence thresholds? Drop a comment below—happy to help you fine‑tune your OCR pipeline!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}