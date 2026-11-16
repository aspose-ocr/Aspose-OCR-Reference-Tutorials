---
category: general
date: 2026-06-06
description: Run OCR on image using Python and see confidence scores. Learn how to
  filter low‑confidence words, set thresholds, and handle edge cases.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: en
og_description: Run OCR on image in Python, inspect confidence levels, and filter
  low‑confidence words. This tutorial walks you through a complete, runnable example.
og_title: Run OCR on Image with Python – Full Guide
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Run OCR on Image with Python – Complete Step‑by‑Step Guide
url: /python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image with Python – Complete Step‑by‑Step Guide

Ever needed to **run OCR on image** files but weren’t sure how to get reliable text out of them? You’re not alone—many developers hit the same wall when the extracted words look shaky and the confidence score is a mystery.  

In this guide we’ll dive straight into a working solution: you’ll see how to run OCR on image, read the overall confidence, and pull out any low‑confidence words that might need manual review. By the end you’ll have a reusable script, understand why each line matters, and know how to tweak the confidence threshold for your own projects.

## What This Tutorial Covers

We’ll walk through the entire workflow—from loading an image to printing a tidy report of words that fell below an 80 % confidence mark. Along the way we’ll discuss:

* Choosing a solid OCR engine (we’ll use **EasyOCR**, a popular Python OCR library)  
* Interpreting the `confidence` attribute that every OCR result returns  
* Filtering words with a custom **OCR confidence threshold**  
* Extending the script for batch processing or alternative engines like **pytesseract**  

No prior OCR experience is required, just a basic familiarity with Python and a working environment (Python 3.9+ recommended).  

Ready to turn blurry screenshots into clean, searchable text? Let’s get started.

---

## ## How to Run OCR on Image with Python

The heart of the tutorial is a three‑step snippet that mirrors the code you already saw. Below we’ll break each line apart, explain the why, and then give you a full, copy‑and‑paste‑ready script.

### Step 1: Install and Import the OCR Engine

First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box for many languages and gives you a confidence score per word.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Why EasyOCR?* It bundles a deep‑learning model that’s been trained on diverse datasets, so you typically get higher confidence values than the older Tesseract engine, especially on mixed‑quality images.

> **Pro tip:** If you’re on a constrained environment (e.g., a tiny Docker container), `pytesseract` might be lighter, but you’ll lose some of the modern accuracy EasyOCR provides.

### Step 2: Run OCR on the Image

Now we actually **run OCR on image**. The `recognize_image` method from the original example is replaced with EasyOCR’s `readtext` call, which returns a list of `(bbox, text, confidence)` tuples.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Each entry in `ocr_results` looks like:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

The third element (`0.92` in the example) is the confidence score ranging from 0 to 1.

### Step 3: Summarize Overall Confidence

Unlike the earlier snippet that printed a single `confidence` attribute, EasyOCR gives a confidence per word. To get an overall sense, we’ll average them:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Why average?* It gives you a quick health check—if the overall confidence is below, say, 70 %, you probably need to improve the image (better lighting, preprocessing, etc.).

### Step 4: List Low‑Confidence Words

Now comes the part that directly answers the “list words whose confidence is below the desired threshold” requirement. We’ll set a **OCR confidence threshold** of 0.80 (80 %) by default, but you can adjust it.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

The loop prints each word that didn’t make the cut, together with its percentage confidence. This is the exact analogue of the original `for recognized_word in recognition_result.words` loop, but now works with EasyOCR’s output format.

---

## ## Understanding OCR Confidence Scores

Confidence isn’t a magic number; it’s the model’s estimate of how sure it is about a particular transcription. Here are a few things to keep in mind:

| Situation | Typical Confidence | What to Do |
|-----------|-------------------|------------|
| Clear, high‑resolution scan | 0.95 – 1.00 | No extra work needed |
| Slight blur or uneven lighting | 0.80 – 0.94 | Consider slight preprocessing (contrast boost) |
| Heavy noise, rotated text | < 0.70 | Apply image preprocessing (deskew, denoise) or switch to a different OCR engine |

> **Watch out:** Some languages (e.g., cursive handwriting) naturally produce lower scores. Adjust the threshold accordingly.

### Edge Cases & Variations

1. **Batch Processing** – If you need to **run OCR on image** files in bulk, wrap the above logic in a loop that iterates over a directory.  
2. **Multiple Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine will detect both.  
3. **Alternative Engines** – Want to try **pytesseract**? Replace the reader block with:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   You’ll then need to aggregate per‑character confidences into per‑word values—a bit more work but doable.

4. **Pre‑processing Tricks** – Applying OpenCV filters (`cv2.threshold`, `cv2.GaussianBlur`) can boost confidence for noisy scans.  

---

## ## Full, Ready‑to‑Run Script

Below is the complete Python file you can drop into your project. Save it as `ocr_report.py` and run `python ocr_report.py`. Make sure the image path points to a real file.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Expected output** (your numbers will vary):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

If every word clears the 80 % bar you’ll see the friendly “All words meet the confidence threshold.” message instead.

---

## ## Frequently Asked Questions (FAQ)

**Q: Does this work with PDFs?**  
A: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`) and then feed the PNG/JPEG into the script.

**Q: My confidence numbers are all low—what can I do?**  
A: Try image preprocessing: increase contrast, remove background noise, or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths` parameter you can tweak.

**Q: Can I export the results to CSV?**  
A: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter` where each row contains `text`, `confidence`, and bounding‑box coordinates.

**Q: Is there a GPU‑accelerated version?**  
A: EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed. Verify with `torch.cuda.is_available()` before running the script.

---

## Conclusion

We’ve just **run OCR on image** using Python, inspected the overall confidence, and isolated any low‑confidence words that need a


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}