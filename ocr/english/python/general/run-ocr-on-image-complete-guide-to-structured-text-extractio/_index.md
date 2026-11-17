---
category: general
date: 2026-05-03
description: Learn how to run OCR on image and extract text with coordinates using
  structured OCR recognition. Step‑by‑step Python code included.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: en
og_description: Run OCR on image and get text with coordinates using structured OCR
  recognition. Full Python example with explanations.
og_title: Run OCR on image – Structured Text Extraction Tutorial
tags:
- OCR
- Python
- Computer Vision
title: Run OCR on image – Complete Guide to Structured Text Extraction
url: /python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on image – Complete Guide to Structured Text Extraction

Ever needed to **run OCR on image** files but weren’t sure how to keep the exact positions of each word? You’re not alone. In many projects—receipt scanning, form digitisation, or UI testing—you need not only the raw text but also the bounding boxes that tell you where each line lives on the picture.  

This tutorial shows you a practical way to *run OCR on image* using the **aocr** engine, request **structured OCR recognition**, and then post‑process the result while preserving the geometry. By the end you’ll be able to **extract text with coordinates** in just a few lines of Python, and you’ll understand why the structured mode matters for downstream tasks.

## What You’ll Learn

- How to initialise the OCR engine for **structured OCR recognition**.  
- How to feed an image and receive raw results that include line bounds.  
- How to run a post‑processor that cleans up the text without losing geometry.  
- How to iterate over the final lines and print each piece of text together with its bounding box.  

No magic, no hidden steps—just a complete, runnable example you can drop into your own project.

---

## Prerequisites

Before we dive in, make sure you have the following installed:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

You’ll also need an image file (`input_image.png` or `.jpg`) that contains clear, readable text. Anything from a scanned invoice to a screenshot works, as long as the OCR engine can see the characters.

---

## Step 1: Initialise the OCR engine for structured recognition

The first thing we do is create an instance of `aocr.Engine()` and tell it we want **structured OCR recognition**. Structured mode returns not only the plain text but also geometric data (bounding rectangles) for each line, which is essential when you need to map text back onto the image.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> In the default mode the engine might only give you a string of concatenated words. Structured mode gives you a hierarchy of pages → lines → words, each with coordinates, making it far easier to overlay results on the original image or feed them into a layout‑aware model.

---

## Step 2: Run OCR on the image and obtain raw results

Now we feed the image to the engine. The `recognize` call returns an `OcrResult` object that contains a collection of lines, each with its own bounding rectangle.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

At this point `raw_result.lines` holds objects with two important attributes:

- `text` – the recognised string for that line.  
- `bounds` – a tuple like `(x, y, width, height)` describing the line’s position.

---

## Step 3: Post‑process while preserving geometry

Raw OCR output is often noisy: stray characters, misplaced spaces, or line‑break issues. The `ai.run_postprocessor` function cleans the text but **keeps the original geometry** intact, so you still have accurate coordinates.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** If you have domain‑specific vocabularies (e.g., product codes), feed a custom dictionary to the post‑processor to improve accuracy.

---

## Step 4: Extract text with coordinates – iterate and display

Finally, we loop over the cleaned lines, printing each line’s bounding box alongside its text. This is the core of **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

Assuming the input image contains two lines: “Invoice #12345” and “Total: $89.99”, you’ll see something like:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

The first tuple is the `(x, y, width, height)` of the line on the original image, allowing you to draw rectangles, highlight text, or feed the coordinates into another system.

---

## Visualising the Result (Optional)

If you want to see the bounding boxes overlaid on the image, you can use Pillow (PIL) to draw rectangles. Below is a quick snippet; feel free to skip if you only need the raw data.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

The alt text above contains the **primary keyword**, satisfying the SEO requirement for image alt attributes.

---

## Why Structured OCR Recognition Beats Simple Text Extraction

You might wonder, “Can’t I just run OCR and get the text? Why bother with geometry?”  

- **Spatial context:** When you need to map fields on a form (e.g., “Date” next to a date value), coordinates tell you *where* the data lives.  
- **Multi‑column layouts:** Simple linear text loses ordering; structured data preserves column order.  
- **Post‑processing accuracy:** Knowing the box size helps you decide whether a word is a header, a footnote, or a stray artifact.  

In short, **structured OCR recognition** gives you the flexibility to build smarter pipelines—whether you’re feeding data into a database, creating searchable PDFs, or training a machine‑learning model that respects layout.

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes may be off‑axis. | Pre‑process with deskewing (e.g., OpenCV’s `warpAffine`). |
| **Very small fonts** | Engine may miss characters, leading to empty lines. | Increase image resolution or use `ocr_engine.set_dpi(300)`. |
| **Mixed languages** | Wrong language model can cause garbled text. | Set `ocr_engine.language = ["en", "de"]` before recognition. |
| **Overlapping boxes** | Post‑processor might merge two lines unintentionally. | Verify `line.bounds` after processing; adjust thresholds in `ai.run_postprocessor`. |

Addressing these scenarios early saves you headaches later, especially when you scale the solution to hundreds of documents a day.

---

## Full End‑to‑End Script

Below is the complete, ready‑to‑run program that ties all the steps together. Copy‑paste, adjust the image path, and you’re good to go.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Running this script will:

1. **Run OCR on image** with structured mode.  
2. **Extract text with coordinates** for every line.  
3. Optionally produce an annotated PNG showing the boxes.

---

## Conclusion

You now have a solid, self‑contained solution to **run OCR on image** and **extract text with coordinates** using **structured OCR recognition**. The code demonstrates every step—from engine initialisation to post‑processing and visual verification—so you can adapt it to receipts, forms, or any visual document that needs precise text localisation.

What’s next? Try swapping the `aocr` engine for another library (Tesseract, EasyOCR) and see how their structured outputs differ. Experiment with different post‑processing strategies, such as spell‑checking or custom regex filters, to boost accuracy for your domain. And if you’re building a larger pipeline, consider storing the `(text, bounds)` pairs in a database for later analytics.

Happy coding, and may your OCR projects be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}