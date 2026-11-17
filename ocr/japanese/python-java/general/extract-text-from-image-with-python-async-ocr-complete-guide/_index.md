---
category: general
date: 2026-05-03
description: Python の非同期 OCR を使用して画像からテキストを抽出します。tif をテキストに変換する方法、OCR 用に画像を読み込む方法、そして画像からテキストを効率的に認識する方法を学びましょう。
draft: false
keywords:
- extract text from image
- convert tif to text
- load image for ocr
- extract image text
- recognize text from image
language: ja
og_description: Pythonの非同期OCRを使用して画像からテキストを抽出します。このガイドでは、tif をテキストに変換する方法、OCR 用に画像を読み込む方法、画像からテキストを認識する方法を示します。
og_title: Python非同期OCRで画像からテキストを抽出する完全ガイド
tags:
- OCR
- Python
- AsyncIO
title: Python非同期OCRで画像からテキストを抽出する完全ガイド
url: /ja/python-java/general/extract-text-from-image-with-python-async-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python Async OCRで画像からテキストを抽出 – 完全ガイド

Need to **画像からテキストを抽出** quickly? With Python's async OCR you can do it in just a few lines of code. Whether you're dealing with a massive .tif scan or a handful of JPEGs, this tutorial shows you how to convert tif to text, load image for OCR, and finally recognize text from image without blocking your event loop.

Here's the thing—most developers reach for a synchronous library, then stare at a frozen UI while the engine crunches pixels. In this guide we’ll flip that script by using Aspose OCR Cloud's asynchronous API, so your application stays responsive. By the end you’ll have a runnable script that pulls text out of any supported image format, and you’ll understand the why behind each step.

## 学べること

- How to set up the Aspose OCR Cloud SDK for Python.
- The exact code needed to **load image for OCR** and start an async recognition task.
- Tips for handling large .tif files and licensing quirks.
- Ways to **extract image text** safely, even when the service returns errors.
- A complete, copy‑paste‑ready example you can drop into your own project.

> **Prerequisite**: Python 3.8+ and an Aspose OCR Cloud license file (`Aspose.OCR.Java.lic`). No other third‑party packages are required.

---

![画像からテキストを抽出するワークフロー](workflow.png){: .align-center alt="画像からテキストを抽出するワークフロー"}

## 画像からテキスト抽出 – Async OCR の概要

Before we dive into code, let’s unpack the flow. When you call `recognize_async` the SDK sends the image to Aspose’s cloud, spins up a background job, and hands you a `Task` object. Awaiting that task yields an `OcrResult` containing the plain‑text representation of the picture. Because the call is asynchronous, you can fire off multiple jobs in parallel—perfect for batch processing large archives of scanned documents.

### 非同期を使う理由

- **Non‑blocking I/O** – Your event loop stays free to handle other work (e.g., serving HTTP requests).
- **Scalability** – Spin up dozens of recognitions at once; the cloud does the heavy lifting.
- **Responsiveness** – UI applications won’t freeze while waiting for the OCR engine.

Now that the “why” is clear, let’s see the **how**.

## Convert TIF to Text Using Aspose OCR

A common stumbling block is assuming every OCR library natively supports .tif. Aspose does, but you still need to feed it an `Image` object. The SDK abstracts the format, so you can simply point it at the file path.

```python
import asyncio
import asposeocrcloud as ocr

async def async_ocr(image_path: str) -> str:
    """
    Asynchronously extract text from the given image file.
    
    Parameters
    ----------
    image_path: str
        Path to the image (e.g., a .tif, .png, or .jpg file).

    Returns
    -------
    str
        The plain‑text OCR result.
    """
    # 1️⃣ Create the OCR engine and apply the license
    ocr_engine = ocr.OcrEngine()
    # The License class reads the .lic file; adjust the path if needed.
    ocr_engine.license = ocr.License().set_license("Aspose.OCR.Java.lic")

    # 2️⃣ Load the image for OCR – this works for TIF, PNG, JPEG, etc.
    ocr_image = ocr.Image.from_file(image_path)

    # 3️⃣ Start the asynchronous recognition task
    recognition_task = ocr_engine.recognize_async(ocr_image)

    # 4️⃣ Await the task and retrieve the extracted text
    ocr_result = await recognition_task
    return ocr_result.text
```

**重要な行の説明**

- `ocr_engine.license = ...` – Without a valid license the cloud returns a 403 error. Make sure the `.lic` file is accessible from your script’s working directory.
- `ocr.Image.from_file(image_path)` – This step **loads image for OCR**; the SDK automatically detects the format, so you don’t have to convert the .tif beforehand.
- `recognize_async` – Returns a coroutine‑compatible task. You could launch several of these in a `gather` call if you have a batch.

> **Pro tip**: If you’re processing gigabyte‑size TIFFs, consider splitting them into pages first. Aspose’s `Image.from_file` can accept a page index, which reduces memory pressure.

## Recognize Text from Image Asynchronously

Let’s see how you’d call the function from a typical script. The `asyncio.run` entry point is the simplest way to fire off the coroutine when you’re not already inside an event loop (e.g., a plain CLI tool).

```python
if __name__ == "__main__":
    # Replace with the actual path to your large TIF file.
    tif_path = "YOUR_DIRECTORY/large_image.tif"

    # Execute the coroutine and capture the output.
    extracted_text = asyncio.run(async_ocr(tif_path))

    # Print the result – this is the final step of **extracting text from image**.
    print("=== OCR Result ===")
    print(extracted_text)
```

**What to expect**

Running the script against a clear, high‑resolution scan typically yields a multi‑line string matching the printed page. If the image is noisy, Aspose still attempts to clean it up, but you may see garbled characters. In that case, consider pre‑processing with OpenCV (e.g., thresholding) before feeding the file to the OCR engine.

### エラーを優雅に処理する

```python
try:
    extracted_text = asyncio.run(async_ocr(tif_path))
except ocr.OcrException as exc:
    print(f"⚠️ OCR failed: {exc}")
    # Fallback: you could retry, log, or switch to a different service.
else:
    print(extracted_text)
```

Catching `OcrException` ensures your program doesn’t crash when the cloud returns an error—something that often trips newcomers who forget about network hiccups.

## Load Image for OCR – Practical Tips

1. **File Path vs. Bytes** – The SDK accepts a file path, but you can also load from a `bytes` object if the image lives in memory (`ocr.Image.from_bytes`). This is handy when you’ve already fetched the file from S3 or a database.
2. **Supported Formats** – Besides .tif, Aspose handles PDF, BMP, GIF, and even multi‑page TIFFs. Use `Image.from_file("doc.pdf")` to OCR PDFs directly.
3. **Performance** – For batch jobs, reuse the same `OcrEngine` instance; creating a new engine for each file adds unnecessary overhead.

## Full Working Example (All Steps in One Script)

Below is the complete, ready‑to‑run script that incorporates licensing, error handling, and a simple command‑line argument parser. Copy‑paste it, adjust the license path, and you’re set.

```python
# full_async_ocr.py
import asyncio
import argparse
import asposeocrcloud as ocr
import sys
from pathlib import Path

async def async_ocr(image_path: Path) -> str:
    """Extract text from an image file asynchronously."""
    engine = ocr.OcrEngine()
    # Adjust this if your .lic file lives elsewhere
    license_path = Path("Aspose.OCR.Java.lic")
    if not license_path.is_file():
        sys.exit("❌ License file not found. Place Aspose.OCR.Java.lic beside the script.")
    engine.license = ocr.License().set_license(str(license_path))

    # Load the image (supports TIFF, PNG, JPEG, PDF, etc.)
    image = ocr.Image.from_file(str(image_path))

    # Fire off the async recognition
    task = engine.recognize_async(image)

    # Await and return the plain text
    result = await task
    return result.text

def parse_args():
    parser = argparse.ArgumentParser(
        description="Extract text from image using Aspose OCR async API."
    )
    parser.add_argument(
        "image",
        type=Path,
        help="Path to the image file (e.g., .tif, .png, .jpg, .pdf)."
    )
    return parser.parse_args()

def main():
    args = parse_args()
    if not args.image.is_file():
        sys.exit(f"❌ File not found: {args.image}")

    try:
        text = asyncio.run(async_ocr(args.image))
    except ocr.OcrException as e:
        sys.exit(f"⚠️ OCR failed: {e}")

    print("\n=== Extracted Text ===\n")
    print(text)

if __name__ == "__main__":
    main()
```

**Expected output**

```
=== Extracted Text ===

Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
...
```

If the image contains a simple paragraph, the console will display the same lines, preserving line breaks. For multi‑page TIFFs, the SDK concatenates the pages in order.

## Frequently Asked Questions (FAQ)

**Q: 他の非同期フレームワーク（例: FastAPI）でも動作しますか？**  
A: Absolutely. Replace the `asyncio.run` call with `await async_ocr(path)` inside your endpoint, and FastAPI will handle the event loop for you。

**Q: 数百のファイルを一度に処理したい場合は？**  
A: Use `asyncio.gather`:

```python
tasks = [async_ocr(p) for p in list_of_paths]
results = await asyncio.gather(*tasks, return_exceptions=True)
```

**Q: パスワードで保護された PDF からテキストを抽出できますか？**  
A: Not directly. You’ll need to unlock the PDF first (e.g., with `pikepdf`) and then feed the decrypted bytes to `ocr.Image.from_bytes`。

**Q: 英語以外の言語を扱うには？**  
A: Set the language before recognition:

```python
engine.language = "spa"   # Spanish ISO code
```

Aspose supports over 60 languages; check the docs for the exact identifiers.

## Conclusion

You now have a solid, **extract text from image** solution that leverages Python’s `asyncio` and Aspose OCR Cloud’s asynchronous API. By following the steps above you can **convert tif to text**, **load image for OCR**, and **recognize text from image** in a non‑blocking fashion—perfect for both command‑line utilities and high‑traffic web services.

What’s next? Try batching a folder of scans, experiment with language settings, or pipe the OCR output into a downstream NLP pipeline. The sky’s

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}