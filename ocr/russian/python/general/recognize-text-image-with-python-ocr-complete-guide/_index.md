---
category: general
date: 2026-06-28
description: Узнайте, как распознавать текстовые изображения с помощью Python OCR,
  извлекать текст из файлов PNG и выводить распознанный текст с надёжной обработкой
  ошибок.
draft: false
keywords:
- recognize text image
- extract text png
- load image ocr
- process image ocr
- print recognized text
language: ru
og_description: Пошаговое руководство по распознаванию текстового изображения в Python,
  извлечению текста из PNG и безопасному выводу распознанного текста.
og_title: Распознавание текста на изображении с помощью Python OCR – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text image using Python OCR, extract text png
    files, and print recognized text with robust error handling.
  headline: recognize text image with Python OCR – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Распознавание текста на изображении с помощью Python OCR – Полное руководство
url: /ru/python/general/recognize-text-image-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста на изображении с помощью Python OCR – Полное руководство

Ever wondered how to **recognize text image** in a Python script without pulling in a heavyweight framework? You're not alone. Many developers need a quick way to *load image OCR* a screenshot, a scanned receipt, or a simple PNG and get the text back.  

In this tutorial we’ll wire up a minimal OCR engine, attach a custom logger, **load image OCR**, run the **process image OCR**, and finally **print recognized text**. By the end you’ll have a self‑contained script that can also **extract text png** files on demand.

## Что вы получите

- Полностью рабочий фрагмент кода Python, который создаёт OCR‑движок, ведёт журнал каждого шага и корректно обрабатывает ошибки.  
- Чёткие объяснения *почему* каждая строка важна — чтобы вы могли адаптировать код под Tesseract, EasyOCR или любой другой бекенд.  
- Советы по типичным подводным камням (отсутствующие шрифты, повреждённые PNG) и способы их отладки.  

### Предварительные требования

- Установлен Python 3.8+  
- OCR‑библиотека, предоставляющая класс `OcrEngine` (в примере используется вымышленный, но типичный API; замените его на `pytesseract`, `easyocr` и т.д.).  
- PNG‑изображение, которое вы хотите проанализировать, сохранённое как `input.png` в выбранной вами папке.  

> **Pro tip:** Если вы используете `pytesseract`, сначала установите системный бинарный пакет Tesseract (`sudo apt install tesseract-ocr` в Linux), а затем выполните `pip install pytesseract pillow`.

---

## ## Recognize Text Image: Setting Up the Logger

A good logger is the unsung hero of any OCR pipeline. It tells you *when* the engine started, *what* file it opened, and *why* it might have failed.

```python
# Step 1: Define a simple logger for the OCR engine
def my_logger(level, message):
    """
    level: str – e.g., "INFO", "WARN", "ERROR"
    message: str – human‑readable description of the event
    """
    print(f"[{level}] {message}")
```

*Why this matters:*  
The logger decouples diagnostic output from the OCR core, making it easy to redirect logs to a file, a monitoring service, or even a UI later on.  

---

## ## Load Image OCR: Feeding the Engine a PNG

Before the engine can **process image OCR**, it needs a proper image object. Most libraries accept a Pillow `Image` instance.

```python
from PIL import Image

# Step 2: Create the OCR engine and attach the logger
ocr_engine = OcrEngine(logging=my_logger)

# Step 3: Load the image to be processed
image_path = "YOUR_DIRECTORY/input.png"
ocr_engine.set_image(Image.from_file(image_path))
my_logger("INFO", f"Loaded image from {image_path}")
```

*Key points:*  

- **load image ocr** – `Image.from_file` abstracts away the PNG decoding details.  
- Keep the path configurable; hard‑coding makes the script brittle.  
- The logger call confirms the image was successfully read, which is useful when the file is missing or corrupted.

---

## ## Process Image OCR: Recognizing the Text

Now the heavy lifting begins. The engine scans the bitmap, applies its neural nets or heuristics, and spits out a Unicode string.

```python
# Step 4: Recognize text from the image
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:
    # Step 5: Handle OCR errors gracefully
    my_logger("ERROR", f"OCR failed with code {e.code}: {e.message}")
    extracted_text = None
```

*Why we wrap it in `try/except`:*  
OCR can explode on low‑resolution PNGs, unsupported color spaces, or missing language data. Catching `OcrException` lets you **print recognized text** only when it actually exists, avoiding cryptic stack traces for end users.

---

## ## Print Recognized Text & Extract Text PNG

If the recognition succeeded, we display the result and optionally write it to a `.txt` file that mirrors the original PNG name.

```python
if extracted_text:
    # Step 6: Print the recognized text
    print("Recognized text:", extracted_text)
    my_logger("INFO", "Printed recognized text to console")

    # Optional: Save extracted text for later use
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
```

*What you get:*  

- **print recognized text** – immediate visual feedback in the terminal.  
- A side‑by‑side `.txt` file that effectively **extract text png** for downstream processing (search indexing, data entry, etc.).

---

## ## Common Edge Cases & How to Tackle Them

| Ситуация | Симптом | Решение |
|-----------|---------|-----|
| PNG только в градациях серого | OCR возвращает пустую строку | Преобразуйте в RGB (`Image.convert("RGB")`) перед передачей в движок. |
| Язык не поддерживается | `OcrException` с кодом `LANG_NOT_FOUND` | Установите языковой пакет (например, `tesseract‑lang‑fra` для французского) и задайте `ocr_engine.language = "fra"`. |
| Очень большое изображение ( > 5 MB ) | Медленное распознавание или ошибка памяти | Уменьшите размер с помощью `image.thumbnail((2000, 2000))` перед `set_image`. |
| Неожиданные символы | Искажённый вывод | Убедитесь, что файл действительно PNG; некоторые файлы маскируются под PNG, но являются JPEG. Используйте `Image.verify()` для проверки. |

---

## ## Full Working Example (Copy‑Paste Ready)

```python
# -*- coding: utf-8 -*-
"""
Complete script to recognize text image using a generic OCR engine.
Replace OcrEngine, OcrException with the concrete classes from your library.
"""

from PIL import Image

# ----------------------------------------------------------------------
# 1️⃣  Logger definition
# ----------------------------------------------------------------------
def my_logger(level: str, message: str) -> None:
    """Simple console logger."""
    print(f"[{level}] {message}")

# ----------------------------------------------------------------------
# 2️⃣  Engine creation & image loading
# ----------------------------------------------------------------------
ocr_engine = OcrEngine(logging=my_logger)   # <- adapt to your library

image_path = "YOUR_DIRECTORY/input.png"
try:
    img = Image.open(image_path)
    img.verify()                     # sanity check the PNG
    img = Image.open(image_path)     # reopen after verify
    ocr_engine.set_image(img)
    my_logger("INFO", f"Loaded image from {image_path}")
except Exception as load_err:
    my_logger("ERROR", f"Failed to load image: {load_err}")
    raise SystemExit(1)

# ----------------------------------------------------------------------
# 3️⃣  Text recognition
# ----------------------------------------------------------------------
try:
    extracted_text = ocr_engine.recognize()
    my_logger("INFO", "OCR succeeded")
except OcrException as e:            # replace with actual exception class
    my_logger("ERROR", f"OCR failed ({e.code}): {e.message}")
    extracted_text = None

# ----------------------------------------------------------------------
# 4️⃣  Output handling
# ----------------------------------------------------------------------
if extracted_text:
    print("Recognized text:", extracted_text)          # ✅ print recognized text
    txt_path = image_path.rsplit(".", 1)[0] + ".txt"
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(extracted_text)
    my_logger("INFO", f"Saved extracted text to {txt_path}")
else:
    my_logger("WARN", "No text extracted; check image quality.")
```

**Expected console output (happy path):**

```
[INFO] Loaded image from YOUR_DIRECTORY/input.png
[INFO] OCR succeeded
Recognized text: Invoice #12345
Total Amount: $1,250.00
Date: 2026‑06‑01
[INFO] Saved extracted text to YOUR_DIRECTORY/input.txt
```

If something goes wrong, you’ll see a clear `[ERROR]` line with the reason, thanks to the custom logger.

---

## ## Next Steps & Related Topics

- **extract text png** from batches: wrap the script in a `for` loop that walks a directory tree.  
- **process image ocr** with preprocessing (deskew, contrast boost) using OpenCV before feeding the engine.  
- Switch to a cloud OCR service (Google Vision, Azure Read) by swapping the `OcrEngine` implementation—your surrounding code stays the same.  
- Learn how to **print recognized text** into PDFs using `reportlab` for automated report generation.  

---

## Conclusion

We just walked through a compact, production‑ready way to **recognize text image** in Python, from loading the PNG to **print recognized text** and saving the result. By injecting a tiny logger, handling exceptions, and optionally persisting the output, the script is ready for both quick experiments and integration into larger pipelines.

Give it a spin with your own screenshots, tinker with image preprocessing, and you’ll soon be extracting text from any PNG you throw at it. Got questions? Drop a comment—happy OCRing!  

![пример распознавания текста на изображении](placeholder.png)


## Что следует изучить дальше?


The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Извлечение текста из изображения с помощью Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как выполнить извлечение текста из изображения из потока с использованием Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [Преобразование изображения в текст – OCR изображения по URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}