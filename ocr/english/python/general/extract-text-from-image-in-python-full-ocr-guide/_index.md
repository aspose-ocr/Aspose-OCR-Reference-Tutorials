---
category: general
date: 2026-06-25
description: Extract text from image using Python OCR. Learn how to load image for
  OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: en
og_description: Extract text from image using Python OCR. This tutorial walks you
  through loading an image for OCR, performing OCR in Python, and converting a receipt
  to JSON.
og_title: Extract Text from Image in Python – Full OCR Guide
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Extract Text from Image in Python – Full OCR Guide
url: /python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image in Python – Full OCR Guide

Ever needed to **extract text from image** but weren’t sure where to start? In this tutorial we’ll walk you through how to **load image for OCR**, **perform OCR in Python**, and **convert receipt to JSON**—all with just a handful of lines of code.

If you’ve ever built a receipt‑scanning app, an expense‑tracker, or just want to automate data entry, you’ll see why mastering this flow is a game‑changer. By the end you’ll have a working script that reads a picture of a receipt and spits out a clean JSON payload ready for downstream services.

## What You’ll Learn

We’ll cover every step from installing the `aocr` library to handling the raw result. Specifically you’ll learn how to:

1. **Create an OCR engine instance** – the entry point for all recognition work.  
2. **Load an image for OCR** – tell the engine which file to read.  
3. **Choose the export format** – JSON or XML, we’ll pick JSON because it’s easier to consume.  
4. **Run the recognition** – actually perform OCR in Python.  
5. **Print or store the result** – convert receipt to JSON and see the output.

No prior experience with OCR is required; just a basic Python setup and an image file (a receipt, a flyer, whatever you need).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="extract text from image using Python OCR"}

## Extract Text from Image – Step‑by‑Step Python OCR

Below is the complete, ready‑to‑run script. Feel free to copy‑paste it into a file called `receipt_ocr.py` and run `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Why This Works

- **Engine instance** – `aocr.OcrEngine()` encapsulates all the heavy lifting (model loading, preprocessing, etc.).  
- **Loading the image** – `engine.load_image()` tells the library exactly which bitmap to analyze; you can feed JPEG, PNG, or even multi‑page PDFs.  
- **Export format** – Setting `engine.export_format` to `aocr.ExportFormat.JSON` makes the result a structured string, perfect for APIs that expect JSON.  
- **Recognition call** – `engine.recognize()` runs the neural net inference behind the scenes; it returns a JSON string that contains detected text blocks, confidence scores, and layout information.  

---

## Load Image for OCR with aocr

If you’re wondering whether the image needs any special preprocessing, the short answer is **no**—`aocr` handles most common cases (contrast adjustment, deskewing) automatically. However, you can improve accuracy by:

- Ensuring the image is at least 300 dpi.  
- Cropping out irrelevant borders.  
- Converting to grayscale before feeding it (optional, `engine.load_image()` will do it for you).

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* If the receipt contains a lot of noise, the extra step above can boost the **perform OCR in Python** accuracy by a noticeable margin.

---

## Choose Export Format and Convert Receipt to JSON

You might ask, “Why not just get plain text?” Because JSON preserves the hierarchical structure (lines, words, bounding boxes). This makes it far easier to map fields like *total amount* or *date* later on.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

When you run the script, `json_result` will look something like this (trimmed for brevity):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

You now have a **convert receipt to JSON** payload you can feed straight into a database, a REST endpoint, or a machine‑learning model.

---

## Run Recognition and Retrieve Results

The final step—actually performing the OCR—is as simple as calling `recognize()`. Behind the scenes the library:

1. Sends the image through a pre‑trained convolutional network.  
2. Decodes the network output into readable characters.  
3. Packages everything into the selected format (JSON in our case).

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

If you need to store the output instead of printing, just write it to a file:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Some receipts contain non‑ASCII characters (e.g., “€”). Ensure you open the file with UTF‑8 encoding, as shown above, to avoid garbled text.

---

## Full Working Example (All Steps in One Script)

Putting everything together, here’s the final script you can run end‑to‑end:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Run it with:

```bash
python receipt_ocr.py
```

You should see a confirmation line and, in the same folder, a `receipt_output.json` file containing the structured data.

---

## Conclusion

You now know **how to extract text from image** using Python, how to **load image for OCR**, how to **perform OCR in Python**, and how to **convert receipt to JSON** for downstream consumption. This end‑to‑end flow is lightweight, requires only the `aocr` package, and can be dropped into any automation pipeline.

What’s next? Try swapping the export format to XML, experiment with different image preprocessing techniques, or build a tiny Flask API that accepts an uploaded receipt and returns the JSON payload instantly. The sky’s the limit once you’ve got the basics down.

Got questions or hit a snag? Drop a comment below, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}