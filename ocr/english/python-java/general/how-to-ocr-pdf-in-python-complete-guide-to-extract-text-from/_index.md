---
category: general
date: 2026-06-22
description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
  PDF to text using a stream‑based approach. Simple steps for processing scanned PDF.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: en
og_description: How to OCR PDF files in Python? Follow this guide to extract text
  from PDF, convert PDF to text, and process scanned PDF using a stream.
og_title: How to OCR PDF in Python – Step‑by‑Step Guide
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
url: /python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to OCR PDF in Python – Complete Guide to Extract Text from PDFs

Ever wondered **how to OCR PDF** files without wrestling with heavyweight desktop tools? You're not the only one. In many real‑world projects—think invoice automation or digitizing archival scans—you need a reliable way to turn a scanned PDF into searchable, editable text.

In this tutorial we’ll walk through a clean, end‑to‑end example that **extracts text from PDF** pages using a lightweight Python OCR engine. By the end you’ll know exactly how to **convert PDF to text**, how to **load PDF from stream**, and how to **process scanned PDF** efficiently. No magic, just plain Python code you can drop into your project today.

## What You’ll Learn

- Install and configure a Python OCR library that understands PDF input.  
- Enable PDF‑recognition mode and set the output format to plain text.  
- Load a multi‑page PDF from a file stream (the classic “load pdf from stream” pattern).  
- Run OCR across all pages and retrieve the textual content.  
- Print or store the results for downstream processing.

**Prerequisites**  
- Python 3.8+ installed on your machine.  
- Basic familiarity with pip and virtual environments.  
- A scanned PDF file (named `multipage.pdf` in the example) placed in a known directory.

If any of those sound unfamiliar, don’t worry—each step is explained in plain language, and we’ll provide the exact commands you need.

---

## Step 1: Install the OCR Engine (how to OCR PDF)

First things first—you need an OCR engine that can handle PDF input. For this guide we’ll use the hypothetical `ocr` package (the API mirrors popular commercial SDKs, but the same pattern works with Tesseract‑OCR, ABBYY, or Google Vision when wrapped appropriately).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** If you’re on Windows and hit permission errors, try `pip install --user ocr` instead.

Once the package is installed, you can import it in your script and spin up an engine instance—this is the heart of **how to OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

The `OcrEngine` object holds all the settings we’ll tweak later, such as language, DPI, and—crucially—PDF mode.

---

## Step 2: Enable PDF Recognition and Choose Output (extract text from PDF)

By default many OCR SDKs assume you’re feeding them images. To make the engine treat the incoming stream as a PDF, we enable the PDF recognition flag and ask for plain‑text output.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Why bother specifying the output format? Because some engines can return PDF with hidden text layers, searchable PDFs, or JSON with bounding boxes. For most data‑extraction pipelines, **extract text from PDF** as plain strings is the cleanest downstream format.

---

## Step 3: Load the PDF from a File Stream (load PDF from stream)

Loading a PDF from a stream is a memory‑efficient pattern—you avoid loading the whole file into RAM at once. This is especially handy when dealing with large multi‑page documents.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **What if the file is on S3 or another cloud bucket?**  
> Simply replace `from_file` with a method that accepts a byte buffer (e.g., `ImageStream.from_bytes(s3_object.read())`). The rest of the pipeline stays identical.

---

## Step 4: Run OCR on All Pages (process scanned PDF)

Now the heavy lifting begins. The engine will iterate through every page, run the recognition engine, and return a list of page objects—each exposing its textual content.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Behind the scenes, the OCR library decompresses each PDF page, rasterizes it at the configured DPI, and feeds the bitmap through its neural‑network model. The result? A collection of `Page` objects ready for extraction.

---

## Step 5: Retrieve and Display the Recognized Text (convert PDF to text)

Finally, we loop over the returned pages and print the recognized text. This is the moment where **convert PDF to text** truly happens.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Expected Output

If `multipage.pdf` contains three scanned pages, you’ll see something like:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Notice the clean separation between pages—useful if you need to store each page’s text in a database or feed it to a downstream NLP model.

---

## Handling Common Edge Cases

### 1. PDFs with Mixed Image and Text Layers
Some PDFs already contain a hidden text layer (e.g., exported from Word). If you want the OCR engine to **ignore existing text** and re‑process the image, set:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Large Files Exceeding Memory Limits
When working with gigabyte‑size PDFs, consider processing in chunks:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Language and Font Support
If your scanned documents are in French or contain special characters, tell the engine which language model to use:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

---

## Full Script – Ready to Run

Below is the complete, runnable example that ties all the pieces together. Save it as `ocr_pdf.py` and execute `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Running the script** will print each page’s text to the console, exactly as shown in the “Expected Output” section. From here you can redirect the output to a file:

```bash
python ocr_pdf.py > extracted_text.txt
```

---

## Conclusion

We’ve just covered **how to OCR PDF** files in Python from start to finish. By configuring the engine, loading the document via a stream, and iterating over each recognized page, you can **extract text from PDF**, **convert PDF to text**, and **process scanned PDF** with just a handful of lines. The approach scales from tiny two‑page invoices to massive multi‑hundred‑page archives.

What’s next? Try feeding the extracted strings into a search index, a language‑model summarizer, or a data‑validation pipeline. You might also experiment with output formats like JSON to retain positional metadata for advanced document analysis.

Got questions about handling encrypted PDFs or integrating with cloud storage? Drop a comment below—happy coding! 

![Diagram showing the OCR PDF workflow – how to OCR PDF, load PDF from stream, recognize pages, and extract text](ocr-pdf-workflow.png "how to OCR PDF workflow diagram")


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}