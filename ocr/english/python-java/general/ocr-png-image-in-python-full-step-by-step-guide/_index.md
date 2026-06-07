---
category: general
date: 2026-06-06
description: OCR PNG image with Python – learn how to extract text from image, run
  a python OCR example and even read ancient greek text easily.
draft: false
keywords:
- ocr png image
- extract text from image
- python ocr example
- read ancient greek
- recognize image text
language: en
og_description: OCR PNG image in Python explained. This guide shows how to extract
  text from image, run a python OCR example and read ancient greek with ease.
og_title: OCR PNG Image in Python – Complete Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  headline: OCR PNG Image in Python – Full Step‑by‑Step Guide
  type: TechArticle
- description: OCR PNG image with Python – learn how to extract text from image, run
    a python OCR example and even read ancient greek text easily.
  name: OCR PNG Image in Python – Full Step‑by‑Step Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Modern syntax and type hints | | `pytesseract` package | Thin wrapper
      around the Tesseract engine | | Tesseract OCR binaries (≥ 5.0) | The actual
      engine that does the heavy lifting | | Greek language data (`grc.trained'
  - name: How do I improve accuracy on a noisy PNG?
    text: '- Convert the image to grayscale: `img = img.convert(''L'')` - Apply a
      binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, ''1'')`
      - Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`'
  - name: Can I process a whole folder of PNGs?
    text: Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`.
      Store each result in a dictionary or write to a CSV for later analysis.
  - name: What if I need to extract numbers only?
    text: 'Pass a custom **config** string to `image_to_string`:'
  - name: Is there a way to get confidence scores?
    text: Yes—use `pytesseract.image_to_data` which returns a TSV with confidence
      per word. You can filter out low‑confidence tokens before assembling the final
      string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR PNG Image in Python – Full Step‑by‑Step Guide
url: /python-java/general/ocr-png-image-in-python-full-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR PNG Image in Python – Full Step‑by‑Step Guide

Ever wondered how to **OCR PNG image** files straight from a Python script? Maybe you have a folder full of scanned ancient manuscripts and you need to **extract text from image** files without manually typing everything. The good news is you don’t need a PhD in computer vision—just a few lines of code and the right library, and you’ll be reading ancient greek in seconds.

In this tutorial we’ll walk through a **python OCR example** that recognises text from a PNG, sets the language to Greek polytonic, and prints the result. By the end you’ll know exactly how to **recognize image text**, handle common pitfalls, and adapt the script for other languages or image formats.

## What You’ll Learn

- Install and configure a Python OCR library (pytesseract + Tesseract OCR)
- Create an OCR engine instance and load a PNG file
- Set the recognition language to Greek polytonic so you can **read ancient greek**
- Output the recognised text and troubleshoot typical issues
- Extend the script to batch‑process multiple PNGs or switch to another language

### Prerequisites

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Modern syntax and type hints |
| `pytesseract` package | Thin wrapper around the Tesseract engine |
| Tesseract OCR binaries (≥ 5.0) | The actual engine that does the heavy lifting |
| Greek language data (`grc.traineddata`) | Needed for **read ancient greek** correctly |
| A PNG image you want to analyse (e.g., `ancient_greek.png`) | Our target for the **ocr png image** demo |

You can install the Python side with:

```bash
pip install pytesseract Pillow
```

And on Ubuntu/macOS you’d add the engine itself:

```bash
# Ubuntu
sudo apt-get install tesseract-ocr libtesseract-dev

# macOS (Homebrew)
brew install tesseract
```

Don’t forget to download the Greek polytonic trained data:

```bash
wget https://github.com/tesseract-ocr/tessdata/blob/main/greek.traineddata -P /usr/share/tesseract-ocr/4.00/tessdata/
```

*(Path may differ; adjust `TESSDATA_PREFIX` if needed.)*

---

## OCR PNG Image: Create the Engine Instance

The first thing we need is an object that talks to Tesseract. In `pytesseract` the engine is accessed through module‑level functions, but for clarity we’ll wrap it in a tiny class. This mirrors the “engine” concept you saw in the original snippet.

```python
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    """
    Simple wrapper around pytesseract to keep the API similar to the original example.
    """
    def __init__(self, tess_cmd: str = "tesseract"):
        # You can point pytesseract to a custom binary if you installed it somewhere unusual.
        pytesseract.pytesseract.tesseract_cmd = tess_cmd

    def set_recognition_language(self, language: str):
        """
        Store the language code for later calls.
        Example: 'grc' for Greek polytonic.
        """
        self.lang = language

    def recognize_image(self, image_path: str):
        """
        Open the PNG, run OCR, and return the raw result object.
        """
        img = Image.open(image_path)
        # pytesseract returns a string; we wrap it for consistency with the original code.
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text=text)

class OcrResult:
    """Container for OCR output – mimics the .text attribute used in the example."""
    def __init__(self, text: str):
        self.text = text
```

**Why wrap it?**  
- Keeps the public API identical to the snippet you started with, making migration painless.  
- Allows us to add logging or error handling later without touching the main flow.  
- Demonstrates good OOP practice—something senior developers appreciate.

---

## Extract Text from Image: Set the Language to Greek Polytonic

Now that we have an engine, we need to tell it which language to expect. Greek polytonic uses diacritics that aren’t covered by the standard “greek” data, so we point Tesseract at the `grc` trainedfile.

```python
# Step 2: Set the recognition language to Greek polytonic
engine = OcrEngine()
engine.set_recognition_language("grc")   # 'grc' is the ISO‑639‑2 code for ancient Greek
```

If you ever want to **extract text from image** files in another language, just replace `"grc"` with `"eng"` for English, `"fra"` for French, etc. The same line works for any language you have installed.

---

## Recognize Image Text: Run the OCR on a PNG

With the language set, we feed the PNG into the engine. The original example used a hard‑coded path; we’ll make it a little more flexible by using `Path` objects.

```python
# Step 3: Recognize text from the image file
image_path = Path("YOUR_DIRECTORY/ancient_greek.png")
ocr_result = engine.recognize_image(str(image_path))
```

**Tips & Edge Cases**

- **File not found** – wrap the call in a `try/except FileNotFoundError` to give a friendly message.
- **Low‑resolution PNG** – consider pre‑processing (e.g., resizing, binarization) with Pillow before OCR.  
- **Non‑Greek text** – Tesseract will still try to decode, but accuracy drops sharply. Always match the language.

---

## Output the Recognized Text

Finally, we print the result. In a real project you might write to a database, a CSV, or even feed it into a translation pipeline.

```python
# Step 4: Output the recognized text
print("=== OCR Result ===")
print(ocr_result.text)
```

When you run the script against a clear scan of an ancient Greek inscription, you should see something like:

```
=== OCR Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος...
```

If the output looks garbled, double‑check that the **greek.traineddata** file is in the right folder and that the PNG isn’t too noisy.

---

## Full Working Example (All Steps in One Script)

Below is the complete, ready‑to‑run program. Save it as `ocr_greek.py` and execute `python ocr_greek.py`.

```python
# ocr_greek.py
from pathlib import Path
from PIL import Image
import pytesseract

class OcrEngine:
    def __init__(self, tess_cmd: str = "tesseract"):
        pytesseract.pytesseract.tesseract_cmd = tess_cmd
        self.lang = "eng"  # default fallback

    def set_recognition_language(self, language: str):
        self.lang = language

    def recognize_image(self, image_path: str):
        img = Image.open(image_path)
        text = pytesseract.image_to_string(img, lang=self.lang)
        return OcrResult(text)

class OcrResult:
    def __init__(self, text: str):
        self.text = text

def main():
    # 1️⃣ Create an OCR engine instance
    engine = OcrEngine()

    # 2️⃣ Set the language to Greek polytonic (read ancient greek)
    engine.set_recognition_language("grc")

    # 3️⃣ Path to the PNG you want to analyse
    png_path = Path("YOUR_DIRECTORY/ancient_greek.png")
    if not png_path.is_file():
        raise FileNotFoundError(f"Cannot find image at {png_path}")

    # 4️⃣ Recognize and retrieve the text
    result = engine.recognize_image(str(png_path))

    # 5️⃣ Print the extracted text
    print("=== OCR PNG Image Result ===")
    print(result.text)

if __name__ == "__main__":
    main()
```

**Expected output** (truncated for brevity):

```
=== OCR PNG Image Result ===
Ἀνδρὸς ἐστὶν ὁ ἥλιος·
Καὶ ὁ ἥλιος ἀνατέλλει·
```

If you see the proper Greek characters, congratulations—you’ve successfully performed an **ocr png image** operation in Python!

---

## Common Questions & Pro Tips

### How do I improve accuracy on a noisy PNG?

- Convert the image to grayscale: `img = img.convert('L')`
- Apply a binary threshold: `img = img.point(lambda x: 0 if x < 128 else 255, '1')`
- Upscale with `img = img.resize((img.width*2, img.height*2), Image.LANCZOS)`

These steps often turn a **recognize image text** nightmare into a clean result.

### Can I process a whole folder of PNGs?

Absolutely. Wrap the `recognize_image` call in a `for` loop over `Path.glob("*.png")`. Store each result in a dictionary or write to a CSV for later analysis.

```python
for png in Path("my_folder").glob("*.png"):
    res = engine.recognize_image(str(png))
    print(f"{png.name}: {res.text[:50]}...")
```

### What if I need to extract numbers only?

Pass a custom **config** string to `image_to_string`:

```python
digits = pytesseract.image_to_string(img, lang=self.lang, config='outputbase digits')
```

That way you can **extract text from image** files that contain tables, serial numbers, or timestamps.

### Is there a way to get confidence scores?

Yes—use `pytesseract.image_to_data` which returns a TSV with confidence per word. You can filter out low‑confidence tokens before assembling the final string.

---

## Extending the Tutorial

Now that you’ve mastered the basics, consider exploring these related topics:

- **Batch OCR with multiprocessing** – speed up large corpora of PNGs.
- **Hybrid OCR + NLP pipelines** – automatically translate the extracted ancient Greek into modern English.
- **Alternative engines** – try `easyocr` or `opencv`‑based methods for specific use‑cases.
- **Cloud OCR services** – Google Vision, Azure Computer Vision, or AWS Textract for serverless scaling.

Each of these builds on the core **python ocr example** we just covered, so you’ll feel comfortable diving deeper.

---

## Conclusion

We’ve taken a simple snippet and turned it into a robust **ocr png image** workflow in Python. By creating an `OcrEngine`, setting the language to Greek polytonic, feeding a PNG, and printing the result, you now know how to **extract text from image** files, **recognize image text**, and even **read ancient greek


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}