---
category: general
date: 2026-07-05
description: Извлечение таблицы из изображения с помощью Python OCR. Узнайте, как
  извлечь таблицу, преобразовать изображение в TSV и освоить техники OCR таблиц в
  Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: ru
og_description: Извлеките таблицу из изображения с помощью Python OCR. Это руководство
  показывает, как извлечь таблицу, преобразовать изображение в TSV и использовать
  инструменты OCR‑таблиц на Python.
og_title: Извлечь таблицу из изображения — преобразовать изображение в TSV на Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Извлечение таблицы из изображения – преобразование изображения в TSV на Python
url: /ru/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение таблицы из изображения – Конвертация изображения в TSV на Python

Задумывались когда‑нибудь, как извлечь таблицу из изображения, не теряя волосы? В этом руководстве мы пройдемся по **как извлечь таблицу** данным из картинки, используя библиотеку `aocr`, а затем превратим эти данные в аккуратный TSV‑файл. Никакой магии, лишь несколько строк кода на Python и немного AI‑поддерживаемой пост‑обработки.

Если вы когда‑либо пытались скопировать‑вставить таблицу из отсканированного счета или скриншота и получали путаный набор данных, вы оцените, почему подход на основе OCR стоит освоить. К концу вы сможете передать любое изображение таблицы в Python и получить чистые табличные значения, готовые для электронных таблиц или баз данных.

---

## Что понадобится

Перед тем как начать, убедитесь, что у вас есть следующее:

| Требование | Зачем это нужно |
|------------|-----------------|
| Python 3.9+ | Пакет `aocr` ориентирован на современные версии Python. |
| `aocr` library (`pip install aocr`) | Предоставляет OCR‑движок и AI‑пост‑процессор, которые мы будем использовать. |
| An image file containing a table (PNG, JPG, etc.) | Исходные данные, которые будем извлекать. |
| Optional: a virtual environment | Изолирует зависимости — настоятельно рекомендуется. |

Наличие этих компонентов избавит вас от прерываний посередине руководства.

---

## Установка зависимостей

Сначала установим инструменты OCR. Откройте терминал и выполните:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Pro tip:** Если вы столкнулись с ошибками доступа, добавьте `--user` к команде `pip install` или используйте `pipx` для глобальной установки.

---

## Шаг 1 – Инициализация OCR‑движка

Движок – сердце процесса. Представьте его как «мозг», который смотрит на каждый пиксель и решает, какой символ где находится.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Почему мы создаём объект движка, а не вызываем одну функцию? Объект движка позволяет позже прикрепить пользовательские пост‑процессоры, давая тонкий контроль над выводом — это необходимо, когда вам нужна точность **ocr table image python**.

---

## Шаг 2 – Подключение AI‑пост‑процессора

`aocr` поставляется с лёгким AI‑пост‑процессором, который очищает сырые результаты OCR, сохраняя границы ячеек. Дополнительные аргументы не требуются, что делает код аккуратным.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Если пропустить этот шаг, вы всё равно получите сырый текст, но структура таблицы будет шумной — представьте себе электронную таблицу, где каждая ячейка — загадка. Пост‑процессор берёт на себя тяжёлую работу по выравниванию текста в исходную сетку.

---

## Шаг 3 – Загрузка изображения таблицы

Вы можете загрузить изображение из любого пути, но для ясности будем использовать каталог‑заполнитель. Замените `"YOUR_DIRECTORY/invoice_table.png"` на фактический путь к вашему файлу.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Note:** `aocr.Image` автоматически определяет формат изображения и нормализует цветовые каналы, поэтому предварительная обработка файла не нужна, если только он не сильно повреждён.

---

## Шаг 4 – Выполнение структурированного OCR

Теперь движок сканирует изображение и возвращает объект сырой таблицы. Этот объект содержит строки, столбцы и сырой текст каждой ячейки.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Почему использовать `recognize_structured` вместо обычного вызова `recognize`? Структурированный вариант пытается определить границы строк/столбцов, предоставляя матричный результат, который гораздо проще преобразовать в TSV позже.

---

## Шаг 5 – Очистка данных с помощью AI‑пост‑процессора

Запуск пост‑процессора уточняет сырые результаты: он удаляет лишние символы, объединяет разбитые фрагменты и гарантирует правильное выравнивание текста в каждой ячейке.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Если вы посмотрите `processed_table.table`, вы увидите список строк, где каждая строка — это список объектов `Cell`. Каждый `Cell` имеет атрибут `.text`, содержащий очищенную строку.

---

## Шаг 6 – Экспорт таблицы в TSV

Последний шаг — превратить обработанные данные в файл с табличными значениями (TSV) — именно то, что нужно, когда вы хотите **convert image to TSV** для Excel или Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Запуск скрипта выводит каждую строку в консоль (если хотите) и записывает чистый TSV‑файл, который можно открыть в любой программе для работы с таблицами.

### Быстрая проверка

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Вы должны увидеть аккуратно выровненные столбцы, например:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Если вывод выглядит перемешанным, проверьте качество изображения (резкость, контраст) и подумайте о настройке параметров OCR‑движка — `engine.set_config(...)` позволяет менять языковые модели и пороги уверенности.

---

## Обработка распространённых граничных случаев

| Ситуация | Рекомендуемое решение |
|----------|-----------------------|
| **Skewed image** | Предварительно поверните с помощью `Pillow` (`Image.rotate`) перед передачей в `aocr`. |
| **Low contrast** | Примените гистограммное выравнивание (`cv2.equalizeHist`) для повышения читаемости. |
| **Merged cells** | Пост‑обработайте TSV, разделив ячейки по известным разделителям, или используйте флаг `merge_cells=False`, если он доступен. |
| **Multi‑page PDFs** | Сначала конвертируйте каждую страницу в изображение (`pdf2image`) и запустите конвейер в цикле. |

Эти настройки делают ваш рабочий процесс **ocr table image python** надёжным при работе с разными источниками.

---

## Полный скрипт – Универсальное решение

Ниже представлен полностью готовый к запуску скрипт, объединяющий все обсуждённые шаги. Сохраните его как `extract_table.py` и выполните `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Извлечение текста из изображения с помощью Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как извлечь таблицу из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Как извлечь текст из изображения, подготовив прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}