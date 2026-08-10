---
category: general
date: 2026-06-06
description: Как выполнять OCR PDF с помощью Aspose OCR Cloud. Узнайте, как извлекать
  текст из PDF, конвертировать страницу PDF в PNG и сохранять изображения страниц
  PDF в Python.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf page png
- extract plain text pdf
- save pdf page images
language: ru
og_description: Как выполнять OCR PDF с помощью Aspose OCR Cloud. Это руководство
  показывает, как извлекать простой текст из PDF, конвертировать страницу PDF в PNG
  и сохранять изображения страниц PDF.
og_title: Как выполнить OCR PDF с помощью Aspose OCR Cloud – пошагово
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF using Aspose OCR Cloud. Learn to extract text from PDF,
    convert PDF page PNG, and save PDF page images in Python.
  headline: How to OCR PDF with Aspose OCR Cloud – Complete Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Как распознать PDF с помощью Aspose OCR Cloud – Полное руководство
url: /ru/python-java/general/how-to-ocr-pdf-with-aspose-ocr-cloud-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR PDF с помощью Aspose OCR Cloud – Полное руководство

Ever wondered **how to OCR PDF** files without wrestling with heavyweight desktop tools? You’re not alone—many developers hit that wall when they need a quick, programmatic way to pull text out of scanned documents. The good news? With Aspose OCR Cloud you can **extract text from PDF**, turn each page into a PNG, and even **save PDF page images** for later use, all from a tidy Python script.

In this tutorial we’ll walk through everything you need to know: from installing the SDK, licensing the engine, and recognizing multi‑page PDFs, to extracting plain text, converting pages to PNG, and persisting those images on disk. By the end you’ll have a reusable snippet you can drop into any project that needs **how to OCR PDF** capabilities.

## Что вам понадобится

- **Python 3.8+** (код работает также на 3.10 и новее)  
- Учётная запись Aspose OCR Cloud – вы получите бесплатный пробный файл лицензии (`Aspose.OCR.lic`)  
- Пакет `asposeocrcloud` (`pip install asposeocrcloud`)  
- Отсканированный многостраничный PDF, который вы хотите обработать  

Это всё. Нет дополнительных бинарных файлов, нет нативных зависимостей, только чистый Python.

## Как выполнить OCR PDF – Настройка и лицензия

Before you can call any OCR methods, you have to tell the SDK who you are. Aspose uses a lightweight license file that you place somewhere accessible to your script.

```python
# Step 1: Import the OCR package and apply your license (optional but recommended)
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply the license – replace the path with your actual .lic file location
License().set_license("Aspose.OCR.lic")
```

*Pro tip:* Если пропустить шаг с лицензией, SDK всё равно будет работать, но в полученных изображениях появится небольшой водяной знак. Не идеально для продакшна.

## Шаг 2: Установите Python SDK Aspose OCR Cloud

Open a terminal and run:

```bash
pip install asposeocrcloud
```

The package pulls in all required dependencies (requests, pillow, etc.) so you don’t have to hunt down anything else.

## Шаг 3: Создайте OCR‑движок и выберите язык

The engine is the heart of the operation. You can specify any language supported by Aspose; English works for most cases.

```python
# Step 3: Create an OCR engine and set the recognition language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)
```

Why set the language? Потому что OCR‑движок использует словари, специфичные для языка, чтобы повысить точность. Если вы обрабатываете французские PDF, просто замените `ENGLISH` на `FRENCH`.

## Шаг 4: Укажите путь к вашему многостраничному PDF

Give the engine the full path to the file you want to process. Relative paths are fine as long as they resolve from the script’s working directory.

```python
# Step 4: Specify the path to the multi‑page PDF you want to process
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"
```

Make sure the file is readable; otherwise you’ll see a `FileNotFoundError`.

## Шаг 5: Запустите OCR – Вы получите список результатов

Calling `recognize_pdf` returns a list where each element corresponds to one page of the source PDF.

```python
# Step 5: Run OCR on the PDF – a list of OcrResult objects is returned (one per page)
results = engine.recognize_pdf(pdf_path)
```

Each `OcrResult` contains two handy properties:

- `text` – текстовое представление страницы (отлично подходит для **extract plain text pdf**)
- `image` – объект Pillow `Image` отрисованной страницы (идеально для **convert pdf page png**)

## Шаг 6: Извлеките текст из PDF и конвертируйте страницы в PNG

Now we loop through the results, print the extracted text, and save a PNG version of every page.

```python
# Step 6: Iterate through each page, output the extracted text and optionally save the page image
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    # Extract plain text for this page
    print(res.text)                     # <-- this is the "extract plain text pdf" part
    # Convert the page to PNG and save it
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # <-- this does the "convert pdf page png"
```

### Ожидаемый вывод в консоль

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

You’ll also find `page_1.png`, `page_2.png`, … floating in `YOUR_DIRECTORY`. Those are the rasterized page images you can feed into downstream image‑processing pipelines.

## Шаг 7: Сохраните изображения страниц PDF (необязательно, пост‑обработка)

If you only need the images and not the text, you can skip the `print(res.text)` line. Conversely, if you want to store the text in separate `.txt` files, just add a tiny write‑out:

```python
# Optional: Save each page's text to a .txt file
for i, res in enumerate(results, start=1):
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)
```

This small addition demonstrates how easy it is to **save PDF page images** while also persisting the extracted content.

## Полный рабочий пример

Putting everything together, here’s the complete script you can copy‑paste into `ocr_pdf.py`:

```python
import asposeocrcloud as ocr
from asposeocrcloud import OcrEngine, License

# Apply your license – optional but removes watermarks
License().set_license("Aspose.OCR.lic")

# Initialize the OCR engine and set language
engine = OcrEngine()
engine.set_recognition_language(ocr.Language.ENGLISH)

# Path to the source PDF
pdf_path = "YOUR_DIRECTORY/sample_multi_page.pdf"

# Run OCR – get a list of results (one per page)
results = engine.recognize_pdf(pdf_path)

# Process each page
for i, res in enumerate(results, start=1):
    print(f"--- Page {i} ---")
    print(res.text)  # extract plain text PDF
    # Save the rendered page as PNG
    res.image.save(f"YOUR_DIRECTORY/page_{i}.png")  # convert PDF page PNG
    # Optional: also save the text to a .txt file
    with open(f"YOUR_DIRECTORY/page_{i}.txt", "w", encoding="utf-8") as f:
        f.write(res.text)  # save PDF page images + text
```

Run it with:

```bash
python ocr_pdf.py
```

You should see the console dump of each page’s text and a series of PNG files

## Что изучать дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}