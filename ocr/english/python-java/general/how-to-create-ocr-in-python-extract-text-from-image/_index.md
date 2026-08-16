---
category: general
date: 2026-04-26
description: How to create OCR quickly and reliably. Learn to extract text from image,
  load image for OCR, and run OCR on PNG with a custom dictionary.
draft: false
keywords:
- how to create OCR
- extract text from image
- extract text scanned document
- load image for OCR
- run OCR on png
language: en
og_description: How to create OCR in Python and extract text from image. This guide
  shows how to load image for OCR, run OCR on PNG, and use a custom dictionary.
og_title: How to Create OCR in Python – Fast Text Extraction
tags:
- OCR
- Python
- Image Processing
title: How to Create OCR in Python – Extract Text from Image
url: /python-java/general/how-to-create-ocr-in-python-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Create OCR in Python – Step‑by‑Step Guide

Ever wondered **how to create OCR** that can read your scanned PDFs, screenshots, or handwritten notes? You're not alone. In many real‑world projects we need to *extract text from image* files, but the out‑of‑the‑box engines often stumble on domain‑specific words.  

In this tutorial you’ll see a complete, runnable example that loads an image for OCR, applies a custom dictionary, and finally **run OCR on PNG** files. By the end you’ll be able to extract text from any image and adapt the engine to your own terminology.

## What This Tutorial Covers

We'll walk through every single step you need:

* Installing the tiny yet powerful `aocr` package (or any compatible library).  
* Configuring a **custom dictionary** so that terms like `aspocorp` or `licensekey` are recognized.  
* **Loading an image for OCR**, whether it’s a PNG, JPEG, or a scanned PDF page.  
* Running the OCR process and printing the result.  

No external documentation links, just a self‑contained solution you can copy‑paste and run today.

### Prerequisites

* Python 3.8 or newer (the code uses f‑strings).  
* Basic familiarity with the command line – you’ll type a couple of `pip install` commands.  
* An image file (`technical_doc.png` in the example) placed somewhere you can reference.  

If you meet those three items, you’re good to go.  

---

## Step 1: Install the OCR Library

First, we need an OCR engine that supports a programmable configuration object. The `aocr` package is a lightweight wrapper around a native OCR engine and works well for demos.

```bash
# Install the library (run once)
pip install aocr
```

> **Pro tip:** If you’re on Windows and hit a compilation error, try `pip install aocr‑binary` which ships pre‑built wheels.

### Why Install This Library?

`aocr` gives us direct access to a `config` object where we can inject a **custom dictionary**. That’s the secret sauce for improving accuracy on niche vocabularies.

---

## Step 2: Create the OCR Engine Instance & Add a Custom Dictionary

Now we spin up the engine and tell it which words it should treat as known.

```python
from aocr import OcrEngine

# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()

# Provide a custom dictionary to improve recognition of domain‑specific terms
ocr_engine.config.custom_dictionary = [
    "aspocorp",      # our company's brand name
    "ocrengine",    # the library name itself
    "licensekey"    # a common field in our contracts
]
```

### Why a Custom Dictionary Matters

Standard OCR models are trained on generic corpora. When the model sees “aspocorp”, it might split it into “aspo corp” or drop letters entirely. By feeding a custom list, we bias the recognizer toward the exact spelling we need, dramatically cutting post‑processing effort.

---

## Step 3: Load the Image You Want to Process

Here’s where we **load image for OCR**. The `Image.load` method accepts a path string and automatically determines the file type.

```python
import aocr

# Step 3: Load the image that contains the text you want to extract
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/technical_doc.png")
```

> **Edge case:** If your source is a multi‑page PDF, convert each page to PNG first (e.g., with `pdf2image`) and feed them one‑by‑one to the engine.

### Tips for Better Image Quality

* Keep the resolution at least 300 dpi.  
* Ensure the image is upright; rotate with `Pillow` if necessary.  
* Convert colored scans to grayscale to reduce noise.

---

## Step 4: Run the OCR Process on the PNG File

With the engine configured and the image loaded, we finally **run OCR on PNG**.

```python
# Step 4: Run the OCR process
ocr_result = ocr_engine.process()
```

The `process()` call returns an object that contains the recognized text, confidence scores, and bounding boxes for each word.

---

## Step 5: Output the Recognized Text

The simplest way to see what the engine found is to print the `text` attribute.

```python
# Step 5: Output the recognized text
print(ocr_result.text)
```

### Expected Output

If `technical_doc.png` contains the sentence *“The Aspocorp licensekey expires on 2025‑12‑31.”*, the console should display:

```
The Aspocorp licensekey expires on 2025-12-31.
```

Notice how the custom dictionary kept the brand name intact—something a vanilla OCR might have mangled.

---

## Full Working Example (Copy‑Paste Ready)

Below is the entire script, ready to be saved as `run_ocr.py`. Just replace the placeholder path with the location of your image.

```python
# run_ocr.py
# -------------------------------------------------
# Complete example showing how to create OCR,
# load an image, apply a custom dictionary,
# and extract text from a PNG file.
# -------------------------------------------------

from aocr import OcrEngine
import aocr

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Add domain‑specific words
    ocr_engine.config.custom_dictionary = [
        "aspocorp",
        "ocrengine",
        "licensekey"
    ]

    # 3️⃣ Load the image you want to process
    #    (Make sure the path points to a real file)
    image_path = "YOUR_DIRECTORY/technical_doc.png"
    ocr_engine.image = aocr.Image.load(image_path)

    # 4️⃣ Run the OCR engine
    ocr_result = ocr_engine.process()

    # 5️⃣ Print the extracted text
    print("=== Extracted Text ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

Run it from the terminal:

```bash
python run_ocr.py
```

You should see the extracted text printed to the console, exactly as shown in the earlier example.

---

## Frequently Asked Questions (FAQ)

| Question | Answer |
|----------|--------|
| **Can I extract text from a scanned PDF?** | Yes. Convert each page to PNG (or TIFF) first, then feed the images to the same script. |
| **What if my image is a JPEG instead of PNG?** | The `Image.load` method supports JPEG, BMP, TIFF, and PNG out of the box. Just change the file extension. |
| **How do I improve accuracy on low‑contrast scans?** | Pre‑process with `Pillow` – increase contrast, apply binarization, or use `opencv` to deskew. |
| **Is there a way to get confidence scores for each word?** | `ocr_result` includes `words` – each word has a `confidence` attribute you can iterate over. |
| **Can I run this on a headless server?** | Absolutely. `aocr` has no GUI dependencies, making it perfect for CI pipelines. |

---

## Next Steps & Related Topics

Now that you know **how to create OCR** and **extract text from image** files, consider exploring:

* **Pre‑processing techniques** – `load image for OCR` is just the first step; use `opencv` to denoise or sharpen.  
* **Batch processing** – loop over a directory of PNGs to generate a searchable archive.  
* **Multi‑language support** – add language packs to the engine if you need to read French or German documents.  
* **Integrating with Elasticsearch** – index the extracted text for full‑text search across scanned assets.  

Each of these extensions builds on the core pattern we just covered, so you’ll find the transition painless.

---

## Wrap‑Up

In a handful of minutes we’ve answered **how to create OCR** that reliably **extracts text from image** files, especially PNGs, and we’ve shown you how to **load image for OCR**, apply a **custom dictionary**, and **run OCR on PNG** without any external services.  

Give the script a spin, tweak the dictionary to match your own jargon, and you’ll have a solid foundation for any document‑digitization project.  

If you ran into any hiccups, drop a comment below—happy to help. And don’t forget to share your success stories; the community learns best from real‑world examples.  

**Ready to automate your paperwork?** Grab the code, adapt it, and start turning pixels into searchable text today!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}