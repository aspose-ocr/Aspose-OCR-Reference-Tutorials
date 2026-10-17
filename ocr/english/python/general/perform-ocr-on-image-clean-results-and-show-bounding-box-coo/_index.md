---
category: general
date: 2026-03-28
description: Perform OCR on image and get clean text with bounding box coordinates.
  Learn how to extract OCR, clean OCR, and display results step‑by‑step.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: en
og_description: Perform OCR on image, clean the output, and display bounding box coordinates
  in a concise tutorial.
og_title: Perform OCR on Image – Clean Results and Bounding Boxes
tags:
- OCR
- Computer Vision
- Python
title: Perform OCR on Image – Clean Results and Show Bounding Box Coordinates
url: /python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Perform OCR on Image – Clean Results and Show Bounding Box Coordinates

Ever needed to **perform OCR on image** files but kept getting messy text and unsure where each word lives on the picture? You're not alone. In many projects—invoice digitization, receipt scanning, or simple text extraction—getting raw OCR output is just the first hurdle. The good news? You can clean that output and instantly see each region’s bounding box coordinates without writing a ton of boilerplate code.

In this guide we’ll walk through **how to extract OCR**, run a **how to clean OCR** post‑processor, and finally **display bounding box coordinates** for every cleaned region. By the end you’ll have a single, runnable script that turns a blurry photo into tidy, structured text ready for downstream processing.

## What You’ll Need

- Python 3.9+ (the syntax below works on 3.8 and newer)
- An OCR engine that supports `recognize(..., return_structured=True)` – for example, a fictional `engine` library used in the snippet. Replace it with Tesseract, EasyOCR, or any SDK that returns region data.
- Basic familiarity with Python functions and loops
- An image file you want to scan (PNG, JPG, etc.)

> **Pro tip:** If you’re using Tesseract, the `pytesseract.image_to_data` function already gives you bounding boxes. You can wrap its result in a small adapter that mimics the `engine.recognize` API shown below.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: diagram showing how to perform OCR on image and visualize bounding box coordinates*

## Step 1 – Perform OCR on Image and Get Structured Regions

The first thing is to ask the OCR engine to return not just plain text but a structured list of text regions. This list contains the raw string and the rectangle that encloses it.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Why this matters:**  
When you only ask for plain text you lose spatial context. Structured data lets you later **display bounding box coordinates**, align text with tables, or feed precise locations to a downstream model.

## Step 2 – How to Clean OCR Output with a Post‑Processor

OCR engines are great at spotting characters, but they often leave stray spaces, line‑break artifacts, or mis‑recognized symbols. A post‑processor normalizes the text, fixes common OCR errors, and trims whitespace.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

If you’re building your own cleaner, consider:

- Removing non‑ASCII characters (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Collapsing multiple spaces into a single space
- Applying a spell‑checker like `pyspellchecker` for obvious typos

**Why you should care:**  
A tidy string makes searching, indexing, and downstream NLP pipelines far more reliable. In other words, **how to clean OCR** is often the difference between a usable dataset and a headache.

## Step 3 – Display Bounding Box Coordinates for Each Cleaned Region

Now that the text is tidy, we iterate over each region, printing its rectangle and the cleaned string. This is the part where we finally **display bounding box coordinates**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Sample output**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

You can now feed those coordinates into a drawing library (e.g., OpenCV) to overlay boxes on the original image, or store them in a database for later queries.

## Full, Ready‑to‑Run Script

Below is the complete program that ties together all three steps. Swap out the placeholder `engine` calls with your actual OCR SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### How to Run

```bash
python perform_ocr.py sample_invoice.jpg
```

You should see a list of bounding boxes paired with cleaned text, exactly like the sample output above.

## Frequently Asked Questions & Edge Cases

| Question | Answer |
|----------|--------|
| **What if the OCR engine doesn’t support `return_structured`?** | Write a thin wrapper that converts the engine’s raw output (usually a list of words with coordinates) into objects with `text` and `bounding_box` attributes. |
| **Can I get confidence scores?** | Many SDKs expose a confidence metric per region. Append it to the print statement: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **How to handle rotated text?** | Pre‑process the image with OpenCV’s `cv2.minAreaRect` to deskew before calling `recognize`. |
| **What if I need the output in JSON?** | Serialize `processed_result.regions` with `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Is there a way to visualize the boxes?** | Use OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` inside the loop, then `cv2.imwrite("annotated.jpg", img)`. |

## Wrapping Up

You’ve just learned **how to perform OCR on image**, clean the raw output, and **display bounding box coordinates** for every region. The three‑step flow—recognize → post‑process → iterate—is a reusable pattern you can drop into any Python project that needs reliable text extraction.

### What’s Next?

- **Explore different OCR back‑ends** (Tesseract, EasyOCR, Google Vision) and compare accuracy.
- **Integrate with a database** to store region data for searchable archives.
- **Add language detection** to route each region through the appropriate spell‑checker.
- **Overlay boxes on the original image** for visual verification (see the OpenCV snippet above).

If you run into quirks, remember that the biggest win comes from a solid post‑processing step; a clean string is far easier to work with than a raw dump of characters.

Happy coding, and may your OCR pipelines be ever tidy!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}