---
category: general
date: 2026-04-26
description: how to extract ocr from images using Python – a python ocr example that
  shows how to load image for ocr and extract text from receipt.
draft: false
keywords:
- how to extract ocr
- python ocr example
- extract text from receipt
- load image for ocr
- how to use OCR
language: en
og_description: how to extract ocr from images using Python. Learn a python ocr example,
  load image for ocr, and extract text from receipt in minutes.
og_title: how to extract ocr in Python – Complete Guide
tags:
- OCR
- Python
- Image Processing
title: how to extract ocr in Python – Step‑by‑Step Tutorial
url: /python-java/general/how-to-extract-ocr-in-python-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to extract ocr in Python – Complete Guide

Ever wondered **how to extract ocr** from a blurry receipt or a scanned invoice? You're not the only one—developers constantly hit the wall when they need clean, machine‑readable text from images. The good news? With just a few lines of Python you can turn a picture of a receipt into high‑confidence, searchable text.

In this tutorial we’ll walk through a **python ocr example** that demonstrates **how to load image for ocr**, run the engine, and keep only the characters that meet an 85 % confidence threshold. By the end you’ll be able to **extract text from receipt** images without hunting through documentation or guessing API parameters.

## What You’ll Need

- Python 3.9 or newer (the syntax we use works on 3.8+)
- The `aocr` package (or any OCR library that provides an `OcrEngine` class). Install it with:

```bash
pip install aocr
```

- A sample receipt image (`receipt.png`) placed in a folder you can reference.
- A text editor or IDE—VS Code, PyCharm, or even a simple notebook will do.

That’s it. No heavyweight frameworks, no external services, just pure Python.

![High‑confidence OCR result – how to extract ocr from a receipt](/images/ocr-high-confidence.png)

*Image alt text: how to extract ocr from a receipt using Python OCR*

## Step 1 – Create the OCR Engine Instance (how to extract ocr)

The first thing we do is spin up an OCR engine. Think of it as the brain that will read the pixels for us.

```python
# Step 1: Initialize the OCR engine
from aocr import OcrEngine

ocr_engine = OcrEngine()
```

**Why?** Instantiating `OcrEngine` gives you a fresh configuration object. You can later tweak language models, DPI settings, or preprocessing steps—all without touching the core processing loop.

## Step 2 – Load the Image for OCR

Next we point the engine at the image we want to analyze. This is where the **load image for ocr** keyword comes into play.

```python
# Step 2: Load the receipt image
image_path = "YOUR_DIRECTORY/receipt.png"
ocr_engine.image = OcrEngine.Image.load(image_path)
```

> **Pro tip:** If your image lives in a different directory, use `os.path.join` to build a platform‑independent path.

**Why load the image this way?** The `Image.load` helper reads the file into a format the engine understands, handling common formats (PNG, JPEG, TIFF) automatically. Skipping this step or feeding raw bytes would raise a `ValueError`.

## Step 3 – Run the OCR Process

Now we actually run the OCR. The `process` method returns a rich result object containing recognized symbols, confidence scores, and bounding boxes.

```python
# Step 3: Execute OCR and capture the result
ocr_result = ocr_engine.process()
```

**What does `ocr_result` contain?** In most libraries it includes:

- `text`: the raw concatenated string.
- `symbol_confidences`: a list of `(char, confidence)` tuples.
- `boxes`: coordinates for each character (useful for visual debugging).

Having access to per‑character confidence is essential for the next step.

## Step 4 – Keep Only High‑Confidence Symbols (≥ 85 %)

A receipt often has smudges, faint print, or background noise. By filtering out low‑confidence symbols we dramatically improve downstream parsing.

```python
# Step 4: Filter out low‑confidence characters
high_confidence_text = ''.join(
    char for char, confidence in ocr_result.symbol_confidences
    if confidence >= 0.85
)
```

**Why 85 %?** Empirically, a threshold around 0.85 balances recall and precision for most printed receipts. If you notice missing numbers, lower the threshold; if you get gibberish, raise it.

## Step 5 – Output the High‑Confidence Extracted Text

Finally, we print (or store) the sanitized string. This is the core of our **extract text from receipt** workflow.

```python
# Step 5: Show the cleaned result
print("High‑confidence text:", high_confidence_text)
```

Typical output looks like:

```
High‑confidence text: Store XYZ
Date: 2024‑04‑22
Total: $23.45
```

You can now feed this string into a CSV writer, a database, or any downstream analytics pipeline.

## Full, Ready‑to‑Run Script

Below is the complete code snippet that you can copy‑paste into `ocr_receipt.py` and run immediately.

```python
# ocr_receipt.py
# A complete python ocr example that extracts high‑confidence text from a receipt.

from aocr import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the image you want to analyze
    image_path = "YOUR_DIRECTORY/receipt.png"
    ocr_engine.image = OcrEngine.Image.load(image_path)

    # 3️⃣ Run the OCR process
    ocr_result = ocr_engine.process()

    # 4️⃣ Keep only symbols with confidence ≥ 85%
    high_confidence_text = ''.join(
        char for char, confidence in ocr_result.symbol_confidences
        if confidence >= 0.85
    )

    # 5️⃣ Output the result
    print("High‑confidence text:", high_confidence_text)

if __name__ == "__main__":
    main()
```

Save the file, ensure `receipt.png` exists, and execute:

```bash
python ocr_receipt.py
```

You should see the cleaned receipt text printed to the console.

## Edge Cases & What‑If Scenarios

| Situation | Suggested Fix |
|-----------|----------------|
| **Very low confidence across the board** | Pre‑process the image: increase contrast, convert to grayscale, or apply a denoising filter (`cv2.GaussianBlur`). |
| **Non‑Latin characters** | Pass a language model to `OcrEngine` (e.g., `ocr_engine.language = "spa"` for Spanish). |
| **Multiple receipts in one image** | Run OCR on the whole image, then split the result using regular expressions that detect `\n\n+` (double line breaks). |
| **Need the raw OCR text as well** | Keep `ocr_result.text` alongside the filtered version for debugging. |

These variations ensure your **how to use OCR** knowledge scales beyond the simplest case.

## Common Pitfalls (And How to Avoid Them)

- **Forgetting to install the library** – `pip install aocr` must succeed before you import.
- **Using the wrong path separator** on Windows (`\` vs `/`). Use `os.path.join`.
- **Hard‑coding the confidence threshold** without testing – always run a quick visual check on a few receipts first.
- **Ignoring Unicode normalisation** – some receipts contain special dash characters; run `unicodedata.normalize('NFKC', text)` if you plan to store the output.

## Next Steps – Going Beyond the Basics

Now that you know **how to extract ocr** data from a single receipt, you might want to:

1. **Batch process a folder of receipts** – loop over all PNG/JPG files and write each result to a CSV.
2. **Integrate with a database** – store `high_confidence_text` in SQLite for quick look‑ups.
3. **Apply natural‑language parsing** – use regex or `dateutil` to pull dates, totals, and tax amounts.
4. **Experiment with alternative libraries** – `pytesseract`, `easyocr`, or cloud services (Google Vision, Azure OCR) if you need multilingual support or higher accuracy.

Each of these topics naturally incorporates our secondary keywords: *python ocr example*, *extract text from receipt*, *load image for ocr*, and *how to use OCR*.

## Conclusion

We’ve just walked through a complete **python ocr example** that shows **how to extract ocr** text from a receipt image, filter out low‑confidence symbols, and output clean results. The steps are simple, the code is self‑contained, and the approach is flexible enough to adapt to larger projects.

Give it a try with your own receipts, tweak the confidence threshold, and then scale up to batch processing. If you run into quirks—like a faint logo or an unusual font—remember the edge‑case tips above. Happy coding, and may your OCR pipelines be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}