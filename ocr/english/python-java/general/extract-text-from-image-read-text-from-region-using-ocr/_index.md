---
category: general
date: 2026-07-05
description: Extract text from image using Python OCR. Learn how to load image for
  OCR, read text from region, and extract text from invoice with a few lines of code.
draft: false
keywords:
- extract text from image
- read text from region
- load image for ocr
- extract text from invoice
- ocr on region
language: en
og_description: Extract text from image with Python OCR. This guide shows how to load
  image for OCR, read text from region, and extract text from invoice quickly.
og_title: Extract Text from Image – Read Text from Region Using OCR
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, read text from region, and extract text from invoice with a few lines of
    code.
  headline: Extract Text from Image – Read Text from Region Using OCR
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extract Text from Image – Read Text from Region Using OCR
url: /python-java/general/extract-text-from-image-read-text-from-region-using-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Image – Read Text from Region Using OCR

Ever needed to **extract text from image** but only a specific part matters—like the total amount on an invoice? You're not the only one. In many real‑world projects you’ll find yourself needing to **read text from region** rather than parsing the whole picture. Fortunately, with a few lines of Python you can load an image for OCR, define a region of interest (ROI), and pull out exactly the characters you need.

In this tutorial we’ll walk through a complete, runnable example that shows how to **load image for OCR**, set up an ROI, and finally **extract text from invoice**. By the end you’ll have a ready‑to‑drop snippet that works with any popular OCR library supporting region‑based recognition.

---

## What You’ll Need

- Python 3.8+ (the code works on 3.10 as well)  
- An OCR package that exposes an `OcrEngine` class (for the demo we’ll use a fictional `ocr` module; replace it with `pytesseract`, `easyocr`, or any library that offers ROI support)  
- A sample image—e.g., `invoice.png`—that contains clear, printed text  
- Basic familiarity with Python functions and classes (no deep learning background required)

If you already have these, great—let’s dive in. If not, grab the latest Python from python.org and install the OCR package via `pip install your-ocr-lib`.

---

![Extract text from image example](extract-text-from-image.png "Extract text from image – region based OCR demo")

*The picture above illustrates the region (red rectangle) we’ll target to **extract text from image**.*

---

## Step 1: Install and Import the OCR Library

First, make sure the OCR library is available in your environment. The import pattern below works for most packages that expose a high‑level `OcrEngine` class.

```python
# Install the library (uncomment if you haven't yet)
# pip install your-ocr-lib

import ocr  # replace `ocr` with the actual module name, e.g., `import easyocr`
```

> **Pro tip:** If you’re using `pytesseract`, you’ll need to install the Tesseract binary separately and set `pytesseract.pytesseract.tesseract_cmd` to its path.

---

## Step 2: Create the OCR Engine and Set Language

Creating the engine is straightforward, but specifying the language dramatically improves accuracy, especially for invoices that contain numbers and English words.

```python
# Initialise the OCR engine
ocr_engine = ocr.OcrEngine()

# Set the language to English – this is crucial for invoice text
ocr_engine.language = ocr.Language.ENGLISH
```

Why do we do this? The OCR engine uses language models to predict characters; telling it to expect English reduces false positives like misreading “0” as “O”.

---

## Step 3: Load Image for OCR

Now we actually **load image for OCR**. Most libraries accept a file path or a Pillow image object. Here we use the library’s built‑in loader for simplicity.

```python
# Load the source image that contains the text
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)   # replace with cv2.imread or PIL.Image.open if needed
```

Make sure the path points to the correct directory; a common mistake is forgetting the relative path when the script runs from a different working directory.

---

## Step 4: Define the Region of Interest (ROI)

Defining the ROI is the heart of **read text from region**. Think of it as drawing a rectangle around the part of the invoice that holds the total amount.

```python
# Define the ROI (left, top, width, height) in pixels
# Adjust these numbers to match your invoice layout
region_of_interest = ocr.Rectangle(100, 200, 400, 150)
```

- `left` and `top` represent the X and Y coordinates of the rectangle’s upper‑left corner.  
- `width` and `height` set the size of the box.  
- You can experiment with different values using an image viewer that shows pixel coordinates.

> **Why ROI matters:** Running OCR on the whole page wastes CPU cycles and often introduces noise from unrelated text, tables, or graphics. By focusing on a region, you get cleaner results and faster processing.

---

## Step 5: Perform OCR on the Specified Region

With everything set up, we finally **extract text from image**—but only within the ROI we defined.

```python
# Recognize text only within the defined ROI
ocr_result = ocr_engine.recognize(image, region_of_interest)
```

The `recognize` method returns an object that typically contains the raw string, confidence scores, and sometimes bounding boxes for each word. For our purposes we only need the plain text.

---

## Step 6: Output the Extracted Text

Let’s print the result and see what we got. This step demonstrates **extract text from invoice** in a real‑world scenario.

```python
# Output the extracted text
print("Text inside ROI:")
print(ocr_result.text)
```

### Expected Output

```
Text inside ROI:
Total Amount: $1,245.67
```

If your invoice uses a different layout, you’ll see whatever text lives inside the rectangle—perhaps an invoice number, date, or PO reference.

---

## Step 7: Wrap It All Into a Reusable Function (Optional)

To make the solution reusable across multiple invoices, encapsulate the logic into a function. This also illustrates **ocr on region** as a generic utility.

```python
def extract_text_from_region(image_path: str,
                             left: int,
                             top: int,
                             width: int,
                             height: int,
                             language: str = "ENGLISH") -> str:
    """
    Load an image, define a ROI, and return the OCR result as plain text.
    
    Parameters
    ----------
    image_path : str
        Path to the image file.
    left, top, width, height : int
        Coordinates defining the region of interest.
    language : str, optional
        Language code for the OCR engine (default is ENGLISH).
    
    Returns
    -------
    str
        Recognized text inside the ROI.
    """
    # Initialise engine
    engine = ocr.OcrEngine()
    engine.language = getattr(ocr.Language, language.upper(), ocr.Language.ENGLISH)

    # Load image
    img = ocr.Image.load(image_path)

    # Define ROI
    roi = ocr.Rectangle(left, top, width, height)

    # Recognise text
    result = engine.recognize(img, roi)

    return result.text.strip()
```

You can now call the function with any invoice:

```python
total_text = extract_text_from_region(
    "invoices/2024-03-15.png",
    left=100, top=200, width=400, height=150
)
print("Extracted total:", total_text)
```

---

## Common Pitfalls & How to Avoid Them

| Issue | Why it Happens | Fix |
|-------|----------------|-----|
| **Blank output** | ROI does not actually cover any text (wrong coordinates). | Double‑check pixel values with an image editor; add a visual debug overlay. |
| **Garbage characters** | Low image resolution or poor contrast. | Pre‑process the image: convert to grayscale, apply thresholding (`cv2.threshold`). |
| **Wrong language** | Engine defaults to a language without the needed character set. | Explicitly set `ocr_engine.language` to `ENGLISH` or the appropriate locale. |
| **Performance lag** | Running OCR on large images repeatedly. | Resize the image before loading, or only process the ROI by cropping first. |

---

## Extending the Example: Multiple ROIs

Sometimes an invoice contains several fields you need—like **extract text from invoice** for both total amount and invoice date. You can loop over a list of rectangles:

```python
fields = {
    "total": ocr.Rectangle(100, 200, 400, 150),
    "date":  ocr.Rectangle(500, 200, 200, 80)
}

for name, rect in fields.items():
    txt = ocr_engine.recognize(image, rect).text.strip()
    print(f"{name.title()} → {txt}")
```

This pattern keeps your code clean and makes it easy to add more regions later.

---

## Conclusion

We’ve just covered a complete, end‑to‑end workflow to **extract text from image** using Python OCR, focusing on a specific region. By **loading image for OCR**, defining a **region of interest**, and invoking the engine, you can reliably **read text from region**—perfect for pulling totals from invoices, dates from receipts, or any other localized data.  

Feel free to experiment


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}