---
category: general
date: 2026-01-12
description: How to batch OCR images quickly and extract text from JPEG files in Python.
  Learn step‑by‑step batch processing with a complete runnable example.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: en
og_description: How to batch OCR images and extract text from JPEG files. This guide
  walks you through a complete, ready‑to‑run Python solution.
og_title: How to Batch OCR Images – Quick Python Tutorial
tags:
- OCR
- Python
- image processing
title: How to Batch OCR Images – Fast Guide for Extracting Text from JPEG Files
url: /python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR Images – Fast Guide for Extracting Text from JPEG Files

Ever wondered **how to batch OCR images** without writing a separate script for each file? You’re not alone. In many projects—invoice scanning, archival digitisation, or content moderation—we need to pull text from dozens or hundreds of JPEG files in one go. The good news is that you can do it with just a few lines of Python, and you’ll have a reusable engine that you can drop into any pipeline.

In this tutorial we’ll show you exactly **how to batch OCR images**, then walk through extracting text from JPEG files, handling edge cases, and verifying the output. By the end you’ll have a self‑contained script that you can run against any folder of images, and you’ll understand why batch processing matters for performance and maintainability.

## What You’ll Learn

- Set up a simple OCR engine and configure it for English.
- Collect all JPEG files from a directory with `pathlib`.
- Call the OCR engine once to process the whole batch.
- Display a preview of the recognised text for each image.
- Tips for handling large batches, different languages, and common pitfalls.

**Prerequisites**: Python 3.8+, the `ocr` library (or any compatible wrapper), and a folder of JPEG images you want to analyse. No external services are required—everything runs locally.

---

## Step 1: Initialise the OCR Engine – The Core of How to Batch OCR Images

Before we can **batch OCR images**, we need an engine that knows how to read text. In most libraries you create an engine object, optionally set the language, and then reuse it for every file.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Why this matters*: Initialising the engine once avoids the overhead of loading language models repeatedly. It also gives you a single place to tweak settings (e.g., DPI, character whitelist) that will apply to the whole batch.

> **Pro tip**: If you plan to process multilingual documents, switch `ocr.Language.ENGLISH` to `ocr.Language.MULTI` or load multiple language packs before the batch starts.

---

## Step 2: Gather All JPEG Files – The “Extract Text from JPEG Files” Part

Now that the engine is ready, we need to tell it which images to work on. Using `pathlib` makes the code platform‑independent and concise.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Why this matters*: By collecting the file list first, we can feed the whole collection to the OCR engine in one call—exactly what “how to batch OCR images” is all about. If you have sub‑folders, you can change `glob("**/*.jpg")` to search recursively.

> **Edge case**: If your images have mixed extensions (`.jpeg`, `.JPG`), extend the glob pattern: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

---

## Step 3: Process the Whole Batch in One Call – The Real Power of Batch OCR

Most modern OCR libraries expose a `process_batch` (or similarly named) method that accepts an iterable of file paths. This is the heart of **how to batch OCR images** efficiently.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Why this matters*: A single batch call reduces the number of Python‑to‑C transitions, keeps the language model loaded in memory, and often enables internal parallelisation. The result is a list of objects—each containing the recognised text and confidence scores.

> **Performance note**: For very large batches (thousands of images), consider splitting the list into smaller chunks (e.g., 200 files) to avoid excessive memory consumption.

---

## Step 4: Show a Preview of the Extracted Text – Quick Validation

After the batch finishes, it’s useful to peek at the first few characters of each result. This helps you confirm that the OCR is actually extracting text from your JPEG files.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Why this matters*: A short preview lets you spot obvious failures (e.g., blank output, garbled characters) without opening every file. If you notice systematic issues, you can adjust engine settings and rerun the batch.

> **Common pitfall**: Forgetting to strip newline characters can make the preview look messy. The `replace("\n", " ")` line cleans it up.

---

## Full Working Example – All Steps Combined

Below is the complete script that you can copy‑paste, adjust the directory path, and run. It demonstrates the entire **how to batch OCR images** workflow from start to finish.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Expected output** (sample):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

If the preview shows meaningful text, you’ve successfully **extracted text from JPEG files** using a batch approach.

---

## Handling Large Batches and Advanced Scenarios

### Chunking Large Workloads
When dealing with thousands of images, memory can become a bottleneck. Split the list into smaller chunks:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Switching Languages
If your documents contain French or Spanish, change the language before the batch:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Saving Results to Disk
Instead of printing, you might want to write each OCR result to a `.txt` file:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

---

## Conclusion

You now know **how to batch OCR images** and reliably **extract text from JPEG files** using a compact Python script. By initialising the engine once, gathering all JPEG paths, processing them in a single batch, and previewing the output, you achieve both speed and simplicity. From here you can expand the workflow—add multilingual support, store results in a database, or integrate the script into a larger document‑processing pipeline.

Ready for the next step? Try swapping the `ocr` library for Tesseract, experiment with different image pre‑processing (thresholding, resizing), or feed the extracted text into a natural‑language‑processing model for automatic categorisation. The sky’s the limit, and you’ve got a solid foundation to build on.

Happy coding, and may your OCR batches always be error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}