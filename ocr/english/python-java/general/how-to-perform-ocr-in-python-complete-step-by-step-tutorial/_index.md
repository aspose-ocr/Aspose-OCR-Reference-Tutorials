---
category: general
date: 2026-03-26
description: Learn how to perform OCR in Python and recognize text from image files.
  This guide shows how to extract text from PNG and convert image to text quickly.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: en
og_description: How to perform OCR in Python? Follow this guide to recognize text
  from image, extract text from PNG, and convert image to text with a trial license.
og_title: How to Perform OCR in Python – Complete Tutorial
tags:
- OCR
- Python
- Image Processing
title: How to Perform OCR in Python – Complete Step‑by‑Step Tutorial
url: /python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Perform OCR in Python – Complete Step‑by‑Step Tutorial  

Ever wondered **how to perform OCR** on a picture you just snapped on your phone? You’re not alone—developers everywhere need a reliable way to recognize text from image files without wrestling with complex native libraries.  

In this tutorial we’ll walk through a hands‑on example that shows **how to perform OCR**, **recognize text from image**, and **extract text from PNG** using a lightweight Python wrapper. By the end you’ll be able to **convert image to text** in just a few lines of code, and you won’t have to worry about licensing headaches because we’ll use the built‑in trial mode.

## What You’ll Learn  

* How to set up a trial license for the OCR engine (no file path needed).  
* The exact sequence of calls to **recognize text from image** objects.  
* Ways to **extract text from PNG** files and handle common pitfalls like missing fonts.  
* Tips for scaling the solution when you move from a trial to a production license.  

**Prerequisites** – you need Python 3.8+ and the `ocr` package (installable via `pip install ocr`). No other external tools are required.

---  

![how to perform OCR example](https://example.com/ocr-demo.png "how to perform OCR in Python – recognized text displayed")  

*Image alt text: how to perform OCR in Python – sample output*  

## Step 1 – Activate a Trial License (No File Path Needed)  

Before the engine can read anything, it needs a valid license. The trial mode is perfect for experiments and small projects.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Why this matters:* The license object tells the OCR library that you’re operating in a sandbox. If you skip this step, the engine will raise a `LicenseError` the moment you call `recognize()`.  

**Pro tip:** When you move to a paid license, replace the two lines above with `ocr.License("path/to/your/license.key").apply()`.

## Step 2 – Create the OCR Engine Instance  

Now that the trial is active, we instantiate the main engine. Think of it as the “brain” that will look at the image and decide what characters are where.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Why this matters:* The `OcrEngine` holds configuration like language packs and DPI settings. You can tweak those later, but the default works for most English‑only PNGs.

## Step 3 – Load the PNG You Want to Process  

Here’s where we **recognize text from image**. The `ocr.Imaging.Image.load()` method supports PNG, JPEG, BMP, and a few other formats.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Edge case:* If your PNG uses an indexed palette (common for screenshots), the loader will automatically convert it to a 24‑bit RGB buffer. That conversion can be a tiny performance hit, but it guarantees accurate OCR results.

## Step 4 – Run the OCR and Grab the Text  

Finally, we ask the engine to do its thing and then pull the plain‑text result.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Expected output** (example for a simple image containing “Hello World”):

```
Hello World
```

If the image contains multiple lines, the output will preserve line breaks, making it easy to feed downstream processes like CSV parsers or NLP pipelines.

## Optional: Fine‑Tuning for Better Accuracy  

* **Language packs:** `ocr_engine.set_language("eng")` (default) or `"fra"` for French.  
* **DPI scaling:** `ocr_engine.set_dpi(300)` can improve results on low‑resolution scans.  
* **Pre‑processing:** Applying a binary threshold (`ocr.Imaging.Image.threshold()`) before `set_image` often yields cleaner text on noisy backgrounds.

These tweaks are useful when you move from a quick demo to a production‑grade **ocr tutorial python** that processes hundreds of files a day.

## Full Script – Ready to Copy & Paste  

Below is the complete, runnable script that combines all the steps above. Save it as `run_ocr.py` and replace `YOUR_DIRECTORY/sample1.png` with the path to your own PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Run it from the command line:

```bash
python run_ocr.py
```

You should see the extracted text printed to the console. If you get an empty string, double‑check that the image actually contains clear, high‑contrast text and that the trial license applied without errors.

## Common Questions & Gotchas  

* **“Does this work with JPEG?”** – Absolutely. The `load()` method auto‑detects format, so you can swap PNG for JPEG without code changes.  
* **“What if the image is rotated?”** – The engine can auto‑detect orientation, but for best results you can pre‑rotate with `input_image.rotate(90)` before `set_image`.  
* **“Can I process multiple images in a loop?”** – Yes. Just move the loading and `recognize()` calls inside a `for` loop; the same `ocr_engine` instance can be reused, which saves a tiny amount of overhead.  

## Next Steps – From Demo to Production  

Now that you know **how to perform OCR**, consider these follow‑up topics:

* **Batch processing** – Combine this script with `os.listdir()` to **extract text from PNG** files in bulk.  
* **Integrate with PDF** – Use `pdf2image` to convert PDF pages to PNG, then feed them into the same pipeline.  
* **Post‑processing** – Apply regex or fuzzy matching to clean up common OCR mis‑recognitions (e.g., “0” vs “O”).  

Each of these builds on the core idea of **convert image to text** and expands the usefulness of your OCR workflow.

---  

### TL;DR  

We’ve covered everything you need to know to **how to perform OCR** in Python: activate a trial license, create an engine, load a PNG, run the recognition, and print the result. With just a handful of lines you can **recognize text from image**, **extract text from PNG**, and **convert image to text** for any downstream application.  

Give it a try, tweak the DPI or language settings, and let the engine do the heavy lifting. Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}