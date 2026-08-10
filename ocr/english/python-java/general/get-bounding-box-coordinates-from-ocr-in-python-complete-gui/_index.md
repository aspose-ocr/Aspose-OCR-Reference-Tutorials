---
category: general
date: 2026-06-22
description: Get bounding box coordinates from images using Python. Learn how to extract
  text from image python with Aspose OCR and JSON parsing in minutes.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: en
og_description: Get bounding box coordinates from images using Python. This guide
  shows how to extract text from image python with Aspose OCR and parse layout data.
og_title: Get Bounding Box Coordinates from OCR in Python – Full Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Get Bounding Box Coordinates from OCR in Python – Complete Guide
url: /python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Get Bounding Box Coordinates from OCR in Python – Complete Guide

Ever needed to **get bounding box coordinates** for every word in a scanned invoice, but weren’t sure where to start? You’re not the only one. In many automation projects, you have to locate text on an image to highlight, redact, or feed into downstream analytics. The good news? With a few lines of Python and Aspose.OCR you can pull both the text **and** its exact position in a single pass.

In this tutorial we’ll walk through a hands‑on example that shows you how to **extract text from image python**‑style, then dive into the JSON layout data to pull out those bounding boxes. No fluff, just a working script, explanations of why each step matters, and tips to avoid common pitfalls.

---

## What You’ll Build

By the end of this guide you’ll have a ready‑to‑run Python script that:

1. Loads an image (e.g., an invoice PNG) into Aspose OCR.
2. Configures the engine to emit JSON layout information.
3. Parses the JSON into a Python dictionary.
4. Iterates over every recognized word, printing its text **and** its bounding box coordinates.

You’ll also see how to adapt the code for multi‑page PDFs, different image formats, and custom coordinate systems.

### Prerequisites

- Python 3.8+ installed on your machine.  
- An active Aspose.OCR for Python license or a free trial (the library works without a license but adds a watermark).  
- `pip install aspose-ocr` (the package name on PyPI).  
- A sample image called `invoice.png` placed in a folder you can reference.

That’s it—no heavyweight frameworks, no external services. Let’s dive in.

---

## Step 1: Install and Import the Required Libraries

First, make sure the Aspose OCR package and the built‑in `json` module are available. The `json` module ships with Python, so we only need to install Aspose.

```bash
pip install aspose-ocr
```

Now import them in your script:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Why this matters:** Importing `aspose.ocr` gives you access to the high‑performance OCR engine, while `json` lets you turn the raw layout string into a native Python dictionary for easy traversal.

---

## Step 2: Create the OCR Engine and Load Your Image

The engine is the heart of the process. You instantiate it, then point it at the image you want to scan.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Pro tip:** Replace `"YOUR_DIRECTORY/invoice.png"` with an absolute or relative path that points to your actual file. If the file isn’t found, Aspose will raise a `FileNotFoundError`, so double‑check the spelling.

---

## Step 3: Configure the Engine to Output JSON Layout Data

Aspose OCR can return plain text, OCR‑only JSON, or a full layout JSON that includes coordinates for words, lines, and even individual characters. For **get bounding box coordinates**, we need the layout JSON.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Why JSON?** JSON is language‑agnostic, human‑readable, and maps cleanly to Python dictionaries. The layout JSON contains a `"words"` array where each entry holds the text and a `boundingBox` array of eight numbers (the four corner points).

---

## Step 4: Run Recognition and Grab the Raw JSON String

Now we actually run the OCR. The `recognize()` method returns an `OcrResult` object, from which we can extract the JSON string.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

If you print `layout_json` you’ll see something like:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Edge case:** Some images may produce empty `"words"` arrays if the OCR engine cannot detect any text. In that case, verify image quality (contrast, resolution) before proceeding.

---

## Step 5: Parse the JSON into a Python Dictionary

Working with native Python structures is far easier than string fiddling. Use the `json.loads()` function to convert the string.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Now `layout_data["words"]` is a list of dictionaries, each representing a word and its bounding box.

---

## Step 6: Iterate Over Words and **Get Bounding Box Coordinates**

Here’s the core of our tutorial: looping through each word, extracting the text, and printing the coordinates. This is the exact place where we **get bounding box coordinates**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Sample output** (your numbers will differ based on the image):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Why the eight‑point format?** The four corners (top‑left, top‑right, bottom‑right, bottom‑left) allow you to draw a polygon around the word, even if the text is skewed. If you only need a simple rectangle, you can compute `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, and `height = max(y…) - y_min`.

---

## Optional Enhancements

### 1. Convert Bounding Boxes to Simple Rectangles

If your downstream tool expects `(x, y, width, height)` instead of eight points, add a helper:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Handle Multi‑Page PDFs

Aspose OCR can accept PDF streams. Replace the image loading line with:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Iterate `set_page_number` for each page, collecting coordinates per page.

### 3. Visualize Bounding Boxes

If you want to see the boxes drawn on the original image, use Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Now you’ll see red outlines around every recognized word—perfect for debugging or UI overlays.

---

## Common Questions & Gotchas

- **What if the JSON is huge?** For large documents, consider streaming the JSON or processing page‑by‑page to keep memory usage low.
- **Why are some words missing?** Low contrast or handwritten text often trips OCR engines. Pre‑process the image (increase contrast, binarize) before feeding it to Aspose.
- **Can I get character‑level coordinates?** Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)` to receive a `"characters"` array with its own `boundingBox`.
- **Is the coordinate system zero‑based?** Absolutely. (0, 0) is the top‑left corner of the image.

---

## Full Script – Ready to Copy & Run

Below is the complete, runnable example that combines every step. Save it as `extract_bboxes.py` and execute `python extract_bboxes.py`.

```python
import aspose.ocr as ocr
import json

# -------------------------
# 1️⃣ Initialize OCR engine
# -------------------------
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))

# -------------------------------------------------
# 2️⃣ Ask for JSON layout output (contains bounding boxes)
# -------------------------------------------------
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)

# -------------------------
# 3️⃣ Run recognition
# -------------------------
result = engine.recognize()
layout_json = result.get_json()

# -------------------------
# 4️⃣ Parse JSON
# -------------------------
layout_data = json.loads(layout_json)

# -------------------------
# 5️⃣ Helper to turn 8‑point box into rectangle (optional)
# -------------------------
def box_to_rect(box):
    xs = box[0::2]
    ys = box[1::2]
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}