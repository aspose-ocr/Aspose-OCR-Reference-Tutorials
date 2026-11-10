---
category: general
date: 2026-05-31
description: Learn how to use OCR region of interest to load image for OCR and extract
  text from rectangle, perfect for recognizing amount on an invoice.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: en
og_description: Master OCR region of interest to load image for OCR, extract text
  from rectangle and recognize text from invoice in a single tutorial.
og_title: OCR Region of Interest – Step‑by‑Step Python Guide
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR Region of Interest – Extract Text from Rectangle in Python
url: /python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Region of Interest – Extract Text from Rectangle in Python

Ever wondered how to **ocr region of interest** a specific part of a scanned invoice without feeding the whole page into the engine? You're not the first one staring at a blurry receipt and thinking, “How do I extract the amount that lives somewhere in the lower right?” The good news is that you can tell the OCR library exactly where to look, dramatically boosting both speed and accuracy.

In this guide we’ll walk through a complete, runnable example that shows you how to **load image for OCR**, define a **region of interest**, and then **extract text from rectangle** to finally **recognize text from invoice** and answer the classic “how to extract amount” question. No vague references—just concrete code, clear explanations, and a few pro tips you’ll wish you’d known earlier.

---

## What You’ll Build

By the end of this tutorial you’ll have a tiny Python script that:

1. Loads an invoice image from disk.  
2. Marks a rectangular ROI where the total amount lives.  
3. Runs OCR only inside that ROI.  
4. Prints the cleaned‑up amount string.  

All of this works with any OCR library that supports ROI—here we’ll use a fictitious but representative `SimpleOCR` package that mimics popular tools like Tesseract or EasyOCR. Feel free to swap it out; the concepts stay the same.

---

## Prerequisites

- Python 3.8+ installed (`python --version` should show ≥3.8).  
- A pip‑installable OCR package (e.g., `pip install simpleocr`).  
- An invoice image (PNG or JPEG) placed in a folder you can reference.  
- Basic familiarity with Python functions and classes (nothing fancy).

If you already have those, great—let’s dive in. If not, grab the image first; the rest of the steps are independent of the actual file content.

---

## Step 1: Load Image for OCR

The first thing any OCR workflow needs is a bitmap to read from. Most libraries expose a simple `load_image` method that accepts a file path. Here’s how you do it with our `SimpleOCR` engine:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Use absolute paths or `os.path.join` to avoid “file not found” surprises when running the script from a different working directory.

---

## Step 2: Define OCR Region of Interest

Instead of letting the engine scan the whole page, we tell it *exactly* where the amount sits. This is the **ocr region of interest** step, and it’s the key to reliable extraction, especially when the document contains noisy headers or footers.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Why those numbers? `x` and `y` are pixel offsets from the top‑left corner, while `width` and `height` describe the box size. If you’re unsure, open the image in any editor, enable a ruler, and note the coordinates. Many IDEs even let you print the cursor position while hovering.

---

## Step 3: Extract Text from Rectangle

Now that the ROI is set, we ask the engine to **recognize text from invoice** but limited to the rectangle we just added. The call returns a result object that typically contains the raw string, confidence scores, and sometimes bounding boxes.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

Behind the scenes, `recognize()` iterates over each ROI, crops that slice, runs the OCR model, and stitches the results together. This is why defining a tight **extract text from rectangle** region can shave seconds off processing time for batch jobs.

---

## Step 4: How to Extract Amount – Clean the Output

OCR isn’t perfect; you’ll often get stray spaces, line feeds, or even mis‑read characters (think “S” vs “5”). A quick `strip()` and a tiny regex usually do the trick for monetary values.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** If you plan to feed the amount into a database or a payment gateway, you need a predictable format. Stripping whitespace and filtering non‑numeric characters prevents downstream errors.

---

## Step 5: Recognize Text from Invoice – Full Script

Putting it all together, here’s the complete, ready‑to‑run script. Save it as `extract_amount.py` and execute `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Expected Output

```
Amount: 1,245.67
```

If the ROI is mis‑aligned, you might see something like `Amount: 1245.6S`—notice the stray “S”. Adjust the rectangle coordinates and rerun until the output looks clean.

---

## Common Pitfalls & Edge Cases

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **ROI too small** | The amount text gets clipped, leading to partial recognition. | Expand `width`/`height` by ~10‑20 % and re‑test. |
| **Incorrect DPI** | Low‑resolution scans (≤150 dpi) reduce OCR accuracy. | Resample the image to 300 dpi before loading, or ask the scanner for higher DPI. |
| **Multiple currencies** | Regex picks the first numeric group, which might be an invoice number. | Refine the regex to look for currency symbols (`$`, `€`, `£`) before the digits. |
| **Rotated invoices** | OCR engines assume upright text; rotated pages break recognition. | Apply a rotation correction (`ocr_engine.rotate(90)`) before adding ROI. |
| **Noise in background** | Shadows or stamps confuse the model. | Pre‑process with a simple threshold (`cv2.threshold`) or use a denoising filter. |

Addressing these edge cases early saves you hours of debugging later.

---

## Pro Tips for Real‑World Projects

- **Batch Processing:** Loop over a folder of invoices, compute ROI dynamically (e.g., based on template detection), and store results in CSV.  
- **Template Matching:** If you handle several invoice layouts, maintain a JSON map of `template_id → ROI coordinates`. Switch ROI based on a quick layout classifier.  
- **Parallel Execution:** Use `concurrent.futures.ThreadPoolExecutor` to run multiple OCR instances concurrently—great for high‑volume back‑office pipelines.  
- **Confidence Filtering:** Most OCR results include a confidence score. Discard results below a threshold (e.g., 85 %) and flag them for manual review.

---

## Conclusion

We’ve covered everything you need to **ocr region of interest**, **load image for OCR**, **extract text from rectangle**, and finally **recognize text from invoice** to answer the classic **how to extract amount** question. The script is compact, yet flexible enough to adapt to different document formats, languages, and OCR back‑ends.

Now that you’ve mastered the basics, consider extending the workflow: add barcode scanning, integrate with a PDF parser, or push the extracted amount to an accounting API. The sky’s the limit, and with a well‑defined ROI you’ll always get faster, cleaner results.

If you hit a snag, drop a comment below—happy OCRing!

![ocr region of interest example](https://example.com/ocr_roi_example.png "ocr region of interest example")


## What Should You Learn Next?

- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}