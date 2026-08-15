---
category: general
date: 2026-03-26
description: How to run OCR on a PNG file and extract text from image with a custom
  dictionary for improved OCR accuracy. Learn to load image for OCR quickly.
draft: false
keywords:
- how to run OCR
- extract text from image
- recognize text from png
- improve OCR accuracy
- load image for OCR
language: en
og_description: How to run OCR on a PNG file and extract text from image with custom
  dictionary for improved OCR accuracy. Step‑by‑step guide.
og_title: How to Run OCR – Extract Text from Image in Python
tags:
- OCR
- Python
- Image Processing
title: How to Run OCR – Extract Text from Image in Python
url: /python-java/general/how-to-run-ocr-extract-text-from-image-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR – Extract Text from Image in Python

Ever wondered **how to run OCR** on a scanned invoice or a screenshot and get clean, searchable text? You're not alone. In many projects the bottleneck is simply loading the image for OCR and then coaxing the engine to understand domain‑specific words.  

In this tutorial we’ll walk through a complete, ready‑to‑run example that **extracts text from image** files, shows you how to **recognize text from PNG** assets, and even demonstrates tricks to **improve OCR accuracy** with custom dictionaries and special characters. By the end you’ll have a self‑contained script you can drop into any Python codebase.

## What You’ll Need

- Python 3.8+ (the code uses type hints but works on earlier 3.x versions)
- The `ocr` library that ships with the OCR engine you’re targeting (install via `pip install ocr‑engine` – replace with the actual package name)
- An image file (`input.png`) you want to process
- Optional: a plain‑text file (`invoice_terms.txt`) with domain‑specific words, one per line

No heavy external dependencies, no cloud API keys, just a local OCR engine.

---

## Step 1: Install and Import the OCR Library

First, make sure the OCR package is installed. If you’re using the hypothetical `ocr-engine` package, run:

```bash
pip install ocr-engine
```

Now import the classes you’ll need:

```python
# Step 1: Import the OCR SDK
import ocr
from ocr import Imaging
```

> **Pro tip:** If you’re on a virtual environment, activate it before installing to keep your global Python clean.

## Step 2: Create an OCR Engine Instance

Creating an engine object is the entry point for every OCR task. Think of it as turning on the scanner hardware in software.

```python
# Step 2: Initialise the OCR engine
ocr_engine = ocr.OcrEngine()
```

Why this matters: the engine holds configuration such as language packs, recognition modes, and any custom resources you’ll attach later. Without it, you can’t **load image for OCR** or run the recognition pipeline.

## Step 3: Load the Image You Want to Recognize

Here we actually **load image for OCR**. The `Imaging.Image.load()` method reads the file and converts it into the internal bitmap format the engine expects.

```python
# Step 3: Load the PNG image you want to process
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Imaging.Image.load(image_path))
```

If you have a JPEG or TIFF, the same method works—just change the extension. The engine automatically detects the format.

> **Edge case:** Very large images (over 5 MP) can cause memory spikes. Consider down‑scaling with Pillow before loading if you hit performance issues.

## Step 4: Provide a Custom Dictionary to Boost Accuracy

Most OCR engines ship with generic language models. For invoices, receipts, or legal documents you’ll often see missed words. Supplying a custom word list tells the engine “these terms are legit, treat them as correct”.

```python
# Step 4: Attach a custom dictionary (one word per line)
custom_dict_path = "YOUR_DIRECTORY/invoice_terms.txt"
ocr_engine.set_custom_dictionary(custom_dict_path)
```

Typical entries might be:

```
VAT
InvoiceNumber
Øre
ß
Ħ
```

Adding these improves the **improve OCR accuracy** metric dramatically—especially for non‑ASCII symbols.

## Step 5: Add Special Characters Not Covered by the Default Set

If your domain uses symbols like the Euro sign (€) or the Scandinavian Ø, you can explicitly add them:

```python
# Step 5: Register additional characters
ocr_engine.add_custom_characters("ØßĦ")
```

The engine will now treat those glyphs as valid during the recognition phase, reducing the chance of “garbage” output.

## Step 6: Run the OCR Process and Retrieve Text

Finally, invoke the recognizer and pull the plain‑text result. The `recognize()` call returns a rich object; we only need the raw string for most use‑cases.

```python
# Step 6: Execute OCR and print the result
result = ocr_engine.recognize()
print("=== Recognized Text ===")
print(result.get_text())
```

**Expected output** (truncated for brevity):

```
=== Recognized Text ===
Invoice #12345
Date: 2026-03-01
Total: €1,250.00
VAT: 25%
...
```

If the output looks garbled, double‑check that your custom dictionary and special characters are correctly loaded.

---

## Visual Overview

![how to run OCR diagram](ocr-workflow.png){alt="how to run OCR diagram"}

The diagram above illustrates the flow from loading an image to getting clean text, highlighting where you can inject custom dictionaries and character sets.

---

## Common Questions & Gotchas

### Does this work with multi‑page PDFs?

Yes—just convert each page to a PNG (using `pdf2image` or similar) and feed them sequentially to the same `ocr_engine` instance. The engine processes each image independently, so you’ll get a list of strings you can concatenate.

### What if the image is rotated?

Most modern OCR engines auto‑detect orientation, but you can force a rotation with:

```python
ocr_engine.set_image(Imaging.Image.load(image_path).rotate(90))
```

### How to handle languages other than English?

Swap the language model before loading the image:

```python
ocr_engine.set_language("de")  # German
```

Make sure the corresponding language pack is installed.

---

## Full Script – Ready to Copy & Paste

Below is the entire program, ready to run after you replace the placeholder paths.

```python
#!/usr/bin/env python3
"""
How to Run OCR – Complete example that extracts text from a PNG,
uses a custom dictionary, and adds special characters for better accuracy.
"""

# Install the OCR package first:
# pip install ocr-engine

import ocr
from ocr import Imaging

def main():
    # 1️⃣ Initialise the OCR engine
    ocr_engine = ocr.OcrEngine()

    # 2️⃣ Load the image you want to recognize
    image_path = "YOUR_DIRECTORY/input.png"      # <-- change this
    ocr_engine.set_image(Imaging.Image.load(image_path))

    # 3️⃣ Provide a custom dictionary (optional but recommended)
    dict_path = "YOUR_DIRECTORY/invoice_terms.txt"   # one word per line
    ocr_engine.set_custom_dictionary(dict_path)

    # 4️⃣ Add any special characters not covered by the default set
    ocr_engine.add_custom_characters("ØßĦ")   # e.g., currency symbols

    # 5️⃣ Run the OCR process
    result = ocr_engine.recognize()

    # 6️⃣ Output the recognized text
    print("=== Recognized Text ===")
    print(result.get_text())

if __name__ == "__main__":
    main()
```

Run it with:

```bash
python run_ocr.py
```

You should see the extracted text printed to the console. From there you can write it to a file, feed it into a database, or pass it to downstream NLP pipelines.

---

## Recap & Next Steps

We’ve covered **how to run OCR** on a PNG, how to **extract text from image**, and shown practical ways to **recognize text from PNG** while **improving OCR accuracy** with dictionaries and custom characters.  

Next, consider:

- **Batch processing:** Loop over a directory of images.
- **Post‑processing:** Use regex to pull out invoice numbers or dates.
- **Integration:** Hook the script into a Flask API for on‑demand OCR services.

If you’re curious about more advanced topics, check out tutorials on **load image for OCR** with OpenCV preprocessing, or dive into deep‑learning based OCR models like Tesseract 4+ with LSTM layers.

---

### Keep Experimenting!

Try swapping the `invoice_terms.txt` with a list of medical terminology, add Greek characters, or feed the engine a low‑resolution photo to see how far the accuracy can stretch. The more you tinker, the better you’ll understand the trade‑offs between preprocessing, custom vocabularies, and engine settings.

Happy coding, and may your OCR results be ever crisp!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}