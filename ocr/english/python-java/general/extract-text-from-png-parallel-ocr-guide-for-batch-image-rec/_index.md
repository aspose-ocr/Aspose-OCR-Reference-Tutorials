---
category: general
date: 2026-03-18
description: Extract text from PNG using Python and Aspose OCR. Learn how to load
  image for OCR, run ocr multiple files, and achieve batch OCR images with parallel
  image recognition.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: en
og_description: Extract text from PNG with Aspose OCR in Python. This tutorial shows
  how to load image for OCR, process ocr multiple files, and run batch OCR images
  using parallel image recognition.
og_title: Extract text from PNG – Parallel OCR Guide
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Extract text from PNG – Parallel OCR Guide for Batch Image Recognition
url: /python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract text from PNG – Parallel OCR Guide for Batch Image Recognition

Ever needed to **extract text from PNG** files but felt stuck at the point where a single image takes forever to process? You're not alone. In many real‑world projects—think invoice scanners, receipt digitizers, or archival tools—speed matters, and processing each PNG one‑by‑one just won’t cut it.  

In this guide we’ll walk through a complete, ready‑to‑run solution that **loads image for OCR**, runs **ocr multiple files** in a **batch OCR images** fashion, and leverages **parallel image recognition** with Python’s `threading` module. By the end you’ll have a script that pulls text from any number of PNGs in seconds, not minutes.

## What You’ll Need

- Python 3.8 or newer (the syntax shown works on 3.10+ as well).  
- The Aspose OCR for Java/​Python package (`aspose-ocr`). You can install it via `pip`.  
- A folder with a handful of PNG files you want to process.  
- A modest amount of RAM—each thread holds a tiny OCR engine instance, so even a laptop can spin up dozens of workers.

No external services, no cloud keys, and no mysterious configuration files. Just pure Python code you can copy‑paste and run.

## Why extract text from PNG in parallel?

Processing a PNG is CPU‑bound: the OCR engine runs a series of image‑analysis algorithms that chew through pixel data. When you have ten, twenty, or a hundred images, the total runtime is essentially the sum of each individual run.  

By spawning a thread for every file, we let the operating system schedule those CPU‑heavy jobs concurrently. On a multi‑core machine this often halves—or even quarters—the wall‑clock time. The trade‑off is a slightly higher memory footprint, but for most batch jobs the gain in speed is well worth it.

> **Pro tip:** If you’re dealing with hundreds of megabytes of images, consider using `concurrent.futures.ProcessPoolExecutor` instead of `threading`. Processes give you true parallelism on the GIL‑bound CPython interpreter, at the cost of a bit more overhead.

## Step 1: Install Aspose OCR for Python

First things first—let’s get the OCR library onto your system.

```bash
pip install aspose-ocr
```

That single line pulls the latest Aspose OCR binaries and its Python bindings. If you hit a permission error, try adding `--user` or using a virtual environment.

## Step 2: Load image for OCR – the worker function

Now we define the core routine that will be executed in each thread. It **loads image for OCR**, runs the recognition, and prints a preview of the extracted text.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

A few things to note:

- **Why a new `OcrEngine` per thread?** The engine holds internal buffers; sharing one instance would cause race conditions and garbled output.  
- **Why strip newlines?** When we log to the console it keeps the line tidy.  
- **Error handling?** In production you’d wrap the body in a `try/except` and maybe log to a file—something we’ll cover later.

## Step 3: List the PNG files you want to process

You could hard‑code the list, but a more flexible approach is to scan a directory. Below we manually list three files for clarity; replace the paths with your own folder.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

If you prefer an automatic discovery:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

That small tweak lets you **extract text from PNG** files in bulk without touching the source code each time.

## Step 4: Set up ocr multiple files with batch OCR images

We now create a thread for every image. This is the heart of the **batch OCR images** pattern.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

The list comprehension keeps the code concise, and each `Thread` object stores the target function and its argument (`image_path`).  

> **Side note:** Python’s `threading` module uses native OS threads, so on a 4‑core laptop you’ll typically see up to four threads truly running at once; the rest will be scheduled as cores become free.

## Step 5: Run parallel image recognition

Launching the workers is straightforward: iterate over the list and call `start()`. After that we wait for every thread to finish using `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

When the script finishes, you’ll see a series of lines like:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

That output confirms each PNG was processed and the extracted text is available for further handling (e.g., saving to a database or feeding into a NLP pipeline).

## Step 6: Verify the results and handle edge cases

### Checking for empty results

Sometimes an image is too noisy, or the OCR engine fails to detect any characters. A quick sanity check can save you from downstream errors.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Limiting the number of concurrent threads

If you run this on a modest VM, spawning hundreds of threads might overwhelm the scheduler. You can cap concurrency with a semaphore:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Saving results to a file

Instead of printing, you might want a CSV with the filename and extracted text:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Make sure to open the CSV **once** outside the thread function to avoid race conditions; the `csv` module’s writer is thread‑safe for simple writes.

## Full Working Example

Putting everything together, here’s a single script you can drop into a file called `batch_ocr.py` and run:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}