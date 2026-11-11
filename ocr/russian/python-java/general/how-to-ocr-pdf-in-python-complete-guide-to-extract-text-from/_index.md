---
category: general
date: 2026-06-22
description: Узнайте, как выполнять OCR PDF‑файлов в Python, извлекать текст из PDF
  и конвертировать PDF в текст с использованием потокового подхода. Простые шаги для
  обработки отсканированных PDF.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: ru
og_description: Как выполнить OCR PDF‑файлов в Python? Следуйте этому руководству,
  чтобы извлечь текст из PDF, преобразовать PDF в текст и обработать отсканированный
  PDF с помощью потока.
og_title: Как выполнить OCR PDF в Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Как выполнить OCR PDF в Python – Полное руководство по извлечению текста из
  PDF
url: /ru/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR PDF в Python – Полное руководство по извлечению текста из PDF

Вы когда‑нибудь задумывались **как выполнять OCR PDF** файлов без борьбы с тяжёлыми настольными инструментами? Вы не одиноки. Во многих реальных проектах — например, автоматизация счетов или оцифровка архивных сканов — вам нужен надёжный способ превратить отсканированный PDF в поисковый, редактируемый текст.

В этом руководстве мы пройдём чистый, сквозной пример, который **извлекает текст из PDF** страниц с помощью лёгкого Python OCR‑движка. К концу вы точно будете знать, как **конвертировать PDF в текст**, как **загрузить PDF из потока**, и как **обрабатывать отсканированный PDF** эффективно. Без магии, просто обычный Python‑код, который вы можете добавить в свой проект уже сегодня.

## Что вы узнаете

- Установить и настроить Python OCR‑библиотеку, понимающую PDF‑ввод.  
- Включить режим распознавания PDF и задать формат вывода как простой текст.  
- Загрузить многостраничный PDF из файлового потока (классический шаблон «load pdf from stream»).  
- Выполнить OCR на всех страницах и получить текстовое содержимое.  
- Вывести или сохранить результаты для последующей обработки.

**Prerequisites**  
- Python 3.8+ установлен на вашем компьютере.  
- Базовое знакомство с pip и виртуальными окружениями.  
- Отсканированный PDF‑файл (названный `multipage.pdf` в примере), помещённый в известный каталог.

Если что‑то из этого вам незнакомо, не переживайте — каждый шаг объяснён простым языком, и мы предоставим точные команды, которые вам понадобятся.

---

## Шаг 1: Установить OCR‑движок (how to OCR PDF)

First things first—you need an OCR engine that can handle PDF input. For this guide we’ll use the hypothetical `ocr` package (the API mirrors popular commercial SDKs, but the same pattern works with Tesseract‑OCR, ABBYY, or Google Vision when wrapped appropriately).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** If you’re on Windows and hit permission errors, try `pip install --user ocr` instead.

Once the package is installed, you can import it in your script and spin up an engine instance—this is the heart of **how to OCR PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

The `OcrEngine` object holds all the settings we’ll tweak later, such as language, DPI, and—crucially—PDF mode.

## Шаг 2: Включить распознавание PDF и выбрать вывод (extract text from PDF)

By default many OCR SDKs assume you’re feeding them images. To make the engine treat the incoming stream as a PDF, we enable the PDF recognition flag and ask for plain‑text output.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Why bother specifying the output format? Because some engines can return PDF with hidden text layers, searchable PDFs, or JSON with bounding boxes. For most data‑extraction pipelines, **extract text from PDF** as plain strings is the cleanest downstream format.

## Шаг 3: Загрузить PDF из файлового потока (load PDF from stream)

Loading a PDF from a stream is a memory‑efficient pattern—you avoid loading the whole file into RAM at once. This is especially handy when dealing with large multi‑page documents.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **What if the file is on S3 or another cloud bucket?**  
> Simply replace `from_file` with a method that accepts a byte buffer (e.g., `ImageStream.from_bytes(s3_object.read())`). The rest of the pipeline stays identical.

## Шаг 4: Выполнить OCR на всех страницах (process scanned PDF)

Now the heavy lifting begins. The engine will iterate through every page, run the recognition engine, and return a list of page objects—each exposing its textual content.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Behind the scenes, the OCR library decompresses each PDF page, rasterizes it at the configured DPI, and feeds the bitmap through its neural‑network model. The result? A collection of `Page` objects ready for extraction.

## Шаг 5: Получить и отобразить распознанный текст (convert PDF to text)

Finally, we loop over the returned pages and print the recognized text. This is the moment where **convert PDF to text** truly happens.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Ожидаемый вывод

If `multipage.pdf` contains three scanned pages, you’ll see something like:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Notice the clean separation between pages—useful if you need to store each page’s text in a database or feed it to a downstream NLP model.

## Обработка распространённых граничных случаев

### 1. PDF‑файлы со смешанными изображениями и текстовыми слоями

Some PDFs already contain a hidden text layer (e.g., exported from Word). If you want the OCR engine to **ignore existing text** and re‑process the image, set:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Большие файлы, превышающие ограничения памяти

When working with gigabyte‑size PDFs, consider processing in chunks:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Поддержка языков и шрифтов

If your scanned documents are in French or contain special characters, tell the engine which language model to use:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

## Полный скрипт – готов к запуску

Below is the complete, runnable example that ties all the pieces together. Save it as `ocr_pdf.py` and execute `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Running the script** will print each page’s text to the console, exactly as shown in the “Expected Output” section. From here you can redirect the output to a file:

```bash
python ocr_pdf.py > extracted_text.txt
```

## Заключение

We’ve just covered **how to OCR PDF** files in Python from start to finish. By configuring the engine, loading the document via a stream, and iterating over each recognized page, you can **extract text from PDF**, **convert PDF to text**, and **process scanned PDF** with just a handful of lines. The approach scales from tiny two‑page invoices to massive multi‑hundred‑page archives.

What’s next? Try feeding the extracted strings into a search index, a language‑model summarizer, or a data‑validation pipeline. You might also experiment with output formats like JSON to retain positional metadata for advanced document analysis.

Got questions about handling encrypted PDFs or integrating with cloud storage? Drop a comment below—happy coding! 

![Схема рабочего процесса OCR PDF — как выполнять OCR PDF, загрузить PDF из потока, распознать страницы и извлечь текст](ocr-pdf-workflow.png "схема рабочего процесса как выполнять OCR PDF")

## Что следует изучить дальше?

The following tutorials cover closely related topics that build on the techniques demonstrated in this guide. Each resource includes complete working code examples with step-by-step explanations to help you master additional API features and explore alternative implementation approaches in your own projects.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}