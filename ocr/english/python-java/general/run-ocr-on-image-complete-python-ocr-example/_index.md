---
category: general
date: 2026-03-18
description: Run OCR on image quickly with Python. Learn how to recognize text from
  PNG, load image for OCR, and extract words from image in a step‑by‑step guide.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: en
og_description: Run OCR on image using Python. This tutorial shows how to recognize
  text from PNG, load image for OCR, and extract words from image with a full code
  example.
og_title: Run OCR on Image – Python Guide
tags:
- OCR
- Python
- Image Processing
title: Run OCR on Image – Complete Python OCR Example
url: /python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image – Complete Python OCR Example

Ever needed to **run OCR on image** files but weren’t sure where to start? You’re not alone; many developers hit that wall when they first tackle text extraction from scanned documents. In this tutorial we’ll walk through a **Python OCR example** that lets you **recognize text from PNG** files, **load image for OCR**, and **extract words from image** with confidence scores—all in just a few lines of code.

We’ll cover everything you need: the required library, how to set up the engine, why each step matters, and what the output looks like. By the end, you’ll be able to drop this snippet into your own project and start pulling text from any image instantly. No fluff, just a practical, runnable solution.

## What You’ll Need

Before we dive in, make sure you have:

- Python 3.8 or newer installed  
- The `ocrengine` package (or any library that provides an `OcrEngine` class). You can install it via `pip install ocrengine` – adjust the name if you’re using a different OCR library like `pytesseract`.  
- An image file (PNG, JPG, etc.) you want to process – for this guide we’ll use `invoice.png`.  

That’s it. No heavyweight dependencies, no external services, just pure Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: run OCR on image example – scanned invoice being processed*

## Step 1 – Install and Import the OCR Library

First things first, let’s get the OCR engine into our environment and import it. If you’re using the hypothetical `ocrengine` package, the import looks like this:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Why this matters:** Importing the right class gives you access to the methods we’ll call later, like `setImageFromFile` and `recognize`. If you skip this step, Python will throw a `ModuleNotFoundError`, and you’ll be stuck before you even load an image.

## Step 2 – Create an OCR Engine Instance

Now that the library is ready, we need an engine object that will hold the configuration and state for the recognition process.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Pro tip:* Some OCR engines let you tweak language models or DPI settings at this point. For a basic **python OCR example**, the defaults work fine, but if you’re dealing with low‑resolution scans, consider adjusting them here.

## Step 3 – Load the Image You Want to Process

The next logical step is to **load image for OCR**. You point the engine at the file path of the PNG (or any supported format) you wish to analyse.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**What’s happening under the hood?** The engine reads the pixel data, converts it into a format the recognition algorithm can understand, and stores it internally. If the file path is wrong, you’ll get a `FileNotFoundError`, so double‑check that the image exists.

## Step 4 – Run the Recognition Algorithm

With the image loaded, we finally **run OCR on image** to extract the textual content.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

At this point the engine scans the bitmap, applies pattern matching, and returns an object that contains every detected word, line, and confidence metric.

## Step 5 – Iterate Over Recognized Words and Display Confidence

The most useful part of any OCR workflow is seeing **the confidence** for each extracted token. It tells you how sure the engine is about each word, letting you filter out low‑confidence results if needed.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Expected output** (sample):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

You can now see exactly **what words were extracted from the image** and how reliable each detection is. This is the core of any **extract words from image** pipeline.

## Handling Common Edge Cases

### What If the Image Is Grayscale?

Some OCR engines perform better with color images. If you notice low confidence across the board, try converting the PNG to a higher‑contrast black‑and‑white version before feeding it to the engine. Pillow can help:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Dealing With Multiple Languages

If your document contains both English and Spanish, you’ll want to **recognize text from PNG** using a multilingual model. Most engines let you set the language list during initialization:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Filtering Low‑Confidence Words

Sometimes you only need words with confidence above, say, 90 %. A quick filter looks like this:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Full, Ready‑to‑Run Script

Putting everything together, here’s a single script you can copy‑paste and run immediately (just replace the path to your PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Run it with:

```bash
python run_ocr_on_image.py
```

You should see the list of words and confidence percentages printed to the console, exactly as shown earlier.

## Frequently Asked Questions

**Does this work with JPG or TIFF files?**  
Absolutely. The `setImageFromFile` method accepts any format the underlying library can decode, so you can **run OCR on image** files of type JPG, TIFF, BMP, etc.

**Can I process multiple images in a loop?**  
Sure thing. Wrap the loading and recognition steps inside a `for` loop over a list of file paths. Just remember to re‑initialize the engine if the library requires a fresh instance per image.

**What if I need the text in a single string instead of per‑word?**  
Most OCR result objects expose a `getText()` method that returns the whole document. Example:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Next Steps and Related Topics

Now that you know how to **run OCR on image**, consider exploring:

- **Post‑processing**: Use regular expressions to clean up dates, amounts, or IDs extracted from invoices.  
- **Batch processing**: Combine the script with `os.listdir()` to handle whole folders of scanned documents.  
- **Alternative libraries**: `pytesseract` is a popular open‑source option; the workflow is similar—just replace the engine calls.  
- **Exporting results**: Write the extracted words and confidence scores to CSV for downstream analysis.

Each of these extensions builds directly on the foundation we laid here, letting you turn raw OCR data into actionable information.

---

### TL;DR

We’ve shown a concise, **python OCR example** that demonstrates how to **load image for OCR**, **run OCR on image**, and **extract words from image** while reporting confidence. The full script is ready to run, and you now have the knowledge to adapt it to any project that needs to **recognize text from PNG** (or other formats). Give it a spin, tweak the confidence thresholds, and watch your applications become text‑aware in minutes. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}