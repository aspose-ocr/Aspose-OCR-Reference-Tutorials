---
category: general
date: 2026-03-18
description: 對圖像執行 OCR，從相片中提取手寫文字。了解如何將手寫圖像轉換、從 jpg 提取文字，以及從相片識別文字。
draft: false
keywords:
- perform OCR on image
- convert handwritten image
- extract text from jpg
- extract handwritten text
- recognize text from photo
language: zh-hant
og_description: 在圖像上執行 OCR，從相片中提取手寫文字。本教學示範如何將手寫圖像轉換並辨識 JPG 檔案中的文字。
og_title: 對圖像執行 OCR – 完整手寫文字指南
tags:
- OCR
- Python
- Handwriting Recognition
title: 執行圖像 OCR – 將手寫圖像轉換為文字
url: /zh-hant/python/general/perform-ocr-on-image-convert-handwritten-image-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在圖像上執行 OCR – 全端手寫文字擷取

Ever needed to **perform OCR on image** files but weren’t sure whether the engine could read messy handwriting? You’re not alone. In many real‑world apps—think expense‑receipt scanners or note‑taking utilities—you’ll run into photos of scribbles that need to be turned into plain text.  

In this guide we’ll show you how to **convert handwritten image** files, **extract text from jpg**, and even **recognize text from photo** streams using a tiny Python‑style library called `ocr`. By the end you’ll have a ready‑to‑run script that pulls out every word from a handwritten note, no matter how shaky the pen was.

## 需要的工具

- Python 3.8+ (the code works on any recent interpreter)
- The hypothetical `ocr` package – install it with `pip install ocr-lib` (replace with the real package name you use)
- A clear photograph of a handwritten note saved as `note.jpg` (or any other image format)
- A modest amount of curiosity—no advanced ML background required

That’s it. No external services, no API keys, just a local engine that can **perform OCR on image** data.

![perform OCR on image screenshot](example.png)

*Alt text: perform OCR on image screenshot showing code editor with OCR script.*

## 步驟說明

Below we break the process into bite‑size chunks. Each header includes a keyword so you can skim quickly, and every block explains **why** we’re doing what we do—not just **what**.

### 步驟 1：安裝並驗證 OCR 函式庫

Before you can **perform OCR on image** files, the library must be present in your environment. Open a terminal and run:

```bash
pip install ocr-lib
```

> **Pro tip:** If you work in a virtual environment (highly recommended), activate it first. That keeps your dependencies tidy and avoids version clashes.

After installation, let’s make sure Python can import the package:

```python
try:
    import ocr
    print("OCR library loaded successfully.")
except ImportError as e:
    raise SystemExit("Failed to import ocr library. Did you run pip install?") from e
```

If you see the success message, you’re ready to **convert handwritten image** data.

### 步驟 2：建立引擎實例並選擇手寫模式

Most OCR engines default to printed‑text recognition. Since we want to **extract handwritten text**, we need to switch the mode explicitly. This step is crucial because handwriting often requires different preprocessing (like smoothing strokes).

```python
# Step 2: Initialize the OCR engine
engine = ocr.OcrEngine()

# Tell the engine we’re dealing with handwriting
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

print("Engine configured for handwritten recognition.")
```

*Why this matters:* Handwritten characters can vary wildly in size and slant. By setting `RecognitionMode.HANDWRITTEN`, the engine applies a model trained on cursive samples, boosting accuracy dramatically.

### 步驟 3：載入要分析的照片

Now we actually **perform OCR on image** content. The `load_image` method accepts a path or a file‑like object. For demonstration, we’ll load a JPEG, but the same call works for PNG, BMP, or even PDF pages.

```python
# Step 3: Load the image file (replace the path with yours)
image_path = "YOUR_DIRECTORY/note.jpg"
engine.load_image(image_path)

print(f"Image '{image_path}' loaded into the OCR engine.")
```

If your image lives in a cloud bucket, just download it first or pass a `BytesIO` stream—`ocr` is flexible enough to handle both.

### 步驟 4：執行辨識程序

With the engine primed and the image in memory, we finally **perform OCR on image** and retrieve the raw text.

```python
# Step 4: Execute recognition
extracted_text = engine.recognize()

print("=== Extracted Text ===")
print(extracted_text)
```

The `recognize()` call returns a plain Unicode string. For most use‑cases you can write it straight to a `.txt` file, feed it to a natural‑language pipeline, or display it in a GUI.

### 步驟 5：可選 – 清理或後處理輸出

Handwritten OCR isn’t perfect; you’ll often see stray line breaks or mis‑read characters. A quick clean‑up step can improve downstream results.

```python
# Step 5: Simple post‑processing (optional)
def tidy(text):
    # Collapse multiple spaces, strip leading/trailing whitespace
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(extracted_text)

print("\n=== Cleaned Text ===")
print(clean_text)
```

Feel free to plug in spell‑checkers, language models, or custom regexes depending on your domain.

### 完整腳本 – 可直接複製貼上

Putting everything together, here’s the complete, runnable program that **extracts handwritten text** from a JPEG and prints a tidy result.

```python
# -*- coding: utf-8 -*-
"""
Complete example: Perform OCR on image to extract handwritten text.
"""

# -------------------------------------------------
# Step 1: Import the OCR library and create an engine
# -------------------------------------------------
import ocr

engine = ocr.OcrEngine()

# -------------------------------------------------
# Step 2: Set the engine to recognize handwritten text
# -------------------------------------------------
engine.set_recognition_mode(ocr.RecognitionMode.HANDWRITTEN)

# -------------------------------------------------
# Step 3: Load the image you want to analyze
# -------------------------------------------------
image_path = "YOUR_DIRECTORY/note.jpg"   # <-- change this to your file
engine.load_image(image_path)

# -------------------------------------------------
# Step 4: Perform recognition and output the extracted text
# -------------------------------------------------
raw_text = engine.recognize()
print("=== Raw OCR Output ===")
print(raw_text)

# -------------------------------------------------
# Step 5: Optional cleanup for nicer display
# -------------------------------------------------
def tidy(text):
    return "\n".join(line.strip() for line in text.splitlines() if line.strip())

clean_text = tidy(raw_text)
print("\n=== Cleaned OCR Output ===")
print(clean_text)
```

**Expected output** (your actual text will differ, of course):

```
=== Raw OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3

=== Cleaned OCR Output ===
Meeting notes:
- Discuss project timeline
- Assign tasks to John, Ana
- Review budget Q3
```

If you see gibberish, double‑check the image quality (good lighting, minimal blur) and make sure you’re in `HANDWRITTEN` mode. Those two factors account for most recognition errors.

## 常見問題 (FAQ)

| Question | Answer |
|----------|--------|
| **Can I use this to extract text from a PNG?** | Absolutely. `engine.load_image("scan.png")` works the same way. |
| **What if my image is a PDF page?** | Convert the page to an image first (e.g., with `pdf2image`) then feed it to the engine. |
| **Is the library thread‑safe?** | Yes, you can instantiate separate `OcrEngine` objects per thread. |
| **How does this differ from `pytesseract`?** | `ocr` abstracts away the Tesseract binary and includes a built‑in handwritten model, so you don’t need to install external executables. |
| **What if I need to **extract text from JPG** files in bulk?** | Wrap the script in a loop, or use `engine.load_image` on each file and collect results in a list or CSV. |

## 邊緣情況與最佳實踐

1. **Low‑contrast photos** – Increase contrast programmatically before loading, or use `engine.apply_preprocessing('contrast', level=2)`.
2. **Mixed printed & handwritten** – Run two passes: first with `HANDWRITTEN`, then with `PRINTED`, and merge the outputs.
3. **Large images** – Downscale to ~1500 px width; OCR engines usually perform faster with smaller buffers without losing accuracy.
4. **Unicode characters** – The library returns UTF‑8 strings, so you can handle emojis, accented letters, or mathematical symbols out of the box.

## 總結

We’ve just walked through a concrete example of how to **perform OCR on image** files, specifically targeting handwritten notes. By installing the `ocr` package, configuring the engine for `HANDWRITTEN` mode, loading a photo, and calling `recognize()`, you can **convert handwritten image** data into clean, searchable text.  

From here you might **extract text from jpg** files in bulk, feed the output into a note‑taking app, or combine it with speech synthesis for accessibility. The sky’s the limit, and the code above gives you a solid foundation to experiment.

Got a twist you’d like to share—maybe a different file format or a quirky preprocessing trick? Drop a comment, and let’s keep the conversation going. Happy coding, and enjoy turning those scribbles into digital gold!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}