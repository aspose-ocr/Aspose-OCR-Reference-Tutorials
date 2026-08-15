---
category: general
date: 2026-03-26
description: Как извлечь текст из PDF с помощью OCR. Узнайте, как загрузить PDF как
  изображение, распознать текст в PDF и извлечь его с простым примером на Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: ru
og_description: Как извлечь текст из PDF с помощью OCR. Это руководство покажет, как
  загрузить PDF как изображение, распознать текст в PDF и извлечь текст из PDF в Python.
og_title: Как извлечь текст из PDF с помощью OCR – Полное руководство
tags:
- OCR
- Python
- PDF processing
title: Как извлечь текст из PDF с помощью OCR – Полное пошаговое руководство
url: /ru/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь текст из PDF с помощью OCR – Полное пошаговое руководство

Когда‑то задумывались **как извлечь PDF**‑файлы, которые на самом деле являются просто отсканированными изображениями? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда им нужен индексируемый контент, а есть лишь PDF‑файлы, содержащие только изображения. Хорошая новость? Пара строк кода и надёжная OCR‑библиотека могут за секунды превратить такие «картинки‑PDF» в обычный текст.  

В этом руководстве мы пройдёмся по **использованию OCR** для загрузки PDF как изображения, распознавания текста в PDF и, наконец, **извлечения текста из PDF** любого объёма. К концу вы получите готовый скрипт, понятное объяснение каждого шага и несколько советов, как избежать типичных подводных камней.

## Что понадобится

- Python 3.9 или новее (код также работает на 3.10+)  
- Пакет `ocr` для Python (или любая совместимая OCR‑библиотека, предоставляющая `OcrEngine`, `OcrEngineMode` и `Imaging.Image`)  
- Многостраничный PDF, который нужно обработать (для примера назовём его `multi_page.pdf`)  
- Базовые знания о виртуальных окружениях (необязательно, но рекомендуется)

> **Pro tip:** Если вы работаете в Windows, удобно использовать Anaconda Prompt; в macOS/Linux достаточно выполнить `python -m venv venv && source venv/bin/activate`.

## Шаг 1: Установите OCR‑библиотеку

Сначала скачайте OCR‑пакет с PyPI. В примере ниже используется вымышленный пакет `ocr`, который имитирует API, показанное в коде, но большинство реальных библиотек (например, `pytesseract` + `pdf2image`) работают по тому же принципу.

```bash
pip install ocr
```

Если вы используете другой движок, замените `ocr` на соответствующее название (например, `pip install pytesseract pdf2image`).

## Шаг 2: Инициализируйте OCR‑движок

Создание экземпляра движка — фундамент **как извлечь PDF**‑текст. Движок выступает в роли «мозгов», которые интерпретируют пиксели каждой страницы PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Почему это важно:** `set_engine_mode` позволяет балансировать между скоростью и точностью. `DEFAULT` — сбалансированный вариант; если нужна более высокая точность, переключитесь на `HIGH_ACCURACY` (если библиотека поддерживает такой режим).

## Шаг 3: Загрузите PDF как объект изображения

OCR работает с изображениями, а не с контейнерами PDF, поэтому сначала нужно преобразовать PDF в изображение. Метод `Imaging.Image.load` автоматически обрабатывает многостраничные PDF.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Особый случай:** Некоторые библиотеки принимают только одно‑страничные изображения. В таком случае придётся проходить по каждой странице с помощью `pdf2image.convert_from_path`. Наш вызов `load` скрывает эту сложность, делая **load pdf as image** одно‑строчным.

## Шаг 4: Распознайте текст на всех страницах

Теперь переходим к основной части **recognize PDF text**. Движок сканирует каждую страницу и возвращает список объектов‑результатов — по одному на страницу.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Каждый `page_result` содержит методы вроде `get_text()` (обычный текст) и `get_confidence()` (необязательная метрика качества).  

> **Совет:** Если нужен только первый лист, вызовите `recognize(pdf_image[0])` вместо вспомогательной функции для многостраничных документов.

## Шаг 5: Пройдитесь по результатам и выведите извлечённый текст

Наконец, перебираем результаты, выводя текст каждой страницы. Это завершает рабочий процесс **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Ожидаемый вывод

Если в `multi_page.pdf` три страницы со словами «Hello», «World» и «Python», вы увидите:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

Вот и всё — ваш PDF теперь полностью индексируем, а текст готов к дальнейшей обработке (индексация, анализ тональности и т.д.).

## Шаг 6: Обработка распространённых проблем

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Пустой вывод** | Страницы отсканированы с низким DPI, символы неразличимы. | Увеличьте разрешение перед OCR: `pdf_image = pdf_image.resize(300)` (300 DPI — оптимальный вариант). |
| **Непонятные символы** | Для нелатинских алфавитов нужны языковые пакеты. | Загрузите нужную языковую модель: `ocr_engine.load_language('spa')` для испанского и т.д. |
| **Переполнение памяти при больших PDF** | Одновременная загрузка всех страниц съедает ОЗУ. | Обрабатывайте страницы партиями: `for img in pdf_image.split(batch=10): …` (псевдокод). |
| **Низкая производительность** | Использование `DEFAULT` на огромном документе может быть медленным. | Переключитесь в режим `FAST` или запустите OCR параллельно через `concurrent.futures`. |

## Бонус: Сохранение извлечённого текста в файл

В реальных проектах часто требуется сохранять текст. Ниже небольшая утилита, которая записывает всё в `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Теперь `output.txt` можно передать в поисковый движок, базу данных или любую NLP‑модель.

## Собираем всё вместе — полный скрипт

Ниже полностью готовая к запуску программа. Скопируйте‑вставьте, поправьте пути к файлам, и всё готово.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Запустите её:

```bash
python extract_pdf_ocr.py
```

Вы увидите содержимое каждой страницы в консоли, а затем подтверждение создания файла `extracted_text.txt`.

## Заключение

Мы рассмотрели **как извлечь PDF**‑текст из документов, содержащих только изображения, используя OCR‑движок: от установки библиотеки до работы с многостраничными результатами и сохранения вывода. Теперь вы знаете **как использовать OCR**, **как загрузить PDF как изображение** и **как надёжно распознать PDF‑текст**.  

Что дальше? Попробуйте переключить режим движка на более точный, поэкспериментируйте с языковыми пакетами для многоязычных PDF или передайте извлечённый текст в полнотекстовый поисковый индекс, например Elasticsearch. Возможности безграничны, как только вы освоите базовые принципы извлечения текста из PDF‑файлов.

---

![how to extract pdf example](images/ocr_flowchart.png){alt="как извлечь pdf рабочий процесс диаграмма"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}