---
category: general
date: 2026-04-26
description: How to batch OCR your documents and extract text from scans in Python.
  Learn step‑by‑step batch processing with OcrEngine for JSON output.
draft: false
keywords:
- how to batch OCR
- extract text from scans
- OCR batch processing
- Python OCR automation
- JSON OCR output
language: en
og_description: How to batch OCR your scanned files and extract text from scans in
  a single script. Complete code, tips, and edge‑case handling.
og_title: How to Batch OCR – Fast Python Guide
tags:
- OCR
- Python
- Automation
title: How to Batch OCR – Extract Text from Scans Efficiently
url: /python-java/general/how-to-batch-ocr-extract-text-from-scans-efficiently/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# How to Batch OCR – Extract Text from Scans Efficiently

Ever wondered **how to batch OCR** a mountain of scanned PDFs without losing your sanity? You’re not the only one—developers constantly ask, *“How can I extract text from scans in one go?”* The good news is that a few lines of Python can turn that tedious chore into a smooth, automated pipeline.

In this tutorial we’ll walk through a complete, ready‑to‑run solution that **extracts text from scans**, saves the results as JSON, and gives you a quick sanity check at the end. No external services, no magic—just plain Python, the `OcrEngine` class, and a bit of folder plumbing.

## What You’ll Walk Away With

- A fully functional script that **batches OCR** over any folder of images.
- Clear explanations of *why* each line exists, not just *what* it does.
- Tips for handling empty folders, non‑image files, and large batches.
- A way to verify that the JSON output actually contains the extracted text.

### Prerequisites (the bare minimum)

| Requirement | Why it matters |
|-------------|----------------|
| Python 3.8+ | Modern syntax & type hints |
| `OcrEngine` library (or a compatible wrapper) | Core OCR functionality |
| A directory with scanned image files (PNG, JPG, TIFF) | Input data |
| Write permissions for the output folder | Saving JSON results |

If you already have these, great—let’s dive in.

![how to batch OCR workflow](image-placeholder.png){alt="how to batch OCR workflow"}

## Step 1 – Initialize the OCR Engine (how to batch OCR)

Before we can process anything, we need an OCR engine instance. Think of it as the “brain” that will read each image and spit out text. Initializing it once and re‑using it across the whole batch is the most efficient pattern.

```python
# Step 1: Create an OCR engine instance
# The OcrEngine class abstracts the low‑level OCR library (Tesseract, EasyOCR, etc.)
ocr_engine = OcrEngine()
```

> **Why reuse the same instance?**  
> Creating a new engine for every file would repeatedly load heavy models into memory, dramatically slowing down the batch. One instance keeps the model in RAM and lets you process thousands of images without a noticeable slowdown.

## Step 2 – Point to Your Scans Folder (extract text from scans)

Your scans live somewhere on disk. Let’s tell the script where to find them. Using absolute paths avoids “file not found” surprises when the script is launched from a different working directory.

```python
import os

# Step 2: Specify the folder that contains scanned images
# Replace YOUR_DIRECTORY with the actual base path on your machine.
input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
```

> **Pro tip:**  
> If you’re on Windows, forward slashes (`/`) work just fine with `os.path.abspath`, so you don’t have to escape backslashes.

## Step 3 – Choose Where the JSON Results Should Go

You probably want a tidy folder for the OCR results. Keeping output separate from the source makes it easy to clean up later or feed the JSON into another pipeline.

```python
# Step 3: Specify where the JSON results should be saved
output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
os.makedirs(output_dir, exist_ok=True)   # Ensure the folder exists
```

> **Why create the folder programmatically?**  
> It guarantees the script won’t crash if the directory is missing, and `exist_ok=True` makes the operation idempotent—run the script multiple times without errors.

## Step 4 – Run the Batch Process (how to batch OCR)

Now the heart of the matter: telling `ocr_engine` to walk through every file in `input_dir`, run OCR, and dump JSON into `output_dir`. The `format="json"` flag tells the engine to serialize the result in a structured way that downstream tools love.

```python
# Step 4: Run batch processing to convert all scans to JSON format
ocr_engine.batch_process(
    input_folder=input_dir,
    output_folder=output_dir,
    format="json"
)
```

### What’s happening under the hood?

1. **File discovery** – The engine scans `input_folder` recursively, ignoring hidden files.
2. **File validation** – Only supported image extensions (`.png`, `.jpg`, `.tif`, etc.) are fed to the OCR model.
3. **OCR execution** – Each image is sent to the OCR engine; text, confidence scores, and layout data are captured.
4. **JSON serialization** – The result is written to a file with the same base name but a `.json` extension in `output_folder`.

> **Edge case handling:**  
> - **Empty folder:** The engine logs “No files found” and returns gracefully.  
> - **Corrupt image:** It skips the file, records an error entry in a `batch_errors.log`, and continues.  
> - **Huge batch (10k+ files):** Memory usage stays low because each image is processed independently.

## Step 5 – Confirm the Conversion Finished

A simple `print` statement gives immediate feedback in the console. For production pipelines you might replace this with a logging call or an email notification.

```python
# Step 5: Inform the user that the batch conversion has finished
print("Batch conversion complete.")
```

When you see that line, you can safely inspect the `json_output` folder. Each JSON file will look roughly like this:

```json
{
  "file_name": "invoice_001.png",
  "text": "Invoice #001\nDate: 2024‑12‑01\nTotal: $1,234.56",
  "confidence": 0.97,
  "layout": [
    {"line": 1, "bbox": [10, 20, 200, 40]},
    {"line": 2, "bbox": [10, 50, 180, 70]},
    {"line": 3, "bbox": [10, 80, 150, 100]}
  ]
}
```

You can now feed these JSON files into a database, a search index, or any downstream analytics tool.

## Frequently Asked Questions (and quick answers)

**Q: What if I need to process PDFs instead of images?**  
A: Convert each PDF page to an image first (e.g., using `pdf2image`) and place the resulting PNG/JPG files in `input_dir`. The batch OCR logic stays unchanged.

**Q: Can I change the output format to plain text?**  
A: Absolutely. Replace `format="json"` with `format="txt"` and the engine will write a `.txt` file containing only the extracted text.

**Q: My scans are in multiple sub‑folders—will the script recurse?**  
A: Yes. `batch_process` walks the directory tree by default. If you want a flat output, set `flatten=True` (if the library supports it) or post‑process the JSON filenames.

**Q: How do I handle non‑Latin scripts?**  
A: Initialise `OcrEngine` with a language parameter, e.g., `OcrEngine(lang="spa+eng")`. The batch loop itself doesn’t need any changes.

## Pro Tips & Common Pitfalls

- **Batch size matters:** If you notice CPU spikes, throttle the process with a simple `time.sleep(0.1)` between files.
- **Logging:** Swap the `print` call for Python’s `logging` module to capture timestamps and error levels.
- **File naming collisions:** If two scans share the same base name but reside in different sub‑folders, the JSON files will overwrite each other. Append a hash of the relative path to the output name to avoid this.
- **Memory leaks:** Some OCR back‑ends hold onto native resources. Call `ocr_engine.close()` at the end of your script if the library provides a cleanup method.

## Full Script – Ready to Copy & Paste

```python
import os
from ocr_engine import OcrEngine   # Replace with the actual import path

def main():
    # Step 1: Initialize the OCR engine (how to batch OCR)
    ocr_engine = OcrEngine()

    # Step 2: Directory with scanned images (extract text from scans)
    input_dir = os.path.abspath("YOUR_DIRECTORY/scans/")
    if not os.path.isdir(input_dir):
        raise FileNotFoundError(f"Input folder not found: {input_dir}")

    # Step 3: Destination for JSON results
    output_dir = os.path.abspath("YOUR_DIRECTORY/json_output/")
    os.makedirs(output_dir, exist_ok=True)

    # Step 4: Run the batch OCR process
    ocr_engine.batch_process(
        input_folder=input_dir,
        output_folder=output_dir,
        format="json"
    )

    # Step 5: Confirmation message
    print("Batch conversion complete.")

if __name__ == "__main__":
    main()
```

**Expected console output**

```
Scanning folder: /home/user/YOUR_DIRECTORY/scans/
Found 42 image files.
Processing file 1/42: invoice_001.png … done.
Processing file 2/42: receipt_2024-03.jpg … done.
…
Batch conversion complete.
```

You can verify the JSON by opening any file in `json_output` with a text editor or by loading it in Python:

```python
import json, pathlib

sample = pathlib.Path(output_dir) / "invoice_001.json"
data = json.loads(sample.read_text())
print(data["text"])
```

You should see the raw OCR‑extracted text printed to the console.

## Wrapping Up

We’ve just covered **how to batch OCR** a whole directory of scanned images and **extract text from scans** into clean, machine‑readable JSON files. The approach is deliberately simple: set up the engine once, point it at a folder, and let the library handle the heavy lifting. From here you can:

- Plug the JSON

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}