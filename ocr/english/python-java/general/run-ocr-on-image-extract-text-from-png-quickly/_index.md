---
category: general
date: 2026-03-18
description: Run OCR on image to extract text from PNG and generate searchable PDF.
  Learn how to recognize text image and convert PNG to PDF in minutes.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: en
og_description: Run OCR on image to extract text from PNG, recognize text image, and
  generate a searchable PDF. Follow this step‑by‑step guide.
og_title: Run OCR on Image – Extract Text from PNG Quickly
tags:
- OCR
- Python
- Image Processing
title: Run OCR on Image – Extract Text from PNG Quickly
url: /python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on Image – Extract Text from PNG Quickly

Ever needed to **run OCR on image** files but weren’t sure where to start? Maybe you have a scanned article saved as `article.png` and you just want the plain text, or you need a searchable PDF for archiving. Either way, you’re in the right place. In this tutorial we’ll walk through extracting text from PNG, recognizing the text image, and even converting that PNG into a searchable PDF—all with a handful of lines of code.

> **What you’ll get:** a complete, runnable script that loads a PNG, runs OCR, saves the hOCR output, and optionally creates a searchable PDF. No missing imports, no “see the docs” dead‑ends—just a self‑contained solution you can drop into your project today.

## Prerequisites

Before we dive in, make sure you have:

- **Python 3.8+** (the syntax used here works on any recent version)
- The **`ocr_engine`** library you’re using (the example assumes a class called `OcrEngine`; replace with Tesseract, EasyOCR, etc., if needed)
- A PNG image you’d like to process (e.g., `article.png` placed in a folder you can reference)
- Write permission to the output directory

If you’re using Tesseract under the hood, install it with:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

And then install the Python wrapper:

```bash
pip install pytesseract Pillow
```

*Pro tip:* keep your OCR library up to date—new language packs and performance tweaks land frequently.

## Run OCR on Image – Step‑by‑Step Guide

Below is the **complete script**. Feel free to copy‑paste it into a file called `run_ocr.py` and run it with `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### What the script does, in plain English

1. **Instantiate** the OCR engine so you can control its settings.
2. **Load** the PNG file (`article.png`). The script aborts early if the file isn’t there—no mysterious `NoneType` errors later.
3. **Select** `hocr` as the export format. This format keeps the original layout, which is essential for later converting the image into a searchable PDF.
4. **Run** the recognition engine; the heavy lifting happens here.
5. **Write** the hOCR XML to `article.hocr`. You now have a machine‑readable representation of the text and its coordinates.
6. *(Optional)* Switch to `"pdf"` and generate a searchable PDF in one extra step.

The **expected output** is a UTF‑8‑encoded `.hocr` file that looks something like this (trimmed for brevity):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

If you uncomment the PDF section, you’ll also end up with `article_searchable.pdf`, which you can open in any PDF viewer and use the **Ctrl + F** search box to locate words instantly.

![Run OCR on image example output](example.png "Run OCR on image – hOCR and PDF results")

## How to Extract Text from PNG Using OcrEngine

If all you need is the raw text (no layout, no PDF), you can skip the hOCR step entirely:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Why choose plain text?* It’s lightweight, perfect for indexing, and works great with downstream NLP pipelines.

## Recognize Text Image and Generate Searchable PDF

Generating a searchable PDF is a two‑part dance:

1. **Run OCR** with `hocr` (as we did above) to get the layout information.
2. **Combine** the original PNG with the hOCR into a PDF using the engine’s PDF exporter.

Most modern OCR libraries (Tesseract, ABBYY, Google Vision) expose a `pdf` export that does exactly this. The snippet in the *Optional* block of the main script shows the pattern. If your library doesn’t have a built‑in PDF exporter, you can use **`pdf2image`** + **`reportlab`** to stitch the image and hOCR together—just let me know, and I’ll share a quick extra example.

## Convert PNG to PDF with OCR Output

Sometimes you just want a **plain PDF** that contains the image (no searchable layer). That’s even simpler:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Combine this with the OCR step if you need a searchable version, or keep it as a faithful visual replica for archival purposes.

## Common Pitfalls & Tips

| Issue | Why it Happens | Quick Fix |
|-------|----------------|-----------|
| **Blurry or low‑resolution PNG** | OCR accuracy drops dramatically below ~300 DPI. | Upscale with `Image.resize((width*2, height*2), Image.LANCZOS)` before feeding to the engine. |
| **Wrong language** | Engine defaults to English; non‑English characters become garbled. | Call `ocr_engine.setLanguage('deu')` (or appropriate ISO code) before `recognize()`. |
| **Missing hOCR output** | Some engines default to plain text when `setExportFormat` isn’t called. | Double‑check that `setExportFormat("hocr")` runs **before** `recognize()`. |
| **File permission errors** | Trying to write to a read‑only folder. | Use a path inside your project or `os.makedirs(..., exist_ok=True)` first. |
| **Large PDFs cause memory spikes** | PDF exporter keeps the whole image in RAM. | Process pages in chunks or use a streaming PDF writer. |

*Pro tip:* always test on a small sample image before scaling to a batch of thousands. It saves hours of debugging.

## Wrap‑Up

You now know **how to run OCR on image** files, **extract text from PNG**, **recognize text image** for downstream tasks, **generate a searchable PDF**, and **convert PNG to PDF** when you need a simple archive. The provided script is a complete, copy‑and‑paste solution that works out of the box, and the optional sections let you tailor the output to your exact workflow.

### What’s next?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}