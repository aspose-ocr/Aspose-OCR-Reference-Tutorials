---
category: general
date: 2026-03-26
description: how to batch ocr efficiently using Python—learn extract text from images
  and pdf ocr conversion with parallel processing.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: en
og_description: how to batch ocr efficiently—step‑by‑step guide for extract text from
  images, pdf ocr conversion and batch ocr processing using Python.
og_title: 'how to batch ocr: fast parallel text extraction'
tags:
- OCR
- Python
- Parallel Computing
title: 'how to batch ocr: fast parallel text extraction'
url: /python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to batch ocr: fast parallel text extraction

Ever wondered **how to batch ocr** when you have dozens of scanned pages, screenshots, and PDFs lying around? You're not the only one—most developers hit the same wall: processing each file one‑by‑one becomes a painful bottleneck.  

The good news is that you can spin up a handful of worker threads, feed them all your files, and watch the OCR engine chew through the batch in parallel. In this tutorial we’ll walk through a complete, ready‑to‑run example that shows **extract text from images**, perform **pdf ocr conversion**, and leverage **parallel ocr processing** for speed.

> **What you’ll walk away with**  
> * A fully functional Python script that processes a mixed list of PNG, TIFF, PDF, and JPG files in one go.  
> * Understanding of why a thread pool speeds up I/O‑bound OCR tasks.  
> * Tips for handling errors, large PDFs, and custom thread counts.  

## Prerequisites

Before we dive, make sure you have:

| Requirement | Reason |
|-------------|--------|
| Python 3.8+ | Modern syntax & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Provides `OcrBatchProcessor` and result objects |
| A handful of sample files (PNG, TIFF, PDF, JPG) | To see the **extract text from images** in action |
| Basic familiarity with threads (optional) | Helpful but not mandatory |

If you haven’t installed the `ocr` package yet, run:

```bash
pip install ocr-lib   # replace with the actual package name
```

Now that the environment is ready, let’s break the problem down.

## Step 1: Import helpers and instantiate the batch processor

The first thing we need is a place to collect all the OCR jobs. The `OcrBatchProcessor` class does exactly that—it queues work items and hands you back a list of `Future` objects.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: Importing `as_completed` lets us react to each finished job instantly, rather than waiting for the slowest file. This is the core of **batch ocr processing**.

## Step 2: Tune the worker pool for parallel execution

By default the processor might use a single thread, which defeats the purpose of batching. We explicitly ask for four workers—feel free to bump this number up to the number of CPU cores you have.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: For I/O‑bound tasks like OCR, you often get diminishing returns after `CPU cores * 2`. Test a few values and pick the sweet spot.

## Step 3: Queue every file you want to OCR

Here we add a mixed bag of image and PDF files. The `add` method simply records the path; the actual work won’t start until we submit the batch.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

If you need to process a whole folder, a quick `glob` loop does the trick:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Step 4: Fire off the jobs and collect futures

Calling `submit_all` hands the processor the green light. It returns a list of `Future` objects—think of them as placeholders for results that will appear later.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

At this point the OCR engine is busy in the background, each thread munching on a file.

## Step 5: Pull results as soon as they finish

Using `as_completed` we iterate over futures in the order they finish, not the order we submitted them. This keeps our script responsive, especially when some PDFs take longer than simple PNGs.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (truncated for brevity):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Each block corresponds to the plain‑text representation of the original file. If you’re doing **pdf ocr conversion**, the text will include everything the OCR engine could decipher from each page.

## Handling Edge Cases & Common Pitfalls

| Situation | What to watch for | Quick fix |
|-----------|-------------------|-----------|
| A corrupted image | `future.result()` raises `OSError` | Wrap in `try/except` (see code above) |
| Very large PDFs ( > 100 MB ) | Memory pressure, slower threads | Increase `thread_count` modestly or split PDF into chapters first |
| Mixed language documents | Default OCR model may mis‑detect | Pass language hints to `OcrBatchProcessor` if the library supports it |
| Need to preserve layout | Plain `get_text()` loses columns | Use `ocr_result.get_hocr()` or similar layout‑aware method |

### Pro tip: Custom thread count based on file type

If you know most of your workload is PDFs, you might allocate more threads for those and fewer for tiny PNGs. Some libraries let you pass a per‑job `priority`; otherwise, you can create two separate batches—one for images, one for PDFs—and run them concurrently.

## Visual Overview (optional)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*The diagram illustrates the flow from file discovery → batch creation → parallel execution → result aggregation.*

## Full Script You Can Copy‑Paste

Below is the entire program, ready to drop into a `.py` file. It includes all the snippets above, plus a tiny helper that automatically discovers supported files in a directory.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Save this as `batch_ocr.py`, point it at a folder containing your scans, and watch the console fill with extracted text.  

### Why this works

* **Thread pool** – OCR is mostly waiting on disk I/O and external engine calls, so multiple threads keep the CPU busy.  
* **`as_completed`** – You get results as soon as they’re ready, which is ideal for UI feedback or streaming pipelines.  
* **Error isolation** – One bad file won’t bring the whole batch down; the `try/except` block isolates failures.

## Conclusion

In a nutshell, you now know **how to batch ocr** using Python’s `concurrent.futures` together with an OCR library that supports batch processing. By configuring a modest thread pool, queuing every supported file, and pulling results as they finish, you achieve fast **parallel ocr processing** without sacrificing reliability.  

From here you could:

* Hook the output into a search index for quick document retrieval.  
* Extend the script to write each result to a `.txt` file alongside the original.  
* Replace the built‑in thread pool with `asyncio` if your OCR library offers async APIs.  

Keep experimenting—swap in Tesseract, Azure Cognitive Services, or Google Vision, and you’ll see the same pattern apply. Happy OCR-ing!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}