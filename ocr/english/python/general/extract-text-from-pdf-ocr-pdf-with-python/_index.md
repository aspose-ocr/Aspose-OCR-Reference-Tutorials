---
category: general
date: 2026-04-29
description: Extract text from PDF using Aspose OCR in Python. Learn batch OCR PDF
  processing, convert scanned PDF text, and handle low‑confidence pages.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: en
og_description: Extract text from PDF with Aspose OCR in Python. This guide shows
  batch OCR PDF processing, converting scanned PDF text, and handling low‑confidence
  results.
og_title: Extract Text from PDF – OCR PDF with Python
tags:
- OCR
- Python
- PDF processing
title: Extract Text from PDF – OCR PDF with Python
url: /python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from PDF – OCR PDF with Python

Ever needed to **extract text from PDF** but the file is just a scanned image? You're not alone—many developers hit that wall when trying to turn PDFs into searchable data. The good news? With Aspose OCR for Python you can convert scanned PDF text in a few lines, and even run **batch OCR PDF processing** when you have dozens of files to handle.

In this tutorial we’ll walk through the whole workflow: setting up the library, running OCR on a single PDF, scaling to a batch, and dealing with low‑confidence pages so you know when a manual review is required. By the end you’ll have a ready‑to‑run script that extracts text from any scanned PDF, and you’ll understand the why behind each step.

## What You’ll Need

Before we dive in, make sure you have:

- Python 3.8 or newer (the code uses f‑strings, so 3.6+ works, but 3.8+ is recommended)
- An Aspose OCR for Python license or a free trial key (you can get one from the Aspose website)
- A folder with one or more scanned PDFs you want to process
- A modest amount of disk space for the generated *.txt* reports

That’s it—no heavy external dependencies, no OpenCV gymnastics. The Aspose OCR engine does the heavy lifting for you.

## Setting Up the Environment

First, install the Aspose OCR package from PyPI:

```bash
pip install aspose-ocr
```

If you have a license file (`Aspose.OCR.lic`), place it in your project root and activate it like so:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Pro tip:** Keep the license file out of version control; add it to `.gitignore` to avoid accidental exposure.

## Performing OCR on a Single PDF

Now let’s extract text from a single scanned PDF. The core steps are:

1. Create an `OcrEngine` instance.
2. Point it at the PDF file.
3. Retrieve an `OcrResult` for each page.
4. Write the plain‑text output to disk.
5. Dispose of the engine to free native resources.

Here’s the full, runnable script:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**What you’ll see:** For each page the script prints something like `Page 1: confidence 97.45%`. If a page falls under the 80 % threshold, a warning appears, letting you know that the OCR might have missed characters.

### Why This Works

- **`OcrEngine`** is the gateway to the native Aspose OCR library; it handles everything from image preprocessing to character recognition.
- **`extract_from_pdf`** automatically rasterizes each PDF page, so you don’t need to convert the PDF to images yourself.
- **Confidence scores** let you automate quality checks—critical when you’re processing legal or medical documents where accuracy matters.

## Batch OCR PDF Processing with Python

Most real‑world projects involve more than one file. Let’s extend the single‑file script to a **batch OCR PDF processing** pipeline that walks through a directory, processes each PDF, and stores the results in a matching sub‑folder.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### How This Helps

- **Scalability:** The function walks the folder once, creating a dedicated output sub‑folder for each PDF. This keeps things tidy when you have dozens of documents.
- **Reusability:** `ocr_pdf_file` can be called from other scripts (e.g., a web service) because it’s a pure function.
- **Error handling:** The script prints a friendly message if the input folder is empty, saving you from a silent failure.

## Converting Scanned PDF Text – Handling Edge Cases

While the code above works for most PDFs, you might run into a few quirks:

| Situation | Why It Happens | How to Mitigate |
|-----------|----------------|-----------------|
| **Encrypted PDFs** | The PDF is password‑protected. | Pass the password to `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Multi‑language documents** | Aspose OCR defaults to English. | Set `ocr_engine.language = "spa"` for Spanish, or provide a list for mixed languages. |
| **Very large PDFs (>500 pages)** | Memory usage spikes because each page is loaded into RAM. | Process the PDF in chunks using `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` and loop. |
| **Poor scan quality** | Low DPI or heavy noise reduces confidence. | Pre‑process the PDF with `engine.image_preprocessing = True` or increase the DPI via `engine.dpi = 300`. |

> **Watch out:** Turning on image preprocessing can increase CPU time noticeably. If you’re running a nightly batch, schedule enough time or spin up a separate worker.

## Verifying the Output

After the script finishes, you’ll find a folder structure like:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Open any `.txt` file; you should see clean, UTF‑8 encoded text that mirrors the original scanned content. If you notice garbled characters, double‑check the PDF’s language settings and ensure the correct font packs are installed on the machine.

## Cleaning Up Resources

Aspose OCR relies on native DLLs, so it’s essential to call `engine.dispose()` once you’re done. Forgetting this step can lead to memory leaks, especially in long‑running batch jobs.

```python
# Always the last line of your script
engine.dispose()
```

## Full End‑to‑End Example

Putting everything together, here’s a single

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}