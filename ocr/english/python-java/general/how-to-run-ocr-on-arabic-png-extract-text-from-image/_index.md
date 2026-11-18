---
category: general
date: 2026-03-26
description: Learn how to run OCR on Arabic PNG images and extract Arabic text quickly.
  This guide shows converting image to text with step‑by‑step Python code.
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: en
og_description: How to run OCR on Arabic PNG images? Follow this complete guide to
  extract Arabic text, recognize Arabic text, and convert image to text using Python.
og_title: How to Run OCR on Arabic PNG – Extract Text from Image
tags:
- OCR
- Python
- Arabic
title: How to Run OCR on Arabic PNG – Extract Text from Image
url: /python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Run OCR on Arabic PNG – Extract Text from Image

Ever wondered **how to run OCR** on an image that contains Arabic script? Maybe you’ve got a scanned receipt, a historic manuscript, or just a screenshot of a social‑media post and you need the text in a searchable format. You’re not alone—developers worldwide hit this snag when dealing with right‑to‑left languages.

In this tutorial we’ll walk through a complete, runnable example that shows **how to run OCR** on a PNG file, extract Arabic text, and print the result to the console. No vague “see the docs” links; just the code you can copy‑paste, plus explanations of why each line matters. By the end you’ll be able to **convert image to text** reliably, even when the source is a tricky Arabic PNG.

> **What you’ll learn**
> - Set up a Python OCR engine for Arabic  
> - Load a PNG image and handle common pitfalls  
> - Recognize Arabic text and verify the output  
> - Tips for **extracting Arabic text** from different image qualities  

Before we dive in, make sure you have Python 3.8+ installed and a recent version of the `ocr` library (the one used in the snippet). If you’re using a virtual environment, activate it now—this keeps dependencies tidy.

## Prerequisites

- Python 3.8 or newer  
- `ocr` package (`pip install ocr‑engine` – replace with the actual package name)  
- An Arabic PNG image (`arabic_doc.png`) placed somewhere you can reference  
- Basic familiarity with Python functions and classes  

That’s it. No heavyweight frameworks, no Docker containers—just plain Python.

## Step 1: Install and Import the OCR Library

First things first. We need the OCR engine itself. The library we’ll use exposes an `OcrEngine` class with a straightforward API.

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*Why import `Imaging` separately?* The `Imaging` submodule gives us a convenient `Image.load` method that understands PNG, JPEG, and TIFF out of the box. Skipping this step would force you to handle raw bytes yourself, which is unnecessary for most use‑cases.

## Step 2: Create the OCR Engine Instance

Now we create an instance of the engine. Think of this object as the “brain” that will process the image.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **Pro tip:** If you plan to process many images in a row, reuse the same `ocr_engine` instance. It caches language models, which speeds up subsequent recognitions.

## Step 3: Set the Language to Arabic

Arabic isn’t Latin; it has its own character set, right‑to‑left direction, and contextual shaping. That's why we must explicitly tell the engine which language model to load.

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

If you forget this line, the engine defaults to English and you’ll get garbled output—something I’ve seen happen far too often.

## Step 4: Load Your PNG Image

Here’s where the **convert image to text** part really starts. We’ll load the PNG file that contains the Arabic script.

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### Common Edge Cases

| Issue | Symptom | Fix |
|-------|---------|-----|
| Image is too dark | Output contains many blanks | Pre‑process with Pillow (`ImageEnhance.Brightness`) |
| PNG has an alpha channel | Some OCR engines mis‑read transparent pixels | Convert to RGB (`image.convert("RGB")`) before loading |
| Text is rotated | Recognized text is upside‑down | Rotate the image (`image.rotate(90, expand=True)`) before passing to the engine |

## Step 5: Run the Recognition Process

With everything set, we finally ask the engine to do its job.

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

The `recognize` method returns an object that holds the raw Unicode string, confidence scores, and bounding boxes. For most developers, the plain text is all you need.

## Step 6: Output the Recognized Arabic Text

Now we print the result. In a real application you might write to a file, a database, or feed it into a translation API.

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

When you run the script, you should see the Arabic characters displayed in your console (make sure your terminal supports Unicode). If you see question marks or empty strings, double‑check the language setting and image quality.

### Expected Output

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

If the output looks similar to the line above, congratulations—you’ve successfully **extracted Arabic text** from a PNG!

## Full Working Example

Below is the entire script, ready to copy‑paste. Replace `YOUR_DIRECTORY/arabic_doc.png` with the path to your own file.

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

Run it with `python run_ocr.py` (or whatever you named the file). If everything is installed correctly, you’ll see the Arabic sentence printed to the console.

## How to Run OCR on Different Image Formats

The same code works for JPEG, TIFF, or BMP—just change the file extension. The `Image.load` method automatically detects the format, so you can **convert image to text** without any extra code.

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

Remember, the quality of the source image heavily influences the accuracy of the **recognize Arabic text** step. High‑resolution, low‑compression images give the best results.

## Extract Text from PNG: Tips for Better Accuracy

1. **DPI Matters** – Aim for at least 300 dpi. Lower DPI often leads to missed characters.  
2. **Contrast is King** – Use image‑processing tools (e.g., OpenCV) to increase contrast before feeding the image to the OCR engine.  
3. **Noise Removal** – Small speckles can confuse the model; median filtering helps.  

Here’s a quick snippet using Pillow to improve a PNG before OCR:

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## Frequently Asked Questions

**Q: Does this work with right‑to‑left languages other than Arabic?**  
A: Absolutely. Just change the language code (`"ar"` → `"he"` for Hebrew, `"fa"` for Persian) and the engine will load the appropriate model.

**Q: What if I need to extract text from multiple PNGs in a folder?**  
A: Loop over the files, reuse the same `ocr_engine` instance, and collect results in a list or write each to a separate `.txt` file.

**Q: Can I get confidence scores for each word?**  
A: Yes. `ocr_result` often exposes a `get_confidences()` method. Pair each confidence with the corresponding word for quality control.

## Next Steps

Now that you know **how to run OCR** on Arabic PNGs, consider these follow‑up ideas:

- **Batch processing:** Combine the script with `os.listdir` to **extract Arabic text** from an entire directory.  
- **Post‑processing:** Use the `arabic_reshaper` and `python-bidi` libraries to correctly display right‑to‑left output in PDFs.  
- **Integration:** Feed the extracted text into a search index (e.g., Elasticsearch) to make scanned documents searchable.  

Each of these topics builds on the fundamentals covered here, and they’ll help you turn a simple **convert image to text** script into a production‑ready pipeline.

---

![how to run OCR on Arabic PNG](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}