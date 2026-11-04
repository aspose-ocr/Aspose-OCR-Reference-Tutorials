---
category: general
date: 2026-04-26
description: how to use OCR on scanned PDFs, extract text from PDF, run OCR on PDF,
  and convert scanned PDF to searchable files in a few steps.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: en
og_description: 'how to use OCR in Python: learn how to extract text from PDF, run
  OCR on PDF, and convert scanned PDF into searchable documents.'
og_title: how to use OCR – Quick Guide to Extract Text from PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: how to use OCR – Extract Text from PDF with Python
url: /python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to use OCR – Extract Text from PDF with Python

Ever wondered **how to use OCR** to pull text out of a scanned contract, receipt, or ebook? You're not alone. In many real‑world projects the PDF you receive is just an image, and without OCR you can't search, index, or analyze its contents.  

In this tutorial we'll walk through a complete, runnable example that shows **how to use OCR**, how to **extract text from PDF**, and why you might want to **convert scanned PDF** files into searchable documents. We'll also cover the subtle art of **loading PDF as image** so the OCR engine can see every page clearly.

> **Quick preview:** By the end you’ll have a script that loads a multi‑page PDF, runs OCR on each page, and prints the recognized text – no external services required.

## What You’ll Need

- Python 3.9+ (any recent version works)
- `aocr` package (or any compatible OCR library that provides `OcrEngine` and `Image.load`)
- A scanned PDF file you want to process (e.g., `contract.pdf`)
- A modest amount of RAM (≈ 200 MB per 100‑page PDF is usually fine)

If you haven’t installed the OCR library yet, run:

```bash
pip install aocr
```

> **Pro tip:** Use a virtual environment to keep your dependencies tidy.

## Step 1: Load PDF as Image – The First Piece of the Puzzle

Before any OCR can happen, the PDF must be represented as an image. This is where the secondary keyword **load pdf as image** comes into play.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Why this matters:* `aocr.Image.load` internally rasterizes each PDF page into a bitmap that the OCR engine can understand. If you skip this step and feed the raw PDF, the engine will raise an error because it expects pixel data, not vector data.

> **Note:** The path can be absolute or relative. Make sure the file is readable; otherwise you’ll hit a `FileNotFoundError`.

## Step 2: Run OCR on PDF – Turning Pixels into Characters

Now that the PDF lives as an image, we can finally **run OCR on PDF**. The following snippet processes every page in one go:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*What’s happening under the hood?* `process_all_pages` loops through the rasterized pages, applies the OCR model, and returns a list of result objects—one per page. Each result contains the recognized text, confidence scores, and bounding boxes (if you need them later).

## Step 3: Extract Text from PDF – Pulling the Strings Out

With OCR results in hand, extracting the plain text becomes trivial. We’ll iterate over the pages and print the output, demonstrating the secondary keyword **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Expected output** (truncated for brevity):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

If you need the text in a single string, simply concatenate:

```python
full_text = "\n".join(r.text for r in page_results)
```

Now you have successfully **extracted text from PDF** using OCR.

## Step 4: Convert Scanned PDF – Making It Searchable

Many downstream tools (like Elasticsearch or SharePoint) expect a searchable PDF rather than a plain‑text dump. You can embed the OCR output back into the original PDF, effectively **convert scanned PDF** into a searchable version.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Why bother?* A searchable PDF retains the original layout and images while allowing text selection and indexing—a win‑win for both humans and machines.

## Common Pitfalls & Edge Cases

### Multi‑Page PDFs Larger Than Memory

If your PDF has hundreds of pages, loading everything at once may exhaust RAM. The `aocr` library supports lazy loading:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Then process pages one by one:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Low‑Quality Scans

OCR accuracy drops dramatically on blurry or low‑contrast scans. Before feeding the image to the engine, consider preprocessing:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Language Support

By default the engine assumes English. To **run OCR on PDF** in another language, set the language code:

```python
ocr_engine.language = "spa"  # Spanish
```

Make sure the corresponding language model is installed.

## Full Working Example

Putting everything together, here’s a self‑contained script you can drop into a file called `ocr_pdf.py` and run immediately:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Run it like so:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

You’ll see the text printed to the console, and if you supplied `-o`, a searchable PDF will appear next to the original file.

## Pro Tips & Best Practices

- **Batch processing:** When handling dozens of PDFs, wrap the above logic in a loop and log each file’s success/failure.
- **Confidence filtering:** Each `page_result` includes a confidence metric. Discard or flag pages with low confidence for manual review.
- **Parallelism:** If your CPU has multiple cores, consider using `concurrent.futures` to process pages in parallel—just be mindful of memory usage.
- **Version lock:** The `aocr` API can evolve. Pin the version in `requirements.txt` (e.g., `aocr==2.3.1`) to avoid breaking changes.

## Conclusion

We’ve walked through **how to use OCR** to **extract text from PDF**, **run OCR on PDF**, **load PDF as image**, and even **convert scanned PDF** into a searchable format. The code is complete, the explanations cover both the *what* and the *why*, and you now have a reusable pattern for any project that deals with image‑based PDFs.

What’s next? Try feeding the extracted text into a natural‑language pipeline, index the searchable PDFs with Elasticsearch, or experiment with different OCR back‑ends like Tesseract or Azure Computer Vision. The sky’s the limit, and the tools are right at your fingertips.

Happy coding, and may your PDFs always be searchable! 

![how to use OCR example](/images/ocr_workflow.png "how to use OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}