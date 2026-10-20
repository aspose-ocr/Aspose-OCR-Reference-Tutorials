---
category: general
date: 2026-03-28
description: Extract text from PNG quickly using Aspose OCR in Python. Learn to convert
  scanned pages text with parallel image recognition python for high‑performance results.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: en
og_description: Extract text from PNG quickly using Aspose OCR in Python. This guide
  shows how to convert scanned pages text with parallel image recognition python,
  delivering high‑speed results.
og_title: Extract Text from PNG – Fast Parallel OCR with Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Extract Text from PNG – Fast Parallel OCR with Python and Aspose
url: /python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from PNG – Fast Parallel OCR with Python

Ever needed to **extract text from PNG** files but found single‑threaded OCR painfully slow? You're not alone. Whether you're digitizing a stack of scanned receipts or turning lecture slides into searchable PDFs, the bottleneck is usually the OCR step itself.  

In this tutorial we’ll show you a complete, ready‑to‑run solution that **converts scanned pages text** in parallel, using Aspose OCR’s asynchronous batch mode together with Python’s `ThreadPoolExecutor`. By the end you’ll be able to **recognize image text python**‑style, handling dozens of images in a fraction of the time a naïve loop would take.

> **What you’ll walk away with**  
> * A fully functional script that extracts text from PNG images concurrently.  
> * Understanding of why async batch mode speeds things up.  
> * Tips for scaling the solution to larger workloads.

## What You’ll Need

| Prerequisite | Reason |
|--------------|--------|
| Python 3.9+ | Modern syntax and type hints. |
| `aspose-ocr` and `aspose-storage` packages | Provide the OCR engine and image loader. |
| A folder of PNG files (e.g., scanned pages) | The source material you want to process. |
| Basic knowledge of Python concurrency | Helpful but not mandatory; we’ll explain everything. |

You can install the Aspose libraries with:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** Keep your packages up to date (`pip list --outdated`) to benefit from the latest performance improvements.

## Step 1: Initialize the Aspose OCR Engine in Async Batch Mode

The first thing we do is create an `OcrEngine` instance and switch it to **asynchronous batch mode**. This mode queues recognition requests internally, allowing the engine to process multiple images without blocking your Python thread.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Why async?*  
When you call `recognize` in synchronous mode, the call blocks until the image is fully processed. In async mode, the engine can start working on the next image while the current one is still being decoded, effectively overlapping I/O and CPU work.

## Step 2: List the PNG Files You Want to Process

Here we define the collection of images. In a real project you might generate this list dynamically (e.g., `glob.glob("*.png")`), but keeping it explicit makes the example easy to follow.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Note:** Replace `YOUR_DIRECTORY` with the actual path where your PNG scans reside. If you have hundreds of files, consider using `os.listdir` and filtering for `.png`.

## Step 3: Write a Helper That Loads an Image and Returns Its Text

The helper abstracts the two‑step process of loading a file via **Aspose Storage** and then feeding it to the OCR engine. Adding a tiny docstring makes the function self‑documenting—helpful for future maintenance.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Why a separate function?*  
It keeps the thread‑pool code clean and lets us reuse the logic elsewhere (e.g., in a Flask endpoint). Also, isolating I/O makes debugging easier—if a particular file fails, you’ll see the filename in the exception trace.

## Step 4: Run Parallel Image Recognition Python with a Thread Pool

Now we bring in `ThreadPoolExecutor`. By default we spin up four workers, but you can tune `max_workers` based on your CPU cores and the size of the image set.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### How This Gives You Parallel Image Recognition Python

* **ThreadPoolExecutor** creates a pool of worker threads that each call `recognize_image`.  
* Because the OCR engine is in async batch mode, each thread can hand off work to the engine while still staying responsive.  
* `as_completed` yields futures in the order they finish, so you get results as soon as they’re ready—perfect for streaming large batches.

> **Common pitfall:** Using `max_workers=1` defeats the purpose of parallelism. On a 8‑core machine, `max_workers=8` often yields the best throughput, but test a few values to find the sweet spot for your hardware.

## Step 5: Verify the Output and Handle Edge Cases

When you run the script, you should see a block of text for each PNG, prefixed by its filename:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

If any image fails (corrupted file, unsupported format), the `except` block prints a helpful error message instead of crashing the whole batch.

### Extending the Solution

| Scenario | Suggested tweak |
|----------|-----------------|
| **Thousands of pages** | Switch to `ProcessPoolExecutor` to leverage multiple CPU processes, or chunk the list and process batches sequentially. |
| **Different image formats (JPG, TIFF)** | The `storage.Image.load` method auto‑detects format, so just add the files to `input_images`. |
| **Need to store results** | Write `text` to a `.txt` file or insert into a database inside the `else` block. |
| **Performance monitoring** | Wrap `recognize_image` with a timer (`time.perf_counter`) and log duration per file. |

## Full Working Example (Copy‑Paste Ready)

Below is the complete script, ready to drop into a file called `parallel_ocr.py`. No parts are missing—everything you need is right here.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Save the file, adjust the `YOUR_DIRECTORY` placeholder, and run:

```bash
python parallel_ocr.py
```

You should see the extracted text for each PNG appear in the console, just as shown earlier.

## Conclusion

We’ve just demonstrated how to **extract text from PNG** files efficiently by combining Aspose OCR’s async batch mode with Python’s `ThreadPoolExecutor`. The script converts scanned pages text in parallel, giving you a scalable way to **recognize image text python**‑style without writing a custom thread‑pool from scratch.  

If you’re ready to push this further, try:

* Storing results in a searchable SQLite database.  
* Adding image pre‑processing (deskew, denoise) with OpenCV before OCR.  
* Deploying the script as a microservice behind a Flask or FastAPI endpoint.

Remember, the key to high‑performance OCR isn’t just a faster engine—it’s also about feeding that engine work in a way that maximizes concurrency. With the pattern shown here, you can handle dozens or even hundreds of PNG scans with minimal code changes.

Happy coding, and may your PDFs always be searchable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}