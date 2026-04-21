---
category: general
date: 2026-01-12
description: Run OCR on PNG files quickly with Python. Learn how to extract text from
  image and invoice, and load image for OCR using Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: en
og_description: Run OCR on PNG instantly. This guide shows how to extract text from
  image and invoice, load image for OCR, and save results as JSON and CSV.
og_title: Run OCR on PNG – Full Python Tutorial
tags:
- OCR
- Python
- Image Processing
title: Run OCR on PNG – Complete Python Guide to Extract Text from Images
url: /python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on PNG – Complete Python Guide to Extract Text from Images

Ever needed to **run OCR on PNG** files but weren’t sure which library would give you clean, structured results? You’re not alone. In many real‑world projects—think invoice automation or receipt scanning—the first step is to **extract text from image** files, and PNG is a common format because it preserves lossless quality.

In this tutorial we’ll walk through a hands‑on example using the Aspose.OCR Python package. By the end of the guide you’ll know how to **load image for OCR**, pull out every line of text, turn that data into a tidy JSON object, and even dump it to CSV for downstream processing. No fluff, just a practical, ready‑to‑run solution.

## What You’ll Learn

- How to install and import the Aspose.OCR library.  
- The exact steps to **run OCR on PNG** and handle the result object.  
- Ways to **extract text from invoice** files and format the output as JSON or CSV.  
- Tips for dealing with low‑contrast images, multi‑language documents, and confidence scores.  
- A complete, copy‑and‑paste code sample that you can execute today.

> **Prerequisite:** Python 3.8+ and a basic familiarity with pip. If you’ve never used Aspose before, don’t worry—this guide covers everything you need to get started.

---

## Step 1 – Install Aspose.OCR and Prepare Your Environment

Before we can **run OCR on PNG**, the library has to be present on your system.

```bash
pip install aspose-ocr
```

> **Pro tip:** Use a virtual environment (`python -m venv venv`) to keep dependencies isolated. It prevents version clashes if you’re juggling multiple projects.

Once installed, import the modules we’ll need:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Here we bring in `asposeocr` for the heavy lifting and the built‑in `json` library for later serialization.

---

## Step 2 – Create the OCR Engine and Set the Language

The OCR engine is the core component that actually reads the pixels. For most English invoices, you’ll want the English language pack:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Specifying the language narrows down the character set, which boosts accuracy and speeds up processing. If you ever need to handle multilingual invoices, just swap `ocr.Language.ENGLISH` for the appropriate enum.

---

## Step 3 – Load the Image for OCR

Now we’ll **load image for OCR**. The `Image.load` method accepts a file path, and it works with PNG, JPEG, BMP, and more.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** If the PNG is unusually large (over 5 MB), consider resizing it first to keep memory usage reasonable. Pillow can do that in a single line:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Step 4 – Run OCR on PNG and Capture the Result

With the engine ready and the image loaded, it’s time to **run OCR on PNG** and retrieve the structured result.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

The `ocr_result` object contains a collection of `OcrRegion` items, each with the recognized text and a confidence score (0‑100). This is where you get the granular data needed to **extract text from invoice** lines.

---

## Step 5 – Convert the Result to JSON and Pretty‑Print It

Most downstream systems love JSON, so we’ll turn the OCR output into a nicely formatted string.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Sample Output

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Notice how each line includes a confidence metric—perfect for filtering out low‑confidence entries if you plan to **extract text from invoice** automatically.

---

## Step 6 – Save the OCR Data as CSV (One Line per Text + Confidence)

CSV is ideal for spreadsheets or quick data imports. Aspose offers a one‑liner to dump everything into a CSV file.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

The generated CSV will look like this:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

You can now open it in Excel, Google Sheets, or feed it into a database.

---

## Bonus – Handling Low‑Confidence Text and Multi‑Page PDFs

### Filtering by Confidence

If you only want high‑certainty lines, filter the JSON before you write it out:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Multi‑Page Documents

Aspose.OCR automatically creates a new `page` entry for each page in a multi‑page PNG or PDF. Loop through `ocr_data["pages"]` to process them all—no extra code needed.

---

## Full Working Example

Below is the **complete script** you can copy, paste, and run immediately. Replace `YOUR_DIRECTORY` with the folder that holds your PNG file.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Run the script with `python run_ocr.py` and you’ll see the JSON dump in the console, a CSV file on disk, and a filtered list of high‑confidence entries.

---

## Frequently Asked Questions

**Q: Can I use this to extract text from a scanned receipt instead of an invoice?**  
A: Absolutely. The same workflow applies—just point `image_path` at your receipt PNG. If the receipt uses a different language, switch `engine.language` accordingly.

**Q: What if my PNG contains rotated text?**  
A: Aspose.OCR automatically detects orientation, but for stubborn cases you can manually rotate the image with Pillow before feeding it to the engine.

**Q: Do I need a paid license for Aspose.OCR?**  
A: The library offers a free evaluation mode with a watermark on the output. For production use you’ll need a license, which you can obtain from the Aspose website.

---

## Conclusion

We’ve covered everything you need to **run OCR on PNG** files using Python: installing the SDK, loading the image, extracting structured text, and saving the result as JSON or CSV. Whether you’re looking to **extract text from image** for a simple script or **extract text from invoice** for an automated accounting pipeline, the steps above give you a solid, production‑ready foundation.

Next, you might explore:

- Integrating the CSV output with a database for bulk invoice storage.  
- Adding post‑processing with regular expressions to pull out dates, amounts, or tax IDs.  
- Using the `ocr_engine.recognize_barcode` feature if your invoices include QR codes.

Give it a try, tweak the confidence thresholds, and watch your document‑processing workflow become a breeze. Got more questions or a cool use‑case to share? Drop a comment below—happy OCRing!  

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – visual example of OCR result")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}