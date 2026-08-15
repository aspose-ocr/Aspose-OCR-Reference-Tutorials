---
category: general
date: 2026-03-26
description: Learn how to deskew image, recognize text from image and build an image
  preprocessing pipeline to remove noise from scan and convert scanned image to text.
draft: false
keywords:
- how to deskew image
- recognize text from image
- image preprocessing pipeline
- remove noise from scan
- convert scanned image to text
language: en
og_description: How to deskew image and turn a skewed scan into searchable text. Follow
  this guide to recognize text from image, remove noise from scan, and convert scanned
  image to text.
og_title: How to Deskew Image – Step‑by‑Step OCR Guide
tags:
- OCR
- image-processing
- Python
title: How to Deskew Image – Complete Guide with OCR
url: /python-java/general/how-to-deskew-image-complete-guide-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image – Complete Guide with OCR

Ever wondered **how to deskew image** that came out of a cheap scanner? You're not alone. A crooked page looks unprofessional, and more importantly, the tilt can throw off any OCR engine trying to **recognize text from image**.  

In this tutorial we'll walk through a full **image preprocessing pipeline** that deskews, binarizes, and denoises a scan, then hands it off to an OCR engine so you can **convert scanned image to text** with minimal hassle. No magic, just plain‑vanilla Python and a tiny library that does the heavy lifting.

## What You’ll Need

- Python 3.9+ (the code works on 3.10 and newer)
- The `ocr` package (install via `pip install ocr‑toolkit` – replace with your actual library name)
- A scanned JPEG or PNG that’s noticeably skewed (e.g., `skewed_scan.jpg`)
- A little curiosity about why each preprocessing step matters

That’s it. No heavyweight dependencies like OpenCV unless you want to go deeper later.

## Step 1: Load the Scanned Image

The first thing is to pull the file into memory. This step is straightforward but crucial—if the path is wrong, everything else crashes.

```python
# Step 1: Load the scanned image
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)
```

> **Why?**  
> Loading the image gives us a manipulable object that the `ocr.ImagePreprocessor` can work with. Skipping this step would leave the pipeline blind to the actual pixel data.

## How to Deskew Image and Prepare It for OCR

Now that we have the image, let’s straighten it. The `deskew()` method estimates the tilt angle and rotates the picture back to horizontal.

```python
# Step 2: Create an image preprocessor and correct the orientation
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()
```

> **Pro tip:** If your scans are only slightly off (≤ 3°), the default algorithm is usually spot‑on. For extreme angles you might need to tweak the internal parameters—check the library docs for `max_angle`.

## Binarize the Image – Make It Black‑and‑White

OCR engines love high‑contrast input. Converting the picture to a binary (black‑and‑white) representation removes subtle shades that can confuse character recognition.

```python
# Step 3: Convert the image to a binary (black‑and‑white) representation
preprocessor.binarize(threshold=128)
```

> **What’s happening?**  
> Pixels brighter than 128 become white; everything else turns black. Adjust the threshold if your scan is unusually dark or light.

## Remove Noise from Scan Before OCR

Even a perfectly deskewed image can contain speckles, dust, or compression artifacts. Those little blobs are the bane of any OCR engine.

```python
# Step 4: Reduce noise to improve OCR accuracy
preprocessor.denoise(radius=1)
```

> **Why remove noise?**  
> Noise creates false edges that the OCR engine might interpret as characters. A small radius works for most scans; bump it up for heavily grainy documents.

## Apply the Image Preprocessing Pipeline

All the configuration is set—now we run the pipeline on the original image.

```python
# Step 5: Apply the preprocessing pipeline to the loaded image
processed_image = preprocessor.apply(original_image)
```

> **Result:** `processed_image` is a cleaned‑up, straight, high‑contrast bitmap ready for text extraction.

## Recognize Text from Image with OCR Engine

Time to actually read the text. We initialise the OCR engine, feed it our polished image, and ask for the raw string.

```python
# Step 6: Initialise the OCR engine and provide the processed image
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# Step 7: Recognise text and output the result
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Expected output** (sample):

```
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

If you see garbled characters, double‑check the deskewing step or experiment with a different `threshold` value.

## Building an Image Preprocessing Pipeline – Full Script

Putting everything together, here’s a single, runnable script you can drop into a `.py` file and execute:

```python
import ocr  # Replace with the actual import path of your OCR library

# -------------------------------------------------
# 1️⃣ Load the scanned image
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/skewed_scan.jpg"
original_image = ocr.Imaging.Image.load(image_path)

# -------------------------------------------------
# 2️⃣ Deskew – how to deskew image
# -------------------------------------------------
preprocessor = ocr.ImagePreprocessor()
preprocessor.deskew()

# -------------------------------------------------
# 3️⃣ Binarize – convert to black‑and‑white
# -------------------------------------------------
preprocessor.binarize(threshold=128)

# -------------------------------------------------
# 4️⃣ Denoise – remove noise from scan
# -------------------------------------------------
preprocessor.denoise(radius=1)

# -------------------------------------------------
# 5️⃣ Apply the pipeline
# -------------------------------------------------
processed_image = preprocessor.apply(original_image)

# -------------------------------------------------
# 6️⃣ OCR – recognize text from image
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(processed_image)

# -------------------------------------------------
# 7️⃣ Output – convert scanned image to text
# -------------------------------------------------
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

> **Tip:** Wrap the whole thing in a function (`def ocr_from_file(path): …`) if you plan to process many files in a batch.

## Common Questions & Edge Cases

- **What if the image is already upright?**  
  The `deskew()` method detects a near‑zero angle and leaves the picture untouched, so you can safely run it on every file.

- **My scan is in color—should I keep it?**  
  Color adds no value for most OCR tasks. Binarization strips it away, speeding up processing and reducing memory usage.

- **Can I chain multiple preprocessing steps?**  
  Absolutely. The `ImagePreprocessor` class is designed for pipelines; you can add `sharpen()`, `contrast_enhance()`, or custom filters before calling `apply()`.

- **The OCR output has stray line breaks—how to fix?**  
  Post‑process the string with `text.replace("\n", " ").strip()` or use a more advanced layout analysis library like Tesseract’s `--psm` modes.

## Next Steps

Now that you know **how to deskew image** and have a solid **image preprocessing pipeline**, you might explore:

- Integrating **recognize text from image** into a Flask API for on‑the‑fly document uploads.
- Using the pipeline to **remove noise from scan** of historical documents where preservation is key.
- Scaling up to batch‑process thousands of pages and output a searchable PDF using `pdfminer` or `PyMuPDF`.

Feel free to experiment with different thresholds, denoise radii, or even swap the OCR backend for Tesseract if you need multilingual support. The fundamentals stay the same: straighten, clean, then read.

---

*Happy coding! If you run into trouble, drop a comment below—I'll be glad to help you fine‑tune the pipeline.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}