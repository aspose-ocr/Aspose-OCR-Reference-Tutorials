---
category: general
date: 2026-06-06
description: Extract text from images pdf using Python OCR. Learn how to convert scanned
  documents to text quickly with async batch recognition.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: en
og_description: Extract text from images pdf with Python. This step‑by‑step guide
  shows how to convert scanned documents to text using async OCR.
og_title: Extract Text from Images PDF – Python OCR Tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Extract Text from Images PDF – Python Guide to Convert Scanned Documents to
  Text
url: /python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extract Text from Images PDF – Python Guide to Convert Scanned Documents to Text

Ever needed to **extract text from images pdf** without spending hours re‑typing? In this guide we'll show you how to **convert scanned documents to text** using a simple asynchronous OCR workflow in Python.  

If you’ve ever stared at a stack of scanned PDFs and thought, “There’s got to be a faster way,” you’re in the right place. We'll walk through every line of code, explain why each piece matters, and even cover a few edge cases you might run into.

## What You’ll Learn

- How to spin up an OCR engine and set the recognition language.  
- The mechanics of feeding a mixed list of PNGs and PDFs into a batch recognizer.  
- Running the OCR job asynchronously so your app stays responsive.  
- Pulling the results back, pairing them with their source files, and printing clean output.  

**Prerequisites**: Python 3.8+, a basic understanding of `asyncio` or `concurrent.futures`, and an OCR library that exposes an `OcrEngine` class similar to the one in the example (e.g., Aspose.OCR, Tesseract wrapper, or a custom wrapper). No heavy setup required—just install the library and you’re good to go.

![extract text from images pdf](https://example.com/placeholder.png "Screenshot of OCR output – extract text from images pdf")

## Extract Text from Images PDF – Setting Up the OCR Engine

The first thing you need is an OCR engine instance configured for the language of your documents. In our case we’ll use French, but you can swap it out for any supported language.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Why this matters**: Setting the language up front dramatically improves accuracy. The engine uses language‑specific dictionaries and character models; feeding it the wrong language is a common source of garbled output.

## Prepare the File List – Images and PDFs Together

Our batch recognizer can handle both raster images (`.png`, `.jpg`) and PDF containers. Just feed a plain Python list of file paths.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: Keep the list flat; the engine will internally unpack each PDF page into images before recognition. If you have thousands of files, consider chunking the list into smaller batches to avoid memory spikes.

## Kick Off Asynchronous Batch Recognition

Instead of blocking the main thread, we launch the OCR job in the background. The method returns a `Future` that will eventually hold a list of `OcrResult` objects.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**How it works**: Under the hood the engine spawns a thread pool (or an async task, depending on the implementation). This lets you continue doing other work—like updating a UI, fetching more files, or logging progress—while the heavy lifting happens elsewhere.

## Do Something Useful While OCR Runs

A common mistake is to sit idle and poll the future in a tight loop. Instead, you can perform any unrelated work. For demonstration, we’ll just print a status line.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Gather Results Once the Future Completes

When you’re ready to collect the OCR output, use `as_completed` from `concurrent.futures`. This pattern works whether you have one future or many.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**What you’ll see**: Each file path followed by the extracted plain‑text representation. For PDFs, `result.text` contains the concatenated text of every page.

### Expected Output (example)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

If you notice missing characters, double‑check that the language you set matches the document language, and consider pre‑processing the images (deskew, increase contrast) before feeding them to the engine.

## Handling Edge Cases and Common Pitfalls

| Situation | What to Do |
|-----------|------------|
| **Mixed languages** | Run a language‑detection pass first, then instantiate separate engines per language. |
| **Huge PDFs (> 100 MB)** | Split the PDF into individual pages on disk (e.g., using `PyPDF2`) and feed them as separate entries. |
| **Non‑Latin scripts** | Ensure the OCR library includes the required language pack; some libraries need you to download additional data files. |
| **Performance bottleneck** | Increase the thread pool size (`engine.set_thread_pool_size(8)`) or switch to a GPU‑accelerated backend if available. |
| **Missing text in low‑resolution images** | Pre‑process with OpenCV: `cv2.resize`, `cv2.threshold`, and `cv2.medianBlur` to improve readability. |

## Full Working Example (Copy‑Paste Ready)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Save this as `extract_text_async.py`, replace `YOUR_DIRECTORY` with the path to your files, install the OCR package (`pip install your-ocr-lib`), and run `python extract_text_async.py`. You should see the console output illustrated earlier.

## Next Steps – Going Beyond Basic Extraction

- **Post‑processing**: Strip extra whitespace, normalize Unicode (`unicodedata.normalize`), or run a spell‑checker to clean up OCR noise.  
- **Structured output**: Export results to CSV, JSON, or directly into a database for downstream search.  
- **Parallel batches**: If you have hundreds of files, spin up multiple futures and use a queue to keep the CPU busy without overwhelming memory.  
- **Integrate with web frameworks**: Hook this script into a Flask or FastAPI endpoint to provide on‑demand OCR as a service.

---

### TL;DR

You now know how to **extract text from images pdf** with a minimal Python script that runs OCR asynchronously, letting you **convert scanned documents to text** while your program stays responsive. Play with the language settings, batch sizes, and pre‑processing tricks to squeeze out every last character accuracy.

Got a twist you’d like to share—maybe OCR on handwritten notes or a cloud‑based service? Drop a comment, and happy coding!


## What Should You Learn Next?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Extract Text from Images Using Aspose.OCR – Allowed Characters](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}