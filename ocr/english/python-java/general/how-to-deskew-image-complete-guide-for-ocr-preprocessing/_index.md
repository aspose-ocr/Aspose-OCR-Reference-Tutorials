---
category: general
date: 2026-07-05
description: How to deskew image quickly. Learn to preprocess image for OCR, correct
  image rotation, and convert scan to text with Python.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from image
- convert scan to text
- correct image rotation
language: en
og_description: How to deskew image and preprocess image for OCR. This guide shows
  how to correct image rotation and extract text from image using Python.
og_title: How to Deskew Image – Step-by-Step OCR Preprocessing
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to deskew image quickly. Learn to preprocess image for OCR, correct
    image rotation, and convert scan to text with Python.
  headline: How to Deskew Image – Complete Guide for OCR Preprocessing
  type: TechArticle
tags:
- OCR
- image-processing
- Python
title: How to Deskew Image – Complete Guide for OCR Preprocessing
url: /python-java/general/how-to-deskew-image-complete-guide-for-ocr-preprocessing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Deskew Image – Complete Guide for OCR Preprocessing

Ever wondered **how to deskew image** files that look like they were taken from a crooked scanner?  You’re not the only one.  In many real‑world projects the first thing you have to do before you can **extract text from image** is straighten that wobble.  

In this tutorial we’ll walk through a hands‑on, end‑to‑end example that **preprocesses image for OCR**, fixes the rotation, and finally **converts scan to text** using a Python OCR library.  No vague references, just a working script you can copy‑paste, plus tips on common pitfalls.  

## What You’ll Achieve

By the end of this guide you will be able to:

* Load any scanned JPEG or PNG that’s slightly tilted.  
* Apply a deskew filter and a binarization step to boost OCR accuracy.  
* Run the OCR engine and **extract text from image** reliably.  
* Understand why **correct image rotation** matters for downstream text extraction.  

### Prerequisites

* Python 3.9+ installed on your machine.  
* A pip‑installable OCR package that mimics the `ocr` namespace used in the example (for instance, a thin wrapper around Tesseract).  
* Basic familiarity with Python functions and image processing concepts.  

If you’ve got those, let’s dive in.

![how to deskew image example](deskew_before_after.png){alt="how to deskew image – before and after correction"}

## Step 1: Set Up the OCR Engine – How to Deskew Image Using Python

First things first: you need an OCR engine that can understand the language of your document.  The snippet below shows the minimal boilerplate to create the engine and tell it you’re working with English text.

```python
import ocr  # Assume this is a wrapper around your OCR backend

# Create an OCR engine instance and set the language
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH
```

*Why this matters:*  The engine’s language setting influences the character set and dictionary it uses.  Skipping this step can cause the OCR to misinterpret common words, especially after you **correct image rotation**.

## Step 2: Load the Scanned Image You Want to Straighten

Now we bring the file into memory.  Replace `"YOUR_DIRECTORY/skewed_scan.jpg"` with the path to your own image.

```python
# Load the raw scanned image
raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")
```

If the image is already in a NumPy array or an OpenCV `Mat`, you can adapt the loader accordingly – the key is that the object must expose the `apply_filter` method used later.

## Step 3: Preprocess Image for OCR – Deskew and Binarize

Here’s where the magic happens.  We chain two filters:

1. **Deskew** – automatically detects the dominant text baseline and rotates the image back to horizontal.  
2. **Binarize (Otsu)** – converts the picture to pure black‑and‑white, which dramatically improves recognition rates.

```python
# Preprocess: deskew then binarize
preprocessed_image = (
    raw_image
    .apply_filter(ocr.Filter.deskew())          # <-- how to deskew image
    .apply_filter(ocr.Filter.binarize_otsu())  # improves OCR reliability
)
```

*Pro tip:*  If you notice the text still looks fuzzy after binarization, try tweaking the contrast or using a different thresholding method.  The `ocr.Filter` module often includes `adaptive_threshold()` for tougher cases.

## Step 4: Run OCR – Extract Text from Image

With a clean, straightened canvas, we hand the image to the engine.  The result object contains the recognized string, confidence scores, and even bounding boxes if you need them later.

```python
# Perform recognition on the preprocessed image
recognition_result = engine.recognize(preprocessed_image)

# Print the raw text output
print(recognition_result.text)
```

Typical output looks like:

```
Invoice #12345
Date: 2026-07-01
Total: $1,250.00
Thank you for your business!
```

Notice how the line breaks line up perfectly?  That’s the benefit of **correct image rotation** – the OCR no longer has to guess line orientation.

## Step 5: Put It All Together – A One‑File Script to Convert Scan to Text

Below is the full, runnable script that combines every piece we’ve discussed.  Save it as `deskew_ocr.py` and execute `python deskew_ocr.py`.

```python
#!/usr/bin/env python3
"""
Complete example: how to deskew image, preprocess it for OCR,
and extract text from a scanned document.
"""

import ocr  # Replace with your actual OCR library import

def main():
    # 1️⃣ Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # 2️⃣ Load the image (change path as needed)
    raw_image = ocr.Image.load("YOUR_DIRECTORY/skewed_scan.jpg")

    # 3️⃣ Preprocess – deskew then binarize
    preprocessed = (
        raw_image
        .apply_filter(ocr.Filter.deskew())          # how to deskew image
        .apply_filter(ocr.Filter.binarize_otsu())  # preprocess image for OCR
    )

    # 4️⃣ Recognize text
    result = engine.recognize(preprocessed)

    # 5️⃣ Output the extracted text
    print("=== Recognized Text ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

### Why This Works

* **Deskew first** – rotating the image before binarization ensures the threshold algorithm works on a level horizon.  
* **Binarize after deskew** – Otsu’s method assumes a bimodal histogram; a tilted page would ruin that assumption.  
* **English language model** – tells the OCR what characters to expect, reducing false positives.  

If you need to handle other languages, just swap `ocr.Language.ENGLISH` for the appropriate enum.

## Common Questions & Edge Cases

| Question | Answer |
|----------|--------|
| *What if the scan is upside‑down?* | The `deskew()` filter usually detects 180° rotation as well. If it fails, call `apply_filter(ocr.Filter.rotate(180))` before deskewing. |
| *My document has colored graphics – will binarization erase them?* | Yes. For mixed content, consider using `ocr.Filter.deskew()` alone, then run OCR on the color image. You can still extract text while preserving graphics. |
| *Can I process a batch of files?* | Wrap the logic in a loop, read each file path from a list, and store each `result.text` in a separate `.txt` file. |
| *How do I improve accuracy on low‑resolution scans?* | Upscale the image with a bicubic filter **before** deskewing, then apply a sharpening filter. More pixels give the OCR engine better clues. |

## Bonus: Visual Verification of Deskew

If you want to see the before‑and‑after side by side, add a quick Matplotlib snippet:

```python
import matplotlib.pyplot as plt

def show_comparison(original, processed):
    fig, axs = plt.subplots(1, 2, figsize=(10, 4))
    axs[0].imshow(original.to_numpy(), cmap='gray')
    axs[0].set_title('Original')
    axs[0].axis('off')

    axs[1].imshow(processed.to_numpy(), cmap='gray')
    axs[1].set_title('Deskewed & Binarized')
    axs[1].axis('off')
    plt.show()

show_comparison(raw_image, preprocessed)
```

Seeing the corrected alignment can be reassuring, especially when you’re debugging a tricky batch of scans.

## Conclusion

We’ve covered **how to deskew image** files, why **preprocess image for OCR** is essential, and how to **extract text from image** to finally **convert scan to text**.  The workflow—load → deskew → binarize → recognize—ensures the OCR sees a clean, straight page, which translates into higher accuracy and fewer manual corrections.

What’s next on your OCR journey?  Try experimenting with:

* Different language packs (`ocr.Language.FRENCH`, etc.).  
* Adding a layout analysis step to detect columns or tables.  
* Exporting the OCR results to searchable PDFs using a PDF library.

Feel free to drop a comment if you hit a snag, or share your own tweaks for handling especially stubborn scans.  Happy coding, and may your images always stay perfectly level!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}