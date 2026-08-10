---
category: general
date: 2026-01-12
description: How to perform OCR and convert image to text quickly. Learn to recognize
  special characters, extract text from image, and load image for OCR with a complete
  Python example.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: en
og_description: How to perform OCR in Python, convert image to text, and recognize
  special characters. Follow this hands‑on guide for extracting text from images.
og_title: How to Perform OCR in Python – Complete Tutorial
tags:
- OCR
- Python
- Image Processing
title: How to Perform OCR in Python – Step‑by‑Step Guide
url: /python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in Python – Step‑by‑Step Guide

Ever needed to **perform OCR** on a screenshot that contains both Latin and Cyrillic characters? You're not alone. In many projects—whether it's digitizing receipts, indexing multilingual documents, or building a searchable archive—**how to perform OCR** quickly becomes a top‑of‑mind question.  

In this tutorial we’ll walk through a complete, runnable example that shows you how to **convert image to text**, **recognize special characters**, and **extract text from image** using a simple Python library. By the end you’ll have a ready‑to‑run script that loads an image for OCR, handles multilingual content, and prints the result.

## What You’ll Need

Before we dive in, make sure you have the following prerequisites:

- Python 3.8+ installed on your machine.  
- The `ocr` package (or any compatible OCR library) installed via `pip install ocr`.  
- An image file (`multilingual.png`) that contains both Latin and Cyrillic glyphs.  
- A basic text editor or IDE—VS Code, PyCharm, or even a simple Notepad will do.  

If you don’t have the `ocr` package, you can swap it for `pytesseract` with a few minor changes; the core concepts stay the same.

## Step 1: Install and Import the OCR Library

First, let’s get the OCR engine ready. We’ll import the library, create an engine instance, and configure it for multilingual support.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Why this matters:**  
Creating the engine is the foundation—without it you can’t **load image for OCR** later. Enabling language packs ensures the engine can correctly identify characters like “Ŀ”, “Ҕ”, and “Ǣ”. If you skip this step, you’ll end up with garbled output for non‑Latin scripts.

## Step 2: Load the Image Containing Multilingual Text

Now we point the engine at the file we want to process. The path can be absolute or relative; just make sure it points to a readable image.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![how to perform OCR example](/images/ocr-example.png "how to perform OCR on a multilingual image")

**Why this matters:**  
The `load_image` call reads the pixel data into memory, preparing it for the OCR algorithm. If the image is large, the engine may automatically downscale it; you can fine‑tune that later with `engine.set_max_resolution(3000)` for high‑resolution scans.

## Step 3: Run the Recognition Process

With the engine primed and the image loaded, we can finally extract the textual content.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Why this matters:**  
`recognize()` runs the heavy‑lifting neural network behind the scenes. It returns an object that holds the raw text, confidence scores, and even bounding boxes if you need them for visual debugging.

## Step 4: Output the Recognized Text

Let’s see what the engine found. We’ll print the text to the console, but you could also write it to a file or a database.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Expected Output

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

If you see something similar, congratulations—you’ve successfully **convert image to text** and **recognize special characters**.

## Handling Common Pitfalls

Even with a straightforward script, you might run into a few hiccups. Below are some practical tips from my own experience.

### 1. Missing Language Packs

If you get question marks (`?`) instead of Cyrillic letters, double‑check that the language packs are installed. For many OCR engines you need to download the corresponding `.traineddata` files and place them in the engine’s `tessdata` folder.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Low Image Quality

Blurry or low‑contrast images produce low confidence scores. Pre‑process the image with OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Large Files and Memory Usage

Processing a 10 MB photo can spike memory. Use `engine.set_max_image_size(2000)` to cap the resolution, or split the image into tiles and OCR each tile separately.

### 4. Capturing Bounding Boxes

If you need to highlight where each word appears (useful for UI overlays), access `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Full Script – One‑Click Execution

Putting everything together, here’s a single file you can run as `python ocr_demo.py`. It includes error handling, optional preprocessing, and comments for clarity.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Run it with:

```bash
python ocr_demo.py path/to/multilingual.png
```

You should see the same output shown earlier, confirming that you’ve **extract text from image** successfully.

## Conclusion

We’ve covered **how to perform OCR** in Python from start to finish: installing the library, loading an image, recognizing multilingual content, and handling the most common edge cases. By following this guide you can now **convert image to text**, **recognize special characters**, and **extract text from image** in your own projects—no more manual transcription.

What’s next? Try experimenting with:

- Adding more language packs (e.g., `spa` for Spanish).  
- Exporting results to JSON for downstream processing.  
- Integrating the OCR step into a Flask API so other services can call it.  

If you run into any quirks, the community around most OCR libraries is active—search for “ocr library language pack installation” or drop a comment below. Happy coding, and enjoy turning pictures into searchable text!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}