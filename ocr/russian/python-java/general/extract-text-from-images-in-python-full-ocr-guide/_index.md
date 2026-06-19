---
category: general
date: 2026-06-19
description: Извлекайте текст из изображений с помощью Python OCR. Узнайте об автоматическом
  определении языка, параллельной обработке и пакетном распознавании в кратком руководстве.
draft: false
keywords:
- extract text from images
- Python OCR library
- automatic language detection
- parallel processing OCR
- batch image recognition
- ocr.OcrEngine usage
language: ru
og_description: Извлекать текст из изображений с помощью Python OCR. Это руководство
  демонстрирует автоматическое определение языка, параллельную обработку и пакетное
  распознавание в одном учебнике.
og_title: Извлечение текста из изображений в Python — Полное руководство по OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  headline: extract text from images in Python – Full OCR Guide
  type: TechArticle
- description: extract text from images using Python OCR. Learn automatic language
    detection, parallel processing, and batch recognition in a concise tutorial.
  name: extract text from images in Python – Full OCR Guide
  steps:
  - name: Python 3.8 or newer installed.
    text: Python 3.8 or newer installed.
  - name: The `ocr` package (`pip install ocr`).
    text: The `ocr` package (`pip install ocr`).
  - name: A folder of PNG (or JPG) images you want to process.
    text: A folder of PNG (or JPG) images you want to process.
  - name: Basic familiarity with Python functions and loops.
    text: Basic familiarity with Python functions and loops.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Извлечение текста из изображений в Python — Полное руководство по OCR
url: /ru/python-java/general/extract-text-from-images-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# извлечение текста из изображений в Python – Полное руководство по OCR

Задумывались ли вы когда‑нибудь, как **извлечь текст из изображений** без ручного ввода каждого слова? Вы не одиноки. Будь то оцифровка старых чеков, создание поискового архива документов или просто игра с крутыми AI‑трюками, способность извлекать текст из картинок — это обязательный навык для любого разработчика Python сегодня.

В этом руководстве мы пройдем полный, готовый к запуску пример, который **извлекает текст из изображений** с помощью популярного OCR‑движка. Мы рассмотрим автоматическое определение языка, параллельную обработку для ускорения и пакетное распознавание изображений, чтобы вы могли обрабатывать десятки файлов за секунды. Звучит как то, что вам нужно? Давайте начнём.

## Что вы узнаете

- Как создать экземпляр OCR‑движка с помощью `ocr.OcrEngine`.
- Включение **автоматического определения языка**, чтобы движок сам выбирал нужный язык.
- Настройка **параллельной обработки OCR** с пользовательским пулом потоков.
- Запуск **пакетного распознавания изображений** для списка файлов.
- Вывод распознанного текста для каждого изображения, готового к сохранению или индексации.

Никакой внешней документации не требуется — всё, что нужно, находится здесь, а код работает сразу после установки пакета `ocr` (установите его через `pip install ocr`).

## Требования

1. Python 3.8 или новее установлен.
2. Пакет `ocr` (`pip install ocr`).
3. Папка с PNG (или JPG) изображениями, которые вы хотите обработать.
4. Базовое знакомство с функциями и циклами Python.

Вот и всё — без тяжёлых зависимостей, без магии GPU, просто чистый Python.

![пример извлечения текста из изображений](https://example.com/ocr-demo.png "Скриншот, показывающий вывод извлечения текста из изображений")

*Alt text: скриншот демонстрации извлечения текста из изображений*

## Шаг 1 – Настройка OCR‑движка (Основное ключевое слово в действии)

First thing’s first: create an OCR engine instance. Think of `ocr.OcrEngine()` as the brain behind the operation; it knows how to read characters, lines, and paragraphs.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

Why do we need an explicit engine? Because the **ocr.OcrEngine usage** gives you fine‑grained control over language settings, threading, and more. It’s the most flexible way to **extract text from images** compared to one‑liner helpers.

## Шаг 2 – Позвольте движку автоматически определять языки

Most OCR libraries require you to tell them which language to look for. That’s fine for a single‑language project, but cumbersome for a mixed‑language batch. Luckily, the `ocr` package supports **automatic language detection**.

```python
# Step 2: Enable automatic language detection
engine.language = ocr.Language.Auto
```

Setting `engine.language` to `ocr.Language.Auto` tells the engine to sniff each image and pick the appropriate language model. This tiny line saves you hours of manual configuration when you’re dealing with international documents.

## Шаг 3 – Ускорьте процесс с помощью параллельной обработки OCR

If you have four or more CPU cores, why not use them? The engine can spin up a thread pool, letting multiple images be processed at the same time. This is where **parallel processing OCR** shines.

```python
# Step 3: Enable parallel processing with four worker threads
engine.set_thread_pool_size(4)
```

Feel free to adjust the number `4` based on your machine. More threads → faster batch runs, but remember that each thread consumes memory, so find a sweet spot for your environment.

## Шаг 4 – Сбор изображений для обработки

Now we need a list of file paths. You can build this list manually, read it from a CSV, or use `glob`. For clarity, we’ll hard‑code a short list:

```python
# Step 4: Prepare a list of image files to be recognized
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png",
    "YOUR_DIRECTORY/doc4.png"
]
```

Replace `YOUR_DIRECTORY` with the actual path on your system. If you have dozens of files, a quick `glob.glob("*.png")` will do the heavy lifting.

## Шаг 5 – Запуск пакетного распознавания изображений

Here’s the heart of the tutorial: a single call that processes every image in `files` and returns a list of result objects. This is the **batch image recognition** feature that makes large‑scale OCR practical.

```python
# Step 5: Perform batch recognition on all images
results = engine.recognize_batch(files)
```

Behind the scenes, the engine distributes each file across the four worker threads we configured earlier, while also auto‑detecting the language for each picture. The method returns a list where each element holds the recognized text and metadata.

## Шаг 6 – Вывод (или сохранение) извлечённого текста

Finally, we loop over the results and print the text. In a real project you’d probably write this to a database or a CSV file, but printing keeps the example simple.

```python
# Step 6: Output the recognized text for each image
for result in results:
    print("---")
    print(f"File: {result.file_path}")
    print("Extracted Text:")
    print(result.text.strip())
    print("---\n")
```

**Expected output** (truncated for brevity):

```
---
File: YOUR_DIRECTORY/doc1.png
Extracted Text:
Invoice #12345
Date: 2024‑03‑15
Total: $250.00
---
```

Each block shows the filename followed by the OCR‑derived string. If an image contains multiple languages, you’ll see the appropriate characters appear thanks to the earlier **automatic language detection** step.

## Профессиональные советы и распространённые подводные камни

- **Image quality matters** – blurry or low‑contrast pictures will produce garbage. Pre‑process with OpenCV (`cv2.threshold`, `cv2.resize`) if needed.
- **Thread count vs. I/O** – If your images live on a slow network drive, more threads might not help. Keep an eye on CPU usage with `top` or `Task Manager`.
- **Unicode handling** – The `result.text` is a Unicode string. When writing to files, open them with `encoding="utf‑8"` to avoid `UnicodeEncodeError`s.
- **Memory usage** – Large PDFs can consume a lot of RAM. If you hit `MemoryError`, reduce the thread pool size or process images in smaller chunks.

## Полный рабочий скрипт

Below is the complete, copy‑and‑paste‑ready script that incorporates every step we discussed. Save it as `batch_ocr.py` and run `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script to extract text from images using the ocr package.
Features:
- Automatic language detection
- Parallel processing with configurable thread pool
- Simple batch API for multiple files
"""

import ocr
import os
import sys

def main(image_dir: str, workers: int = 4):
    # Verify directory exists
    if not os.path.isdir(image_dir):
        print(f"Error: Directory '{image_dir}' does not exist.", file=sys.stderr)
        sys.exit(1)

    # Build list of PNG/JPG files
    supported_ext = (".png", ".jpg", ".jpeg", ".tif", ".tiff")
    files = [
        os.path.join(image_dir, f)
        for f in os.listdir(image_dir)
        if f.lower().endswith(supported_ext)
    ]

    if not files:
        print("No supported image files found in the directory.", file=sys.stderr)
        sys.exit(1)

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto          # automatic language detection
    engine.set_thread_pool_size(workers)         # parallel processing OCR

    # Perform batch recognition
    print(f"Processing {len(files)} files with {workers} workers...")
    results = engine.recognize_batch(files)

    # Output results
    for result in results:
        print("---")
        print(f"File: {result.file_path}")
        print("Extracted Text:")
        print(result.text.strip())
        print("---\n")

if __name__ == "__main__":
    # Example usage: python batch_ocr.py ./my_images 4
    if len(sys.argv) < 2:
        print("Usage: python batch_ocr.py <image_directory> [worker_count]")
        sys.exit(1)

    directory = sys.argv[1]
    worker_count = int(sys.argv[2]) if len(sys.argv) > 2 else 4
    main(directory, worker_count)
```

Run it like this:

```bash
python batch_ocr.py ./my_images 4
```

You’ll see a nicely formatted block of text for each image, proving that you can **extract text from images** at scale.

## Что дальше?

Now that you’ve mastered the basics of **extract text from images** with Python, consider exploring:

- **Post‑processing**: очистка вывода OCR с помощью regex или библиотек обработки естественного языка.
- **PDF conversion**: передача извлечённых строк в генератор PDF для поисковых PDF‑файлов.
- **Cloud OCR services**: сравнение локальных результатов `ocr` с Google Vision или Azure OCR для точности в граничных случаях.
- **GUI front‑end**: создание небольшого приложения на Flask или FastAPI, позволяющего пользователям загружать изображения и мгновенно видеть извлечённый текст.

Each of these topics builds on the **Python OCR library** foundation you just set up, and they all benefit from the same **parallel processing OCR** tricks we used here.

---

*Счастливого кодинга! Если возникнут проблемы, оставляйте комментарий ниже — я всегда готов помочь с нюансами OCR.*

## Что следует изучить дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображений с помощью OCR‑операции в папках](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}