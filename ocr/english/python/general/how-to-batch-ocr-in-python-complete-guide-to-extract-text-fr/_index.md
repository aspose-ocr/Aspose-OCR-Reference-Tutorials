---
category: general
date: 2026-06-28
description: How to batch OCR in Python—extract text from images and convert scanned
  pages to text using batch OCR processing.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: en
og_description: Learn how to batch OCR in Python, extract text from images, and convert
  scanned pages to text with efficient batch OCR processing.
og_title: How to Batch OCR in Python – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: How to Batch OCR in Python – Complete Guide to Extract Text from Images
url: /python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR in Python – Complete Guide to Extract Text from Images

If you're wondering **how to batch OCR in Python**, you're in the right place. This tutorial shows you a quick way to **extract text from images** and **convert scanned pages to text** using a single OCR engine instance. No more copy‑pasting one file after another—let the code do the heavy lifting.

We'll walk through everything you need: installing the library, loading a whole folder of scans, running batch OCR processing, and handling the results gracefully. By the end you’ll have a reusable script that turns a stack of PNGs or JPEGs into searchable text files in seconds.

## What You’ll Need

Before we dive in, make sure you have:

* Python 3.9+ installed (the code works on 3.8 as well, but 3.9+ gives you the newest typing features).
* A modern OCR library—here we use **Aspose.OCR for Python via .NET**, which exposes the `OcrEngine` class shown in the original snippet.  
  ```bash
  pip install aspose-ocr
  ```
* A folder with scanned pages (`page1.png`, `page2.png`, …). Anything Pillow can open will work, so PDFs, TIFFs, or BMPs are fine too.
* A tiny bit of curiosity—if you’ve never automated image‑to‑text before, you’re about to see why batch OCR is a game‑changer.

> **Pro tip:** If you prefer a pure‑Python library, swap `OcrEngine` for `pytesseract.image_to_string`. The surrounding logic stays identical.

## How to Batch OCR in Python – Step‑by‑Step Guide

Below is the complete, runnable script. Every line is commented so you can see *why* each piece matters, not just *what* it does.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Expected Output

Running the script against a folder with three PNG scans produces something like:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

The preview shows the first 200 characters of each page, and the full text lives in the `ocr_output` directory.

## Extract Text from Images Using a Single Engine

Why do we create **one** `OcrEngine` and reuse it? Instantiating the engine can be expensive because it loads language packs and native DLLs. By sharing the same instance across the batch, you:

* **Save memory** – only one set of resources lives in RAM.
* **Boost speed** – the engine stays warm, avoiding repeated initialization.
* **Maintain consistency** – same recognition settings apply to every page, which is essential when you want to **extract text from images** that share the same layout.

If you need to tweak recognition (e.g., enable spell‑check or change the language), do it *before* calling `recognize_batch`. All subsequent pages will inherit those settings automatically.

## Convert Scanned Pages to Text Efficiently

The heart of the problem—**convert scanned pages to text**—is solved by `engine.recognize_batch(images)`. Under the hood the library processes each image in a background thread pool, so you get near‑linear scaling on multi‑core machines. A few things to keep in mind:

* **Image quality matters** – 300 dpi or higher yields the best results. If your scans are low‑resolution, consider up‑sampling with Pillow before feeding them to the engine.
* **Color vs. grayscale** – OCR engines usually work faster on 8‑bit grayscale. You can add a preprocessing step:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Language support** – Aspose.OCR supports over 40 languages. Set `engine.language = "eng"` or `"fra"` before the batch call if you’re not working with English.

## Batch OCR Processing Best Practices

Even though the code above is already concise, production‑grade batch OCR often requires a few extra safeguards:

| Concern | Recommended Approach |
|---------|----------------------|
| **Large batches ( > 500 files )** | Split into chunks of 100–200 images to keep memory footprints modest. |
| **Corrupt or unsupported files** | The `load_images` helper already catches exceptions and logs a warning; you can also write a fallback to skip or move bad files. |
| **Progress monitoring** | Wrap `recognize_batch` in a loop that yields after each image if the library exposes per‑image callbacks. |
| **Post‑processing** | Run a spell‑check or regex cleanup on the resulting strings to improve downstream searchability. |
| **Parallelism** | If you have a multi‑node setup, distribute folders across workers and merge the `.txt` outputs at the end. |

These tips help you scale **batch OCR processing** from a handful of pages to thousands without crashing your script.

## Frequently Asked Questions

**Q: Can I use this with PDFs directly?**  
A: Absolutely. Convert each PDF page to an image first (e.g., using `pdf2image`) and feed the resulting list to `recognize_batch`. The rest of the pipeline stays unchanged


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}