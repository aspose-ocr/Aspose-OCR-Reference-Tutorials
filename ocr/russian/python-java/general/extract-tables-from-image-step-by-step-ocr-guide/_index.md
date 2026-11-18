---
category: general
date: 2026-03-26
description: Извлекать таблицы из изображения и преобразовывать изображение в таблицу
  с помощью OCR на Python. Узнайте, как загрузить изображение для OCR, читать таблицы
  и извлекать данные таблиц.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: ru
og_description: Извлекайте таблицы из изображения с помощью Python OCR. Это руководство
  показывает, как загрузить изображение для OCR, прочитать таблицы и преобразовать
  их в электронную таблицу.
og_title: Извлечение таблиц из изображения – Полный учебник по OCR
tags:
- OCR
- Python
- Data Extraction
title: Извлечение таблиц из изображения – пошаговое руководство по OCR
url: /ru/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение таблиц из изображения – Полный OCR‑урок

Когда‑нибудь вам нужно было **extract tables from image**, но вы не знали, с чего начать? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда PDF или скриншот содержит табличные данные, которые необходимо превратить в редактируемые строки и столбцы. Хорошая новость? Пара строк кода на Python в сочетании с надёжным OCR‑движком могут за секунды превратить картинку в удобную таблицу.

В этом руководстве мы пройдём процесс загрузки изображения для OCR, запуска распознавания и извлечения каждой строки таблицы. К концу вы сможете **convert image to spreadsheet**, а также увидите, как **ocr read tables** и **ocr extract table data** для дальнейшей обработки. Никакой скрытой магии, только понятный, готовый к запуску код, который вы можете сразу добавить в свой проект.

---

## Что понадобится

Прежде чем погрузиться в детали, убедитесь, что у вас есть следующее:

- **Python 3.9+** – лучше всего использовать последнюю стабильную версию.  
- Библиотека **`ocr`** (или любой совместимый OCR SDK, предоставляющий `OcrEngine`, `Image` и методы, связанные с таблицами). Установите её командой `pip install ocr‑sdk` (замените на реальное название пакета).  
- Файл изображения (`.png`, `.jpg` и т.п.), содержащий чётко напечатанную таблицу.  
- По желанию: **pandas**, если хотите сразу сохранять извлечённые данные в CSV или Excel (`pip install pandas`).

Всё готово? Отлично — приступаем.

---

## Шаг 1: Импорт OCR SDK и подготовка окружения

Сначала нужно импортировать классы OCR в наш скрипт и создать небольшую вспомогательную функцию, которая позже превратит сырые данные таблицы в DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Почему это важно:** Импорт `ocr` даёт доступ к `OcrEngine`, `Imaging.Image` и объектам таблиц, по которым будем итерировать. `pandas` не обязателен для самого извлечения, но делает часть «convert image to spreadsheet» тривиальной.

---

## Шаг 2: Загрузка изображения для обработки

Теперь действительно **load image for OCR**. SDK ожидает объект `Image`, поэтому обернём путь к файлу методом `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Совет:** Храните изображения в отдельной папке (`assets/` или `data/`) и используйте относительные пути. Так скрипт будет портируемым между машинами.

---

## Шаг 3: Запуск процесса распознавания

С прикреплённым изображением мы наконец можем попросить движок **ocr read tables**. Вызов `recognize()` возвращает объект результата, содержащий всё, что нашёл движок — текстовые блоки, строки и, что самое важное для нас, таблицы.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Зачем проверять:** На некоторых изображениях шум или слабые границы таблицы могут привести к пропуску её распознавателем. Вывод предупреждения даст раннюю обратную связь без прерывания скрипта.

---

## Шаг 4: Извлечение строк и ячеек каждой таблицы

Здесь начинается настоящая магия. Мы пройдемся по каждой найденной таблице, вытянем каждую строку, а затем текст каждой ячейки. Внутреннее list‑comprehension делает код лаконичным, но мы всё равно объясним логику.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**Что происходит?**  

- `enumerate(..., start=1)` даёт удобный номер таблицы для логов.  
- `row_obj.get_cells()` возвращает объекты ячеек; `cell.get_text()` получает строку, декодированную OCR.  
- Сохраняем строки в `rows_data`, затем передаём их в `pandas.DataFrame`, который автоматически выравнивает столбцы.  
- Блок `print` отражает **essential output**, показанный в оригинальном фрагменте, чтобы вы могли сразу проверить результаты.

**Обработка граничных случаев:** Если у строки количество ячеек отличается от остальных, `pandas` заполнит недостающие места `NaN`. Позже можно очистить DataFrame с помощью `df.fillna('')`, если нужны пустые строки.

---

## Шаг 5: Сохранение извлечённых таблиц в таблицу

Теперь, когда у нас есть список DataFrame, экспортировать их в Excel‑книгу (или CSV‑файлы) проще простого. Это решает задачу «convert image to spreadsheet».

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Почему Excel?** Большинство бизнес‑пользователей предпочитают `.xlsx`. Если вам нужен CSV, замените цикл на `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Полный готовый к запуску скрипт

Объединив всё вместе, получаем полностью готовую программу, которую можно скопировать и выполнить.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Ожидаемый вывод в консоль** (для простой таблицы 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

Файл `extracted_tables.xlsx` появится в папке скрипта, каждая таблица будет на отдельном листе.

---

## Часто задаваемые вопросы и советы

| Question | Answer |
|----------|--------|
| **Can I use a different OCR library?** | Absolutely. The pattern stays the same: load image → recognize → iterate over `get_tables()`. Just replace the import and object names. |
| **What if my image is noisy?** | Pre‑process with OpenCV (thresholding, deskew) before feeding it to the OCR engine. Noise reduction often improves **ocr extract table data** accuracy. |
| **Do I need to install `openpyxl`?** | Yes, `pandas` uses it under the hood for Excel output. Install with `pip install openpyxl`. |
| **How do I handle merged cells?** | Some SDKs expose `cell.is_merged()`; you can detect and propagate the value across the merged range manually. |
| **Is there a way to extract only specific tables?** | Filter by `table_obj.get_confidence()` or by checking header keywords before processing. |

---

## Итоги

Теперь у вас есть полное сквозное решение для **extract tables from image**, преобразующее результат в аккуратную таблицу и умеющее работать с несколькими таблицами на одном изображении. Скрипт демонстрирует, как **load image for OCR**, **ocr read tables** и **ocr extract table data**, оставаясь гибким для реальных условий.

Что дальше? Попробуйте подать в OCR‑движок страницу PDF, преобразованную в изображение, или поэкспериментируйте с разными языками и шрифтами. Вы также можете напрямую передавать DataFrame в базу данных или в систему отчётности — границы только у вашего воображения.

Если руководство оказалось полезным, поделитесь им, поставьте звёздочку репозиторию SDK или оставьте комментарий со своими приёмами. Приятного кодинга, и пусть ваши таблицы всегда парсятся без ошибок!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}