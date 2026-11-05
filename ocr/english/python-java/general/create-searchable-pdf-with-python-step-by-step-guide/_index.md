---
category: general
date: 2026-05-31
description: Create searchable PDF from scanned images using Python OCR. Learn how
  to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- convert tiff to pdf
- how to run OCR
- add OCR text layer
language: en
og_description: Create searchable PDF instantly. This guide shows how to run OCR,
  convert scanned image PDF, and add OCR text layer using a single Python script.
og_title: Create Searchable PDF with Python – Complete Tutorial
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  headline: Create Searchable PDF with Python – Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from scanned images using Python OCR. Learn how
    to convert scanned image PDF, convert TIFF to PDF, and add OCR text layer in minutes.
  name: Create Searchable PDF with Python – Step‑by‑Step Guide
  steps:
  - name: Expected Output
    text: 'Running the script prints:'
  - name: 1️⃣ Can I process multi‑page PDFs?
    text: Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page
      with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will
      automatically generate a multi‑page searchable PDF.
  - name: 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?
    text: 'Higher DPI yields better OCR accuracy but also larger memory usage. If
      you hit a `MemoryError`, downscale the image first:'
  - name: 3️⃣ How do I change the language of the OCR?
    text: 'Set the `language` property on the engine before loading the image:'
  - name: 4️⃣ What if I need to keep the original image quality?
    text: The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None`
      to preserve the raster data exactly as it was.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Document Automation
title: Create Searchable PDF with Python – Step‑by‑Step Guide
url: /python-java/general/create-searchable-pdf-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Create Searchable PDF with Python – Step‑by‑Step Guide

Ever wondered how to **create searchable PDF** from a scanned page without juggling dozens of tools? You’re not alone. In many office workflows a scanned TIFF or JPEG lands on a shared drive, and the next person has to copy‑paste text manually—painful, error‑prone, and time‑wasting.  

In this tutorial we’ll walk through a clean, programmatic solution that lets you **convert scanned image PDF**, **convert TIFF to PDF**, and **add OCR text layer** in one go. By the end you’ll have a ready‑to‑use script that runs OCR, embeds the hidden text, and spits out a searchable PDF you can index, search, or share with confidence.

## What You’ll Need

- Python 3.9+ (any recent version works)
- `aspose-ocr` and `aspose-pdf` packages (installed via `pip install aspose-ocr aspose-pdf`)
- A scanned image file (`.tif`, `.png`, `.jpg`, or even a PDF page that’s just an image)
- A modest amount of RAM (the OCR engine is lightweight; even a laptop handles it)

> **Pro tip:** If you’re on Windows, the easiest way to get the packages is to run the command in an elevated PowerShell window.

```bash
pip install aspose-ocr aspose-pdf
```

Now that the prerequisites are out of the way, let’s dive into the code.

## Step 1: Create an OCR Engine Instance – *create searchable pdf*

The first thing we do is spin up the OCR engine. Think of it as the brain that will read every pixel and turn it into characters.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine – this is the core of the create searchable pdf process
ocr_engine = OcrEngine()
```

> **Why this matters:** Initializing the engine only once keeps memory usage low. If you were to call `OcrEngine()` inside a loop for each page, you’d quickly run out of resources.

## Step 2: Load the Scanned Image – *convert tiff to pdf* & *convert scanned image pdf*

Next, point the engine at the file you want to process. The API accepts any raster image, so a TIFF works just as well as a JPEG.

```python
# Load the image you want to OCR. Replace the path with your own file location.
ocr_engine.load_image("YOUR_DIRECTORY/scanned_page.tif")
```

If you happen to have a PDF that contains only a scanned image, you can still use `load_image` because Aspose will extract the first page automatically.

## Step 3: Prepare PDF Save Options – *add OCR text layer*

Here we configure how the final PDF should look. The crucial flag is `create_searchable_pdf`; setting it to `True` tells the library to embed an invisible text layer that mirrors the visual content.

```python
from aspose.pdf import PdfSaveOptions

pdf_save_options = PdfSaveOptions()
pdf_save_options.create_searchable_pdf = True   # embed OCR text layer
pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"
```

> **What the text layer does:** When you open the resulting file in Adobe Reader and try to select text, you’ll see the hidden characters. Search engines can index them, too—perfect for compliance or archiving.

## Step 4: Run OCR and Save – *how to run OCR* in a single call

Now the magic happens. One method call runs the recognition engine and writes the searchable PDF to disk.

```python
# Run OCR and generate the searchable PDF in one go
ocr_engine.recognize(pdf_save_options)

print("PDF saved as searchable PDF.")
```

The `recognize` method returns a status object you can inspect for errors, but for most straightforward scenarios the simple call above is sufficient.

### Expected Output

Running the script prints:

```
PDF saved as searchable PDF.
```

If you open `scanned_page_searchable.pdf` you’ll notice you can select text, copy‑paste it, and even run a `Ctrl+F` search. That’s the hallmark of a **create searchable pdf** workflow.

## Full Working Script

Below is the complete, ready‑to‑run script. Just replace the placeholder paths with your actual file locations.

```python
# ------------------------------------------------------------
# create_searchable_pdf.py – Convert scanned image to searchable PDF
# ------------------------------------------------------------

from aspose.ocr import OcrEngine
from aspose.pdf import PdfSaveOptions

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load image (TIFF, JPEG, PNG, or scanned PDF page)
    image_path = "YOUR_DIRECTORY/scanned_page.tif"
    ocr_engine.load_image(image_path)

    # 3️⃣ Configure PDF output – embed OCR text layer
    pdf_save_options = PdfSaveOptions()
    pdf_save_options.create_searchable_pdf = True
    pdf_save_options.output_path = "YOUR_DIRECTORY/scanned_page_searchable.pdf"

    # 4️⃣ Run OCR and write searchable PDF
    ocr_engine.recognize(pdf_save_options)

    print("PDF saved as searchable PDF.")

if __name__ == "__main__":
    main()
```

Save this as `create_searchable_pdf.py` and execute:

```bash
python create_searchable_pdf.py
```

## Common Questions & Edge Cases

### 1️⃣ Can I process multi‑page PDFs?

Yes. Use `ocr_engine.load_image("file.pdf")` and then loop over each page with `ocr_engine.recognize(pdf_save_options, page_number)`. The library will automatically generate a multi‑page searchable PDF.

### 2️⃣ What if my source file is a high‑resolution TIFF (300 dpi+)?

Higher DPI yields better OCR accuracy but also larger memory usage. If you hit a `MemoryError`, downscale the image first:

```python
from PIL import Image
img = Image.open(image_path)
img = img.resize((int(img.width * 0.5), int(img.height * 0.5)), Image.ANTIALIAS)
img.save("temp.tif")
ocr_engine.load_image("temp.tif")
```

### 3️⃣ How do I change the language of the OCR?

Set the `language` property on the engine before loading the image:

```python
ocr_engine.language = "fra"   # French
```

A full list of supported language codes lives in the Aspose documentation.

### 4️⃣ What if I need to keep the original image quality?

The `PdfSaveOptions` class has a `compression` property. Set it to `PdfCompression.None` to preserve the raster data exactly as it was.

```python
pdf_save_options.compression = "None"
```

## Tips for Production‑Ready Deployments

- **Batch processing:** Wrap the core logic in a function that accepts a list of file paths. Log each success/failure to a CSV for audit trails.
- **Parallelism:** Use `concurrent.futures.ThreadPoolExecutor` to run OCR on multiple cores. Just remember each thread needs its own `OcrEngine` instance.
- **Security:** If you’re handling sensitive documents, run the script in a sandboxed environment and delete the temporary files immediately after processing.

## Conclusion

You now know how to **create searchable PDF** files from scanned images using a concise Python script. By initializing an OCR engine, loading a TIFF (or any raster), configuring `PdfSaveOptions` to **add OCR text layer**, and finally calling `recognize`, the whole **convert scanned image pdf** and **convert TIFF to PDF** pipeline becomes a single, repeatable command.

Next steps? Try chaining this script with a file‑watcher so any new scan dropped into a folder automatically becomes searchable. Or experiment with different OCR languages to support multilingual archives. The sky’s the limit when you combine OCR with PDF generation.

Got more questions about **how to run OCR** in other languages or frameworks? Drop a comment below, and happy coding! 

![Diagram showing the flow from scanned image → OCR engine → searchable PDF (create searchable pdf)](searchable-pdf-flow.png "Create searchable pdf flow diagram")


## What Should You Learn Next?

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}