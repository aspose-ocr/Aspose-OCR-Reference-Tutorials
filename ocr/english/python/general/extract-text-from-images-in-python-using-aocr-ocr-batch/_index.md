---
category: general
date: 2026-06-25
description: Extract text from images with Python aocr library – learn batch OCR,
  set recognition mode printed, and add an AI postprocessor.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: en
og_description: Extract text from images using Python aocr library. This tutorial
  shows batch OCR, printed recognition mode, and optional AI postprocessor.
og_title: Extract Text from Images in Python – Complete aocr Batch Guide
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extract Text from Images in Python Using aocr OCR Batch
url: /python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Images in Python Using aocr OCR Batch

Ever needed to **extract text from images** but felt overwhelmed by dozens of tiny steps? You're not the only one. Whether you're digitizing scanned forms, pulling data from receipts, or building a searchable archive, getting reliable OCR results at scale can feel like climbing a steep hill.

The good news? With the **aocr library** you can spin up a full **Python OCR batch** in just a handful of lines. In this guide we’ll walk through creating an OCR batch, loading every supported image from a folder, picking the right **recognition mode printed**, and even attaching an **AI postprocessor** for that extra boost in accuracy. By the end you’ll have a ready‑to‑run script that extracts text from images and tells you how much was captured per file.

## What You’ll Learn

- How to install and import the `aocr` package.
- Setting up an `OcrBatch` to handle thousands of files automatically.
- Choosing the optimal recognition mode for printed documents.
- (Optional) Hooking an AI post‑processor to clean up noisy results.
- Displaying each file path alongside the length of its extracted text.
- Tips for handling edge cases like unsupported formats or empty pages.

### Prerequisites

- Python 3.8 or newer installed on your machine.  
- Basic familiarity with Python scripting (loops, imports, etc.).  
- Access to a folder of scanned images (PNG, JPG, TIFF, etc.).  

If you’ve got those, let’s dive in—no external services required.

## Step 1: Install the aocr Library

First things first. The `aocr` package isn’t part of the standard library, so you’ll need to pull it from PyPI.

```bash
pip install aocr
```

> **Pro tip:** Use a virtual environment (`python -m venv .venv`) to keep dependencies isolated.  

Once installed, you can import the core classes.

```python
# core imports
import aocr
```

## Step 2: Create an OCR Batch Instance

An `OcrBatch` is the workhorse that will crawl your directory and keep track of every image file. Think of it as a conveyor belt that feeds pictures into the OCR engine.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

At this point the batch is empty, but we’ll fill it in the next step.

## Step 3: Add All Supported Images from a Folder (Recursively)

You probably have a nested folder structure—maybe one sub‑folder per client or per month. The `add_folder` method walks the tree for you, pulling in every image it knows how to read.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Replace `"YOUR_DIRECTORY/scanned_forms/"` with the real path on your system. After this call `ocr_batch.file_paths` holds a list of absolute file names, and the batch knows exactly how many items it will process.

## Step 4: Choose the Recognition Mode for Printed Text

The `aocr` engine supports several modes (handwritten, printed, mixed). Since we’re dealing with clean, printed forms, set the mode accordingly. This tiny flag can dramatically improve accuracy because the engine skips the heavy‑handed heuristics needed for cursive scripts.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Why it matters:** Printed text has consistent baselines and character shapes, letting the OCR model apply tighter character dictionaries. If you leave the mode on “auto” you might get extra noise on low‑resolution scans.

## Step 5: (Optional) Attach an AI Post‑Processor

If your scans suffer from blur, low contrast, or unusual fonts, an AI post‑processor can clean up the raw OCR output before you hand it off to downstream systems. The `set_ai_postprocessor` method expects an object that implements a `process(text: str) -> str` interface.

Below is a minimal example using a fictional `SimpleCleaner` class. In practice you could plug in a HuggingFace transformer, a custom language model, or even a rule‑based spell‑checker.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

If you skip this step, the batch will simply return the raw OCR strings.

## Step 6: Run OCR on the Entire Batch and Collect Results

Now the heavy lifting begins. The `run` method loops over every file, runs the OCR engine, pipes the output through the optional AI post‑processor, and returns a list of strings—one per image.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Because the method returns a plain Python list, you can treat it like any other collection—store it, write it to a CSV, or feed it into a database.

## Step 7: Display Each File Path with the Length of Its Extracted Text

A quick sanity check is to print out how many characters were extracted from each file. If a page is blank or the OCR failed, you’ll see a length of `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Typical output looks like:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Seeing a `0` flag instantly tells you which files need a second look (maybe they’re corrupted or not an image at all).

## Handling Common Edge Cases

### 1. Unsupported File Types

`aocr` silently skips files it can’t decode. If you suspect you have PDFs or BMPs mixed in, filter them beforehand:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Large Batches and Memory Consumption

Running thousands of high‑resolution scans can balloon memory usage. Mitigate this by processing in chunks:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Empty or Low‑Contrast Pages

If a page yields fewer than 10 characters, you might want to flag it for manual review:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Full Working Example

Putting it all together, here’s a script you can copy‑paste and run immediately. Save it as `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Expected output** (truncated for brevity):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Run it with:

```bash
python batch_ocr.py
```

If everything is set up correctly, you’ll see a line for every image, each reporting the character count of the extracted text.

## Frequently Asked Questions

**Q: Does this work on PDFs?**  
A: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to PNG/TIFF first (e.g., using `pdf2image`).

**Q: Can I change the recognition mode to handwritten?**  
A: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`. Expect a slower run time but better results on cursive notes.

**Q: What if I need multilingual support?**  
A: The library ships with language packs. Install the desired language module (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language = "fr"` before running.

## Next Steps and Related Topics

- **Parallel processing:** Wrap the batch execution in a `concurrent.futures.ThreadPoolExecutor` to utilize multiple CPU cores.  
- **Storing results:** Write `ocr_results` to a CSV or SQLite database for downstream analytics.  
- **Integrating with cloud AI:** Swap the `SimpleCleaner` with a transformer model from HuggingFace for state‑of‑the‑art spelling correction.  
- **Fine‑tuning aocr:** If you have a custom font set, explore `aocr.Trainer` to improve the printed‑mode accuracy.

---

That’s it—you now have a solid


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}