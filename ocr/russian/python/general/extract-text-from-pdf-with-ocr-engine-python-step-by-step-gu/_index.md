---
category: general
date: 2026-01-12
description: Извлечение текста из PDF с помощью OCR‑движка в Python – узнайте, как
  читать PDF с OCR, загружать изображение для OCR и получать структурированные результаты.
draft: false
keywords:
- extract text from pdf
- read pdf with ocr
- load image for ocr
- use ocr engine python
language: ru
og_description: Извлечение текста из PDF с помощью OCR‑движка Python. Этот учебник
  показывает, как читать PDF с OCR, загружать изображение для OCR и использовать OCR‑движок
  Python для надёжных результатов.
og_title: Извлечение текста из PDF с помощью OCR‑движка Python – Полное руководство
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Извлечение текста из PDF с помощью OCR‑движка Python – пошаговое руководство
url: /ru/python/general/extract-text-from-pdf-with-ocr-engine-python-step-by-step-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PDF с помощью OCR Engine Python – Полный учебник

Когда‑нибудь вам нужно было **извлечь текст из PDF**, но файл представляет собой просто отсканированное изображение? Вы не одиноки. Во многих реальных проектах получаемый PDF не содержит выделяемого текста, поэтому единственный путь — **читать PDF с помощью OCR**.  

В этом руководстве мы пройдем практическое, сквозное решение, которое покажет, как именно **загрузить изображение для OCR**, запустить **OCR engine Python** и получить структурированный текст, который можно передать в последующие конвейеры. Никаких расплывчатых ссылок, только полностью готовый к запуску пример, который вы можете скопировать‑вставить уже сегодня.

## Что вы узнаете

- Как установить и импортировать нужную библиотеку OCR для Python.  
- Точные шаги **загрузки изображения для OCR** из PDF‑файла.  
- Как вызвать метод `recognize_structured()` движка и пройтись по блокам, строкам и словам.  
- Советы по работе с результатами низкой уверенности и многостраничными PDF.

К концу этого учебника у вас будет скрипт, надёжно **извлекающий текст из PDF**‑документов, независимо от того, содержит ли он одну страницу или сотню.

---

![Диаграмма извлечения текста из PDF, показывающая шаги обработки OCR.](images/ocr_flow.png "диаграмма извлечения текста из pdf")

*Текст альтернативного изображения: диаграмма извлечения текста из pdf, иллюстрирующая шаги обработки OCR.*

## Требования

- Python 3.9 или новее (код использует f‑строки и подсказки типов).  
- Устанавливаемый через pip пакет OCR, предоставляющий класс `OcrEngine` (например, вымышленная библиотека `pyocr`).  
- PDF‑файл, который вы хотите обработать, сохранённый локально (например, `form.pdf`).  

Если у вас отсутствует библиотека OCR, установите её с помощью:

```bash
pip install pyocr   # replace with the actual package name you use
```

---

## Шаг 1: Извлечение текста из PDF – Настройка OCR Engine

Прежде чем мы сможем **читать PDF с OCR**, нам нужен экземпляр движка. Думайте о движке как о мозге, который смотрит на каждый пиксель и решает, какой символ он представляет.

```python
# Step 1: Import the OCR module and create an engine instance
import ocr  # or `import pyocr as ocr` depending on the package

# Create the OCR engine – this may load language models under the hood
ocr_engine = ocr.OcrEngine()
```

> **Почему это важно:** Инициализация движка один раз позволяет переиспользовать загруженные языковые пакеты для нескольких файлов, экономя и время, и память.

---

## Шаг 2: Загрузка изображения для OCR – Подготовка вашего PDF

PDF не является «сырой» картинкой, поэтому библиотека обычно предоставляет вспомогательную функцию для преобразования первой (или всех) страниц в изображение, понятное OCR‑движку.

```python
# Step 2: Load the PDF page(s) you want to process
# The `load_image` method accepts many formats – PDF, PNG, JPEG, etc.
pdf_path = "YOUR_DIRECTORY/form.pdf"
ocr_engine.load_image(pdf_path)
```

> **Подсказка:** Если ваш PDF содержит несколько страниц, многие OCR‑библиотеки позволяют передать `page=2` или выполнить цикл `engine.load_image(pdf_path, page=n)`. Для больших документов рекомендуется обрабатывать страницы пакетами, чтобы избежать всплесков памяти.

---

## Шаг 3: Использование OCR Engine Python – Распознавание структурированного текста

Теперь происходит основная работа. Вызов `recognize_structured()` возвращает иерархию блоков → строк → слов, каждый из которых аннотирован языком, уровнем уверенности и ограничивающим прямоугольником.

```python
# Step 3: Perform structured text recognition
structured_result = ocr_engine.recognize_structured()
```

> **Что вы получаете:**  
> - `structured_result.blocks` – контейнеры верхнего уровня (обычно абзацы или колонки).  
> - Каждый блок содержит `lines`, а каждая строка – `words`.  
> - Оценки уверенности позволяют отфильтровать сомнительные результаты.

---

## Шаг 4: Итерация по результатам – Доступ к блокам, строкам и словам

Ниже представлен компактный цикл, выводящий самую полезную информацию. При желании расширьте его для записи в JSON, CSV или загрузки в базу данных.

```python
# Step 4: Walk through the hierarchy and display key data
for block_idx, text_block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={text_block.language}, confidence={text_block.confidence:.2f}")

    # Show a sample line from the block, if any
    if text_block.lines:
        sample_line = text_block.lines[0]
        print(f"  Sample line: {sample_line.text}")

        # Show a sample word with its bounding box and confidence
        if sample_line.words:
            sample_word = sample_line.words[0]
            print(
                f"    Sample word: '{sample_word.text}' "
                f"bbox={sample_word.bounding_box} "
                f"conf={sample_word.confidence:.2f}"
            )
```

### Ожидаемый вывод

```
Block 1: language=en, confidence=0.97
  Sample line: Invoice Number: 2025-00123
    Sample word: 'Invoice' bbox=(12,34,78,90) conf=0.99
Block 2: language=en, confidence=0.94
  Sample line: Total Amount: $1,250.00
    Sample word: 'Total' bbox=(15,120,70,155) conf=0.96
...
```

> **Почему вам это понравится:** Иерархия отражает то, как человек читает страницу, что упрощает последующее восстановление таблиц или колонок.

---

## Шаг 5: Обработка граничных случаев – Низкая уверенность и многостраничные PDF

### Слова с низкой уверенностью

Если уверенность слова падает ниже, скажем, `0.70`, вы можете пометить его для ручной проверки:

```python
LOW_CONF_THRESHOLD = 0.70

for block in structured_result.blocks:
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

### Обработка всех страниц

```python
# Example: loop over every page in a multi‑page PDF
for page_number in range(ocr_engine.page_count):
    ocr_engine.load_image(pdf_path, page=page_number)
    result = ocr_engine.recognize_structured()
    # …process `result` just like we did above…
```

> **Профессиональный совет:** Кешируйте промежуточные изображения в PNG, если ваша OCR‑библиотека каждый раз их пере‑рендерит — это может сэкономить секунды при обработке больших пакетов.

---

## Полный рабочий скрипт

Объединив всё вместе, получаем один файл, готовый к запуску:

```python
#!/usr/bin/env python3
"""
Extract text from PDF with OCR engine Python.
This script demonstrates loading a PDF, recognizing structured text,
and printing a concise summary of blocks, lines, and words.
"""

import ocr  # Replace with your actual OCR package import

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
PDF_PATH = "YOUR_DIRECTORY/form.pdf"
LOW_CONF_THRESHOLD = 0.70

# ----------------------------------------------------------------------
# Initialize OCR engine
# ----------------------------------------------------------------------
ocr_engine = ocr.OcrEngine()

# ----------------------------------------------------------------------
# Load the PDF (first page by default)
# ----------------------------------------------------------------------
ocr_engine.load_image(PDF_PATH)

# ----------------------------------------------------------------------
# Recognize structured text
# ----------------------------------------------------------------------
structured_result = ocr_engine.recognize_structured()

# ----------------------------------------------------------------------
# Iterate and display results
# ----------------------------------------------------------------------
for block_idx, block in enumerate(structured_result.blocks, start=1):
    print(f"Block {block_idx}: language={block.language}, confidence={block.confidence:.2f}")

    if block.lines:
        line = block.lines[0]
        print(f"  Sample line: {line.text}")

        if line.words:
            word = line.words[0]
            print(
                f"    Sample word: '{word.text}' "
                f"bbox={word.bounding_box} "
                f"conf={word.confidence:.2f}"
            )

    # Flag low‑confidence words inside the block
    for line in block.lines:
        for word in line.words:
            if word.confidence < LOW_CONF_THRESHOLD:
                print(f"⚠️ Low confidence: '{word.text}' ({word.confidence:.2f})")
```

Сохраните его как `extract_pdf_ocr.py` и выполните:

```bash
python extract_pdf_ocr.py
```

Вы увидите детали уровня блоков, выведенные в консоль, вместе с любыми предупреждениями о низкой уверенности.

---

## Заключение

Мы только что рассмотрели полностью готовый к продакшену способ **извлечения текста из PDF** с помощью **OCR engine Python**. Начиная с установки библиотеки, через **загрузку изображения для OCR**, до **чтения PDF с OCR** и итерации по структурированному выводу — теперь у вас есть переиспользуемый скрипт, который можно адаптировать под любой проект.

Дальнейшие шаги, которые стоит исследовать:

- Экспорт иерархии в JSON для последующих NLP‑конвейеров.  
- Добавление автоматического определения языка для переключения OCR‑моделей «на лету».  
- Интеграция с `pdf2image` для предобработки PDF с сложными макетами.  

Попробуйте его на партии многостраничных счетов‑фактур, отрегулируйте порог уверенности и посмотрите, как быстро можно превратить отсканированные PDF в поисковый, редактируемый текст. Если возникнут проблемы, оставляйте комментарий ниже — удачной OCR‑работы!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}