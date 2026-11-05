---
category: general
date: 2026-03-26
description: Create ROI polygon to run OCR on selected area. Learn how to define multiple
  regions, register them, and extract text with a Python OCR engine.
draft: false
keywords:
- create roi polygon
- ocr on selected area
- region of interest
- ocr engine
- python ocr example
language: en
og_description: Create ROI polygon and run OCR on selected area with a Python engine.
  Full code, explanations, and tips included.
og_title: Create ROI Polygon – Quick OCR on Selected Area
tags:
- OCR
- Python
- Image Processing
title: Create ROI Polygon – Step‑by‑Step Guide for OCR on Selected Area
url: /python-java/general/create-roi-polygon-step-by-step-guide-for-ocr-on-selected-ar/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create ROI Polygon – Full Tutorial for OCR on Selected Area

Ever needed to **create ROI polygon** so you can run OCR on just the part of an image that matters? Maybe you’re scanning receipts and only the totals matter, or you have a form where only the signature field needs reading. In those cases, **ocr on selected area** saves time and boosts accuracy.  

In this guide we’ll walk through everything you need: from defining two polygons, registering them with an OCR engine, to pulling the recognized text out in one clean call. By the end you’ll have a ready‑to‑run script and a solid grasp of why focusing on regions of interest matters.

## What You’ll Learn

- How to **create ROI polygon** objects using a typical OCR library.
- The difference between defining a single region versus multiple ones.
- How to register those regions with the engine so that `ocr on selected area` is performed.
- Expected output and how to troubleshoot common pitfalls (e.g., overlapping ROIs, empty results).

### Prerequisites

- Python 3.8+ installed.
- An OCR library that exposes `Polygon`, `Point`, and `add_region_of_interest` methods (the example uses a fictional `ocr` module; replace with your actual SDK, such as Tesseract‑Python wrappers or EasyOCR).
- A sample image file (`sample.png`) that contains text within the coordinates shown below.

> **Pro tip:** If you’re using a real library, make sure the image is loaded in the same coordinate space (origin at top‑left, X increasing right, Y increasing down).  

---  

## Step 1: Import the OCR Module and Load Your Image  

First, bring the OCR package into scope and read the image you want to process.  

```python
import ocr  # Replace with your actual OCR library import
from pathlib import Path

# Load the image – adjust the path as needed
image_path = Path("sample.png")
ocr_engine = ocr.Engine(image_path)
```

*Why this matters:* The engine needs the image data before you can attach any **ROI polygon**. Some libraries also let you pass the image later, but initializing early keeps the workflow tidy.

## Step 2: Define the First ROI Polygon  

Now we create the first region of interest. Think of it as drawing a rectangle around a table header.  

```python
# Step 2: Define the first ROI polygon
first_roi = ocr.Polygon([
    ocr.Point(50, 20),   # top‑left
    ocr.Point(200, 20),  # top‑right
    ocr.Point(200, 80),  # bottom‑right
    ocr.Point(50, 80)    # bottom‑left
])
```

*Explanation:*  
- `ocr.Point(x, y)` uses pixel coordinates.  
- The list of points is ordered clockwise, which most engines expect.  
- You can add as many points as you like to create irregular shapes; a rectangle is just a special case.

## Step 3: Define Additional ROI Polygons (Optional)  

You don’t have to stop at one. Here’s a second polygon that captures a signature field lower on the page.  

```python
# Step 3: Define the second ROI polygon
second_roi = ocr.Polygon([
    ocr.Point(300, 150),
    ocr.Point(480, 150),
    ocr.Point(480, 210),
    ocr.Point(300, 210)
])
```

*Why add more?* Running **ocr on selected area** for multiple zones lets you extract disparate pieces of data in a single pass, which is far faster than cropping and processing each slice separately.

## Step 4: Register the ROIs with the OCR Engine  

With the polygons ready, tell the engine which areas to inspect.  

```python
# Step 4: Register the ROIs
ocr_engine.add_region_of_interest(first_roi)
ocr_engine.add_region_of_interest(second_roi)
```

*Important note:* Some SDKs require you to call a `clear_regions()` method before adding new ones if you reuse the engine for another image.

## Step 5: Run OCR and Retrieve the Text  

Finally, fire off the recognition. The engine will only look inside the polygons we just added.  

```python
# Step 5: Perform OCR on the defined regions
recognized_text = ocr_engine.recognize().get_text()
print("=== Recognized Text ===")
print(recognized_text)
```

**Expected output** (assuming `sample.png` contains the words “Invoice Total: $123.45” in the first ROI and “Signature: John Doe” in the second):

```
=== Recognized Text ===
Invoice Total: $123.45
Signature: John Doe
```

If the output is empty, double‑check that the coordinates actually intersect text and that the image resolution matches the coordinate system.

## Edge Cases & Common Pitfalls  

| Situation                               | What to Watch For                               | Fix / Work‑around                              |
|----------------------------------------|--------------------------------------------------|-----------------------------------------------|
| **Overlapping ROIs**                    | Text may be returned twice.                     | Keep polygons disjoint or deduplicate output. |
| **ROI outside image bounds**           | Engine may raise an error or return nothing.    | Clamp coordinates to `0 ≤ x < width`, `0 ≤ y < height`. |
| **Very small ROI**                     | OCR accuracy drops because of insufficient pixels. | Expand the polygon a few pixels or upscale the image first. |
| **Non‑rectangular shape**               | Some engines only support convex polygons.      | Break complex shapes into multiple convex ROIs. |
| **Changing image size**                | Hard‑coded coordinates become invalid.           | Compute ROI coordinates relative to image dimensions (e.g., percentages). |

## Full Working Example  

Below is the complete script you can copy‑paste and run (replace `ocr` with your actual library).  

```python
import ocr                      # <- your OCR library
from pathlib import Path

# -------------------------------------------------
# Configuration
# -------------------------------------------------
IMAGE_PATH = Path("sample.png")

# -------------------------------------------------
# Initialize OCR engine with the image
# -------------------------------------------------
engine = ocr.Engine(IMAGE_PATH)

# -------------------------------------------------
# Define ROI polygons
# -------------------------------------------------
first_roi = ocr.Polygon([
    ocr.Point(50, 20), ocr.Point(200, 20),
    ocr.Point(200, 80), ocr.Point(50, 80)
])

second_roi = ocr.Polygon([
    ocr.Point(300, 150), ocr.Point(480, 150),
    ocr.Point(480, 210), ocr.Point(300, 210)
])

# -------------------------------------------------
# Register ROIs
# -------------------------------------------------
engine.add_region_of_interest(first_roi)
engine.add_region_of_interest(second_roi)

# -------------------------------------------------
# Run OCR on the selected areas
# -------------------------------------------------
result = engine.recognize().get_text()

print("=== Recognized Text ===")
print(result)
```

Run it with `python ocr_roi_example.py` and you should see the extracted strings from the two defined zones.

## Next Steps  

- **Dynamic ROI generation:** Instead of hard‑coding coordinates, use image processing (e.g., OpenCV contour detection) to automatically locate tables or fields.  
- **Post‑processing:** Strip whitespace, apply regexes, or convert numbers to proper data types.  
- **Batch processing:** Loop over a folder of images, re‑using the same ROI definitions if the layout is consistent.  

If you’re curious about **ocr on selected area** for more complex documents—think multi‑page PDFs or scanned forms—look into libraries that support page‑wise ROI registration.  

---  

### Visual Overview  

![Diagram showing two ROI polygons on a sample image](roi_diagram.png){alt="create roi polygon example showing two selected areas"}

The diagram illustrates how the two rectangles (blue and green) map onto the underlying image, highlighting exactly what the OCR engine will read.

---  

## Conclusion  

We’ve just **created ROI polygon** objects, registered them with an OCR engine, and performed `ocr on selected area` in a clean, reproducible script. By limiting the engine to the zones you care about, you cut processing time, improve accuracy, and make downstream data handling far simpler.  

Give it a spin with your own images—tweak the coordinates, add more polygons, or hook the output into a database. The sky’s the limit once you master region‑based OCR.  

Got questions or want to share a cool use case? Drop a comment below, and happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}