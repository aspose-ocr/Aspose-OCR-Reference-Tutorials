---
category: general
date: 2026-06-25
description: How to use OCR in Python – learn how to load image for OCR, recognize
  text in region, and extract region text quickly.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: en
og_description: How to use OCR in Python – step-by-step guide to load an image, recognize
  text in a specific region, and extract the invoice number.
og_title: 'How to Use OCR Python: Load Image and Extract Region Text'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'How to Use OCR Python: Load Image and Extract Region Text'
url: /python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Use OCR Python: Load Image and Extract Region Text

**How to use OCR in Python** is simpler than you think. Ever stared at a scanned invoice and wondered how to pull just the invoice number without parsing the whole page? You're not alone—many developers hit that snag when they first dabble with optical character recognition. In this guide we’ll walk through loading an image for OCR, defining a rectangle, recognizing text in that region, and finally extracting the region text. By the end you’ll have a ready‑to‑run script that isolates any piece of text you need.

> *Pro tip:* If you’re working with PDFs, convert each page to an image first—most OCR libraries handle PNG/JPEG best.

## What You’ll Need

- Python 3.8+ (the latest stable release is recommended)  
- An OCR library that exposes an `OcrEngine` class (e.g., **ocr** from `pip install ocr-lib`)  
- A sample image—here we’ll use `invoice.png` placed in a folder you control  
- Basic familiarity with rectangles (x, y, width, height)  

No heavy dependencies, no GPU required—just plain CPU work, which keeps things portable.

---

## How to Use OCR: Initialize the Engine (Step 1)

Before any text can be read, you need an OCR engine instance. Think of it as the brain that will analyze pixel patterns.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Why this matters:* Initializing the engine loads language models and sets default configurations. Skipping this step would raise an exception the moment you call `recognize_region`.

---

## Load Image for OCR (Step 2)

Now that the engine is ready, we feed it an image. The library’s `Image.load` method handles common formats and normalizes the bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

If the file isn’t found, Python will throw a `FileNotFoundError`. Make sure the path is absolute or relative to your script’s working directory.  

*Edge case:* Some OCR engines expect a grayscale image. If you notice poor accuracy, convert the image first:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Recognize Text in Region (Step 3)

Defining the region is where you tell the engine *where* to look. The `Rectangle` takes floating‑point values for sub‑pixel precision, which can be handy when dealing with high‑resolution scans.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – top‑left corner of the rectangle (in pixels)  
- **width, height** – size of the box  

You might wonder how to find these numbers. A quick way is to open the image in any editor (e.g., GIMP or Paint.NET) and use the selection tool to read the coordinates.  

*Why not just OCR the whole page?* Limiting the area reduces noise, speeds up processing, and dramatically improves accuracy for small fields like invoice numbers.

---

## How to Extract Region Text (Step 4)

With the region set, ask the engine to recognize only that slice. The result object contains the raw text and confidence scores.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

If the OCR engine supports multiple languages, you can pass an optional language code:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Common pitfall:* Some engines return a list of words instead of a single string. In such cases, concatenate them:

```python
text = " ".join(region_result.words)
```

---

## Output the Extracted Invoice Number (Step 5)

Finally, print—or store—the extracted text. You can also post‑process the string to remove stray whitespace or non‑numeric characters.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Running the script with a correctly aligned rectangle should yield something like:

```
Invoice number: 20231578
```

If you get garbage characters, double‑check the rectangle coordinates or consider increasing the image resolution.

---

## Full Working Example

Putting it all together, here’s a self‑contained script you can copy‑paste and run:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Save the file as `extract_invoice.py`, replace `YOUR_DIRECTORY` with the actual folder, and run:

```bash
python extract_invoice.py
```

You should see the invoice number printed to the console.

---

## Frequently Asked Questions

**Q: What if the invoice number is printed in a fancy font?**  
A: Most modern OCR engines handle a wide range of fonts, but you can boost accuracy by training a custom language model or pre‑processing the image (e.g., applying a threshold filter).

**Q: Can I extract multiple fields at once?**  
A: Absolutely. Define a list of `Rectangle` objects—one per field—and loop over them, storing each result in a dictionary.

**Q: Does this work on multi‑page PDFs?**  
A: Convert each page to an image first (using `pdf2image` or similar), then apply the same region‑based extraction per page.

---

## Wrapping Up

In this tutorial we covered **how to use OCR** in Python to load an image, recognize text in a specific region, and extract that region’s text—perfect for pulling invoice numbers, order IDs, or any small data snippet from scanned documents. By isolating the area of interest you gain speed, accuracy, and less post‑processing hassle.

Ready for the next step? Try extending the script to handle **load image for OCR** from a folder of batch invoices, or experiment with **recognize text in region** for different fields like dates and totals. The same pattern applies—just change the rectangle coordinates.

If you ran into any snags or have ideas for improvement, drop a comment below. Happy coding, and may your OCR pipelines be ever accurate!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}