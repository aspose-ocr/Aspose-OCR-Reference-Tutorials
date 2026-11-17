---
category: general
date: 2026-04-26
description: How to run OCR on a scanned form, learn how to preprocess image to reduce
  noise, and extract text from image quickly.
draft: false
keywords:
- how to run OCR
- how to preprocess image
- extract text from image
- how to extract text
- how to reduce noise
language: en
og_description: How to run OCR on scanned documents, preprocess images, reduce noise,
  and extract text efficiently.
og_title: How to Run OCR and Preprocess Images – Quick Guide
tags:
- OCR
- image processing
- Python
title: How to Run OCR and Preprocess Images – Extract Text from Scanned Forms
url: /python-java/general/how-to-run-ocr-and-preprocess-images-extract-text-from-scann/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR – A Complete Guide for Extracting Text from Images

Ever wondered **how to run OCR** on a messy scanned form and get clean, searchable text? You're not the only one. In many real‑world projects the raw image is full of speckles, uneven lighting, and other quirks that make straight‑out‑of‑the‑box OCR stumble.  

The good news? With just a few lines of Python and a smart preprocessing pipeline, you can dramatically boost recognition accuracy, **reduce noise**, and pull out the exact words you need. In this tutorial we’ll walk through every step—from loading the picture to printing the final string—so you’ll walk away with a ready‑to‑drop snippet you can adapt to invoices, receipts, or any scanned document.

## What You'll Build

- An `OcrEngine` instance that talks to the underlying OCR library.  
- A preprocessing chain that **binarizes** the image and applies a **median blur** to smooth out speckles.  
- A simple call to `process()` that returns an object exposing `text`, the extracted string.  

By the end you’ll have a self‑contained script that you can run on any image file and immediately see the extracted text in the console.

## Prerequisites

- Python 3.9+ (the syntax used here matches the latest stable release).  
- The fictional `aocr` package – think of it as a thin wrapper around Tesseract or any modern OCR engine. Install it with `pip install aocr`.  
- A scanned image (`scanned_form.jpg`) placed in a folder you can reference.  

If you’re using a real OCR library like `pytesseract`, you can swap `OcrEngine` for the appropriate class—everything else stays the same.

![](how-to-run-ocr-example.png "how to run OCR example showing a scanned form and extracted text")

*Alt text: how to run OCR on a scanned document and view the extracted text.*

---

## Step 1: How to Run OCR – Initialize the Engine

Before the engine can read anything, we need to create an instance. Think of the `OcrEngine` as the brain that will later interpret the visual data.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()
```

> **Why this matters:** Instantiating the engine sets up internal models, loads language packs, and prepares the runtime environment. Skipping this step usually results in a `NoneType` error when you later call `process()`.

---

## Step 2: How to Preprocess Image – Load Your Scanned Form

Now that the brain is ready, we feed it a picture. The image can be any format supported by `aocr.Image`.

```python
# Step 2: Load the image you want to recognize
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/scanned_form.jpg")
```

> **Pro tip:** Use absolute paths during development to avoid “file not found” surprises when the script runs from a different working directory.

---

## Step 3: How to Reduce Noise – Apply Binarization & Median Blur

Raw scans often contain stray dots, uneven background, or faint shadows. Two classic tricks—**binarization** and **median blur**—clean things up without sacrificing the edges that define characters.

```python
# Step 3: Pre‑process the image to improve recognition accuracy
# • Binarize converts the image to black‑and‑white using a threshold
# • Median blur reduces noise while preserving edges
ocr_engine.image = ocr_engine.image.apply_filters(
    aocr.ImageFilters.binarize(threshold=180),
    aocr.ImageFilters.median_blur(radius=2)
)
```

### Digging Deeper

- **Binarization**: The `threshold=180` value tells the algorithm: “Anything brighter than 180 becomes white; everything else turns black.” Adjust this number if your scan is overly dark or light.  
- **Median Blur**: A radius of `2` means the filter looks at a 5×5 pixel window and replaces the center pixel with the median value. This smooths out isolated speckles while keeping the strokes of letters intact.

> **Edge case:** If your document has colored highlights, a simple binary threshold may erase them. In that scenario, consider using `aocr.ImageFilters.adaptive_threshold()` instead—this adapts the cutoff locally across the image.

---

## Step 4: How to Extract Text – Run the OCR Process

With a clean image in hand, we finally let the engine do its magic.

```python
# Step 4: Run the OCR process on the prepared image
ocr_result = ocr_engine.process()
```

> **What happens under the hood?** The engine runs a neural network (or legacy pattern matcher) over the pixel matrix, translates each recognized glyph into Unicode characters, and assembles them into lines and paragraphs.

---

## Step 5: How to Extract Text – Print the Result

The `ocr_result` object exposes a convenient `text` attribute. Let’s see what we got.

```python
# Step 5: Print the extracted text
print(ocr_result.text)
```

### Expected Output

If the scanned form contains:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

You should see something like:

```
Name: Jane Doe
Date: 2024-04-24
Amount: $123.45
```

Notice how the preprocessing step eliminated stray dots that previously turned “Amount” into “Am0unt”. That’s the power of **how to reduce noise** before OCR.

---

## Common Pitfalls & How to Fix Them

| Symptom | Likely Cause | Quick Fix |
|---------|--------------|-----------|
| Garbled characters (e.g., “@#%”) | Image too dark or too bright | Tweak the `threshold` in `binarize()`; try `adaptive_threshold`. |
| Missing words | Noise still present | Increase `radius` for `median_blur` or add a `gaussian_blur` filter. |
| Wrong language (e.g., English letters become Chinese) | Wrong language pack loaded | Pass `language="eng"` when creating `OcrEngine()` if the library supports it. |
| Slow processing on large files | High resolution | Downscale the image first: `aocr.ImageFilters.resize(width=1200)` before binarization. |

---

## Going Further – Next Steps and Related Topics

- **Batch processing**: Wrap the above logic in a loop to handle dozens of files automatically.  
- **Structured output**: Use regular expressions on `ocr_result.text` to pull out fields like dates or amounts.  
- **Alternative libraries**: Swap `aocr` for `pytesseract`—the code changes only at the engine initialization step.  
- **How to preprocess image for PDFs**: Convert each PDF page to an image, then apply the same pipeline.  

These extensions let you scale the solution from a single form to an enterprise‑grade document ingestion pipeline.

---

## Conclusion

We’ve covered **how to run OCR** from start to finish, showed **how to preprocess image** to **reduce noise**, and demonstrated **how to extract text from image** with a clean, reproducible script. The key takeaway? A few simple filters—binarization and median blur—can turn a noisy scan into a reliable source of data, saving you hours of manual cleanup.

Give the script a spin with your own documents, tweak the thresholds, and watch the accuracy climb. When you’re ready, explore batch processing or integrate the output into a database for searchable archives. Happy coding, and may your OCR always be spot‑on!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}