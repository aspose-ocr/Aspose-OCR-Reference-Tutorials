---
category: general
date: 2026-07-05
description: Конвертировать PDF в текст с помощью Python OCR. Узнайте, как извлекать
  текст из PDF, выполнять пакетную обработку OCR и загружать PDF для OCR в несколько
  простых шагов.
draft: false
keywords:
- convert pdf to text
- extract text from pdf
- batch ocr processing
- load pdf for ocr
- recognize scanned pdf
language: ru
og_description: Быстро преобразуйте PDF в текст. Этот учебник показывает, как извлекать
  текст из PDF, выполнять пакетную обработку OCR и распознавать отсканированные PDF‑файлы
  с помощью Python.
og_title: Конвертировать PDF в текст с помощью OCR на Python – пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  headline: Convert PDF to Text with Python OCR – Complete Guide
  type: TechArticle
- description: Convert PDF to text using Python OCR. Learn how to extract text from
    PDF, perform batch OCR processing, and load PDF for OCR in a few easy steps.
  name: Convert PDF to Text with Python OCR – Complete Guide
  steps:
  - name: '**Chunked Loading** – Some libraries let you load a range of pages:'
    text: '**Chunked Loading** – Some libraries let you load a range of pages:'
  - name: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
    text: '**Streaming to Disk** – Write each page’s text directly to a file instead
      of keeping the entire list in memory.'
  - name: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
    text: '**Sanity Check** – Open a generated `.txt` file and verify that the first
      few lines match the original document’s header.'
  - name: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
    text: '**Performance Test** – Time the script on a 100‑page PDF using the `time`
      command. If it takes longer than expected, consider enabling the library’s multi‑threading
      flag (often `engine.set_threads(4)`).'
  - name: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
    text: '**Quality Assurance** – Compare the OCR output against a manually typed
      excerpt using a diff tool. Aim for >95 % character accuracy for clean scans.'
  type: HowTo
tags:
- OCR
- Python
- PDF
title: Преобразовать PDF в текст с помощью Python OCR – Полное руководство
url: /ru/python-java/general/convert-pdf-to-text-with-python-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Конвертация PDF в текст с помощью Python OCR – Полное руководство

Когда‑нибудь задавались вопросом, как **конвертировать PDF в текст** без особых усилий? Возможно, у вас есть стопка отсканированных контрактов, счетов или научных статей, и вам нужна версия в виде обычного текста для индексации или анализа. Хорошая новость — несколько строк кода на Python справятся с этой задачей.

В этом руководстве мы пройдем практическое решение, которое не только **конвертирует pdf в текст**, но и покажет, как **извлекать текст из pdf**, настроить **пакетную обработку OCR** и корректно **загружать pdf для OCR**. К концу вы получите готовый к запуску скрипт, способный **распознавать отсканированные pdf** страницы за один проход.

## Что вы узнаете

- Установить и настроить библиотеку Python OCR (мы будем использовать условный пакет `ocr` для иллюстрации).  
- Загрузить многостраничный PDF и передать его OCR‑движку.  
- Итерировать результаты, чтобы вывести или сохранить извлечённый текст.  
- Обрабатывать типичные крайние случаи, такие как большие файлы, зашифрованные PDF и документы с несколькими языками.  

Никаких тяжёлых GUI‑инструментов, без ручного копирования — только чистый код, который можно вставить в CI‑конвейер или настольную утилиту.

![Конвертация PDF в текст с помощью Python OCR](https://example.com/images/convert-pdf-to-text.png "Конвертация PDF в текст с помощью Python OCR")

## Необходимые условия

Прежде чем погрузиться, убедитесь, что у вас есть:

| Требование | Почему это важно |
|-------------|-------------------|
| Python 3.9+ | Современный синтаксис, подсказки типов и лучшая производительность. |
| `ocr` library (or a wrapper around Tesseract) | Предоставляет классы `OcrEngine`, `Language` и `Image`, используемые в примере. |
| A multi‑page scanned PDF (e.g., `contract.pdf`) | Это источник, который вы будете **load pdf for OCR**. |
| Basic command‑line familiarity | Для установки пакетов и запуска скрипта. |

Если вы используете Tesseract под капотом, установите его через менеджер пакетов вашей ОС (`apt-get install tesseract-ocr` в Linux, `brew install tesseract` в macOS). Затем добавьте Python‑обёртку:

```bash
pip install ocr  # replace with the actual package name, e.g., pytesseract-wrapper
```

## Шаг 1: Создайте OCR‑движок и задайте язык распознавания

Сначала нам нужен экземпляр OCR‑движка. Установка языка на английский — обычный вариант по умолчанию, но позже вы можете переключиться на другие поддерживаемые языки.

```python
import ocr  # hypothetical import; replace with your actual OCR package

# Initialize the OCR engine
engine = ocr.OcrEngine()

# Choose the language for recognition – ENGLISH works for most contracts
engine.language = ocr.Language.ENGLISH
```

**Почему это важно:** Движок — это мозг, интерпретирующий пиксельные данные. Явно задавая `engine.language`, вы избегаете накладных расходов на определение языка на каждой странице, что значительно ускоряет **batch OCR processing**.

## Шаг 2: Загрузите PDF‑документ для OCR

Теперь мы загружаем PDF в память. Метод `ocr.Image.load` может принимать путь к файлу и возвращает объект, понятный движку.

```python
# Path to your scanned PDF; adjust as needed
pdf_path = "YOUR_DIRECTORY/contract.pdf"

# Load the PDF – this step **load pdf for OCR**
pdf_document = ocr.Image.load(pdf_path)
```

**Полезный совет:** Если ваш PDF защищён паролем, большинство библиотек позволяют передать аргумент `password`. Обработка этого заранее предотвращает появление непонятной ошибки «cannot open file» позже.

## Шаг 3: Запустите OCR на всех страницах — распознайте отсканированный PDF за один вызов

Запуск OCR постранично может быть медленным, особенно для больших документов. Метод `recognize_multi_page` выполняет **batch OCR processing** внутри, используя несколько потоков, когда это возможно.

```python
# Execute OCR across every page; returns a list of OcrResult objects
page_results = engine.recognize_multi_page(pdf_document)  # List<OcrResult>
```

**Что происходит под капотом?** Движок передаёт каждую страницу в базовый OCR‑движок (например, Tesseract), собирает текст и оборачивает его в `OcrResult`. Такой подход уменьшает нагрузку ввода‑вывода и предоставляет удобный способ **extract text from pdf** позже.

## Шаг 4: Итерируйте результаты и выводите распознанный текст

Наконец, мы проходим по каждому `OcrResult` и выводим текст. Вы также можете записать каждую страницу в отдельный файл `.txt` или объединить их в один документ.

```python
for page_number, result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(result.text)
    # Optional: save to a file
    # with open(f"page_{page_number}.txt", "w", encoding="utf-8") as f:
    #     f.write(result.text)
```

**Зачем использовать enumerate?** Применяя `enumerate(..., start=1)`, вы получаете человекочитаемый номер страницы, что удобно, когда позже нужно сослаться на конкретный раздел оригинального PDF.

### Ожидаемый вывод

Запуск скрипта на 3‑страничном контракте может дать такой результат:

```
--- Page 1 ---
THIS AGREEMENT is made on the 1st day of January 2024...
--- Page 2 ---
WHEREAS, the Parties desire to...
--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed...
```

Если страница не содержит распознаваемого текста, соответствующее `result.text` будет пустой строкой — идеально для обнаружения пустых или только‑изображений страниц.

## Обработка больших PDF и ограничения памяти

Обработка PDF из 500 страниц может исчерпать ОЗУ, если загружать всё сразу. Вот две стратегии:

1. **Chunked Loading** — Некоторые библиотеки позволяют загружать диапазон страниц:

   ```python
   for start in range(0, total_pages, 50):  # process 50 pages at a time
       chunk = pdf_document.select_pages(start, start + 49)
       chunk_results = engine.recognize_multi_page(chunk)
       # handle chunk_results as before
   ```

2. **Streaming to Disk** — Записывайте текст каждой страницы напрямую в файл вместо того, чтобы хранить весь список в памяти.

Обе техники позволяют вашему процессу **convert pdf to text** масштабироваться.

## Обработка ошибок и крайних случаев

- **Encrypted PDFs** — Передайте пароль в `Image.load`:

  ```python
  pdf_document = ocr.Image.load(pdf_path, password="mySecret")
  ```

- **Mixed Languages** — Переключайте язык для каждой страницы, если обнаружите иной скрипт:

  ```python
  if detect_spanish(result.text):
      engine.language = ocr.Language.SPANISH
  ```

- **Low‑Resolution Scans** — Предобрабатывайте изображения с помощью библиотеки, такой как `Pillow`, чтобы увеличить контраст перед OCR. Это может значительно улучшить качество шага **recognize scanned pdf**.

## Полный скрипт: Конвертация PDF в текст за один запуск

Ниже представлен полный, готовый к выполнению скрипт, объединяющий всё вместе. Сохраните его как `pdf_to_text.py` и запустите `python pdf_to_text.py`.

```python
#!/usr/bin/env python3
"""
convert_pdf_to_text.py

A self‑contained script that demonstrates how to convert PDF to text using
Python OCR. It covers loading the PDF, batch processing, and handling common
edge cases.
"""

import os
import ocr  # Replace with your actual OCR package

def convert_pdf_to_text(pdf_path: str, output_dir: str = "output"):
    """Convert a scanned PDF into plain‑text files, one per page."""
    if not os.path.isfile(pdf_path):
        raise FileNotFoundError(f"PDF not found: {pdf_path}")

    os.makedirs(output_dir, exist_ok=True)

    # Step 1 – create engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – load PDF (supports password argument if needed)
    pdf_document = ocr.Image.load(pdf_path)

    # Step 3 – run batch OCR
    page_results = engine.recognize_multi_page(pdf_document)

    # Step 4 – write each page's text to a file
    for page_number, result in enumerate(page_results, start=1):
        page_text = result.text.strip()
        out_file = os.path.join(output_dir, f"page_{page_number}.txt")
        with open(out_file, "w", encoding="utf-8") as f:
            f.write(page_text)

        # Also echo to console for quick sanity check
        print(f"--- Page {page_number} ---")
        print(page_text[:200] + ("…" if len(page_text) > 200 else ""))

if __name__ == "__main__":
    # Example usage – adjust the path to your PDF file
    PDF_PATH = "YOUR_DIRECTORY/contract.pdf"
    convert_pdf_to_text(PDF_PATH)
```

**Запуск скрипта** создаст папку `output`, содержащую `page_1.txt`, `page_2.txt` и т.д., эффективно **extract text from pdf** структурированным способом.

## Тестирование решения

1. **Sanity Check** — Откройте сгенерированный файл `.txt` и проверьте, что первые несколько строк соответствуют заголовку оригинального документа.  
2. **Performance Test** — Замерьте время выполнения скрипта на PDF из 100 страниц с помощью команды `time`. Если он работает дольше ожидаемого, рассмотрите включение флага многопоточности библиотеки (обычно `engine.set_threads(4)`).  
3. **Quality Assurance** — Сравните вывод OCR с вручную набранным отрывком, используя инструмент diff. Стремитесь к точности более 95 % символов для чистых сканов.

## Следующие шаги и связанные темы

- **Improve Accuracy**: Поэкспериментируйте с `engine.dpi = 300` или примените предобработку изображений (выравнивание, шумоподавление) перед OCR.  
- **Searchable PDFs**: Используйте библиотеку PDF (например, `PyPDF2` или `pdfplumber`) для встраивания извлечённого текста обратно в оригинальный PDF, делая его поисковым.  
- **Natural Language Processing**: Передайте извлечённый текст в spaCy или NLTK для извлечения сущностей, анализа тональности или тегирования ключевых слов.  
- **Automation Pipelines**: Скомбинируйте этот скрипт с `watchdog` для мониторинга папки и автоматической **convert pdf to text** каждый раз, когда появляется новый файл.

Освоив эти шаблоны, вы сможете

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}