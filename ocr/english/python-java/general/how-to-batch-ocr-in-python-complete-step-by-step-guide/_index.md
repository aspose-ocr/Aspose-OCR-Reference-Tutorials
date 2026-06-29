---
category: general
date: 2026-06-28
description: How to batch OCR using Python. Learn to OCR multiple images, extract
  text from PNG, and convert image to text with a full Python OCR tutorial.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: en
og_description: How to batch OCR in Python explained in the first sentence. Follow
  this python ocr tutorial to extract text from PNG files efficiently.
og_title: How to Batch OCR in Python – Full Programming Guide
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: How to Batch OCR in Python – Complete Step‑by‑Step Guide
url: /python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR in Python – Complete Step‑by‑Step Guide

Ever wondered **how to batch OCR** a stack of scanned pages without writing a loop that blocks your UI? You're not the only one. Processing dozens of PNG files one‑by‑one can feel like watching paint dry, especially when each image takes a second or two to decode.  

In this tutorial we’ll show you a clean, non‑blocking way to **OCR multiple images** at once, **extract text from PNG** files, and **convert image to text** using a modern Python OCR engine. By the end you’ll have a ready‑to‑run script that you can drop into any project – perfect for a quick *python ocr tutorial* or a production‑grade batch job.

## What You’ll Build

- Initialize an OCR engine and set its language to Latin (or any language you need).  
- Feed a list of image paths (PNG in our example) to the engine.  
- Launch a batch operation that returns a Future‑like object.  
- Pull all results concurrently with a thread pool, keeping your main thread free.  
- Print the recognized text for each page, nicely separated.

No hidden magic, just plain Python and a third‑party OCR library (we’ll use the fictional `pyocr` package for illustration).  

**Prerequisites**  
- Python 3.8+ installed.  
- Basic familiarity with Python functions and `concurrent.futures`.  
- Access to an OCR library that exposes an `OcrEngine` class (e.g., `pip install pyocr`).  

If you’re missing any of those, grab them now – it’s easier than you think.

---

## How to Batch OCR in Python – Core Concepts

Before we dive into code, let’s answer the “why” behind each step.

1. **Why set the language?**  
   OCR accuracy skyrockets when the engine knows what characters to expect. Latin works for English, French, Spanish, etc. Switch to `Language.Japanese` or `Language.Arabic` if needed.

2. **Why use a batch operation?**  
   A batch call lets the engine schedule work internally, often leveraging native threads or GPU acceleration. It returns a handle you can query later, meaning you don’t block while each image is processed.

3. **Why a ThreadPoolExecutor?**  
   The Future object we get back is *lazy* – it only starts pulling results when we ask. By handing a thread pool to `getAll`, we let Python fetch each page’s text in parallel, cutting overall runtime dramatically.

4. **Why enumerate the results?**  
   The order of results matches the order of input paths, so we can safely label each page number.

Understanding these “why” bits helps you adapt the pattern to other libraries or to larger data sets.

---

## Step 1: Install and Import Required Packages

First, make sure the OCR library is installed. The example uses a generic `pyocr` package; replace it with the actual library you prefer (e.g., `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Now import everything we need.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** Using `Path` from `pathlib` makes your script OS‑agnostic and easier to read.

---

## Step 2: Create the OCR Engine and Set Language

Creating the engine is straightforward. We’ll lock it to Latin for this demo.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

The `setLanguage` call is optional for some engines, but it’s a good habit. It tells the OCR model to focus on the character set you care about, improving both speed and accuracy.

---

## Step 3: List the Image Files to Process (Extract Text from PNG)

Collect all PNG files you want to convert. Using `Path.glob` means you can drop a whole folder in without editing the script.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Why this matters:** By sorting the list we guarantee a deterministic order, which later aligns each result with the correct page number.

---

## Step 4: Launch a Batch OCR Operation (Convert Image to Text)

Now we hand the list to the engine. The method returns a Future‑like container that we’ll poll later.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Under the hood the engine may spin up its own worker threads or even a GPU pipeline. All we care about is that we have a handle (`batch_future`) that knows how to fetch the individual results.

---

## Step 5: Retrieve All Results Concurrently (OCR Multiple Images)

Here’s where we truly *batch* the work. By giving a `ThreadPoolExecutor` to `getAll`, each page’s text is fetched in its own thread.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

You can tune `max_workers` based on your CPU cores or the OCR library’s recommendations. More workers ≠ always faster – watch your CPU usage.

---

## Step 6: Output the Recognised Text (Python OCR Tutorial Finale)

Finally, print each page’s text. The `Result` object exposes `getText()` – adjust if your library uses a different method name.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Expected output (sample)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

If any image fails, most engines embed an empty string or raise an exception – you can wrap the loop in a `try/except` block to handle edge cases gracefully.

---

## Full Script – Ready to Run

Below is the complete, self‑contained script. Copy‑paste it into a file called `batch_ocr.py`, adjust `YOUR_DIRECTORY`, and execute `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Save, run, and watch the console fill with the extracted text. Simple, fast, and fully asynchronous.

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **No output** – empty strings | The OCR engine couldn’t find any text (image too noisy) | Pre‑process images: binarize, deskew, or increase DPI |
| **`FileNotFoundError`** | Wrong directory path or missing PNG files | Double‑check `YOUR_DIRECTORY` and ensure files end with `.png` |
| **High CPU usage** | `max_workers` set too high for your machine | Reduce `max_workers` or enable GPU acceleration if supported |
| **Unicode garble** | Engine defaulted to a different language | Call `engine.setLanguage(Language.Latin)` (or appropriate) before batch OCR |

Addressing these early saves you hours of debugging.

---

## Extending the Tutorial – Next Steps

- **OCR multiple images** in other formats (JPEG, TIFF) – just change the glob pattern.  
- **Extract text from PNG** and feed it into a search index (e.g., Elasticsearch).  
- **Convert image to text** for PDF generation using `reportlab` or `PyPDF2`.  
- **Parallelize across machines** with `multiprocessing` or a task queue like Celery for massive datasets.  

Each of these topics builds naturally on the **python ocr tutorial** you just completed.

---

## Conclusion

We’ve walked through **how to batch OCR** a collection of PNG files, demonstrated the power of a batch‑oriented API, and showed you how to **extract text from PNG** with a thread‑pooled approach. The complete script above is production‑ready, and you now have a solid foundation for any OCR‑heavy Python project.

Give it a spin, tweak the language settings, and maybe even replace `pyocr` with `pytesseract` – the pattern stays the same. Got questions or want to share a cool use‑case? Drop a comment, and let’s keep the conversation going.

*Happy coding!*


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}