---
category: general
date: 2026-01-02
description: Узнайте, как исправлять наклон изображения и повышать контраст, чтобы
  быстро получить чистый текст. Включает пошаговый код на Python и советы по извлечению
  текста.
draft: false
keywords:
- how to deskew image
- boost image contrast
- get plain text
- how to boost contrast
- how to extract text
language: ru
og_description: Как исправить наклон изображения и повысить контраст для получения
  чистого текста. Полный пример на Python с извлечением таблиц и ускорением на GPU.
og_title: Как исправить наклон изображения – Полный учебник по OCR на GPU
tags:
- OCR
- Python
- Image Processing
title: Как выпрямить изображение — Руководство по OCR с ускорением на GPU
url: /ru/python-java/general/how-to-deskew-image-gpu-accelerated-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как исправить наклон изображения – Руководство по OCR с ускорением на GPU

Задумывались ли вы когда‑нибудь **как исправить наклон изображения**, когда ваши чеки приходят под странным углом? Вы не одиноки; наклонённое фото может превратить полностью читаемый чек в беспорядочный набор. Хорошая новость в том, что с помощью нескольких строк кода на Python вы можете автоматически исправить наклон, увеличить контраст и получить чистый простой текст — без ручного использования Photoshop.  

В этом руководстве мы пройдём полный, готовый к запуску пример, который не только показывает **как исправить наклон изображения**, но и демонстрирует **как увеличить контраст**, **как получить простой текст**, а также **как извлечь текст** из таблиц, обнаруженных OCR‑движком. К концу вы получите автономный скрипт, который можно вставить в любой проект.

## Что понадобится

- Python 3.9+ установленный (код использует подсказки типов, поэтому рекомендуется современный интерпретатор)
- Библиотека `ocr`, предоставляющая `OcrEngine`, `EngineMode`, `ImageProcessingOptions` и `OcrResult` (установите через `pip install ocr‑sdk` – замените на фактическое название пакета, который используете)
- GPU с совместимыми драйверами, если хотите ускорить процесс (необязательно, но рекомендуется)
- Файл изображения, слегка повернутый или с низким контрастом, например `receipt_skewed.jpg`

> **Pro tip:** Если у вас нет GPU, просто замените `EngineMode.GPU` на `EngineMode.CPU`, и скрипт всё равно будет работать — просто немного медленнее.

## Пошаговая реализация

Ниже мы разбиваем решение на логические части. Каждая часть имеет описательный **H2**, содержащий основной ключевой запрос *как исправить наклон изображения* или один из вторичных запросов. Код полностью готов к запуску, прокомментирован и готов к использованию.

### Как исправить наклон изображения с помощью OCR, ускоренного GPU

Первое, что мы делаем, — указываем OCR‑движку работать на GPU и включаем функцию авто‑исправления наклона. Авто‑исправление анализирует геометрию изображения и вращает его обратно в вертикальное положение.

```python
# Import the required classes from the OCR SDK
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

# Step 1: Initialize the OCR engine with GPU acceleration
ocr_engine = OcrEngine()
ocr_engine.set_engine_mode(EngineMode.GPU)  # Enables GPU backend for faster processing
```

> **Почему это важно:** Ускорение на GPU может сократить время обработки с секунд до миллисекунд, что критично, когда вы обрабатываете десятки чеков в минуту.

### Увеличить контраст изображения для лучшего распознавания

Чек с низким контрастом — кошмар для любой OCR‑системы. Увеличивая контраст, мы даём движку более чёткие границы для работы.

```python
# Step 2: Configure image preprocessing (auto‑deskew and contrast boost)
processing_options = ImageProcessingOptions()
processing_options.set_auto_deskew(True)          # Corrects slight rotation
processing_options.set_contrast_boost(30)         # Improves readability
ocr_engine.set_image_processing_options(processing_options)
```

> **Как увеличить контраст:** Метод `set_contrast_boost` принимает процент; 30 % — безопасное значение по умолчанию, которое подходит для большинства отсканированных чеков. Если ваши изображения очень тёмные, поднимите до 50 % или экспериментируйте.

### Получить простой текст из обработанного изображения

Теперь, когда изображение выровнено и ярко, мы передаём его движку и запрашиваем результат в виде простого текста.

```python
# Step 3: Load the target image and perform OCR
image_path = "YOUR_DIRECTORY/receipt_skewed.jpg"
ocr_result: OcrResult = ocr_engine.recognize_image(image_path)

# Step 4: Output the recognized plain text
print("Detected text:")
print(ocr_result.get_text())
```

**Ожидаемый вывод (усечённый для краткости):**

```
Detected text:
Store: Coffee Corner
Date: 2025-12-31
Item          Qty   Price
Latte          1    $3.50
Muffin         2    $5.00
Total                $8.50
```

> **Как получить простой текст:** Метод `get_text()` удаляет любую информацию о макете и возвращает чистую строку, которую вы можете сохранить в базе данных, отправить в API или передать в последующий аналитический процесс.

### Как извлечь текст из обнаруженных таблиц

Часто в чеках присутствуют табличные данные (товары, количество, цены). OCR‑SDK может обнаруживать таблицы и позволять проходить по строкам и ячейкам.

```python
# Step 5: If tables are detected, print their contents
if ocr_result.get_tables():
    for idx, table in enumerate(ocr_result.get_tables()):
        print(f"\nTable {idx + 1}:")
        for row in table.get_rows():
            # Join each cell's text with a tab for easy copy‑paste
            print("\t".join(cell.get_text() for cell in row.get_cells()))
```

**Пример вывода таблицы**:

```
Table 1:
Item	Qty	Price
Latte	1	$3.50
Muffin	2	$5.00
Total		$8.50
```

> **Почему извлекать таблицы:** Структурированные данные упрощают подсчёт итогов, генерацию отчётов или передачу в бухгалтерское программное обеспечение.

### Полный рабочий скрипт

Объединив всё вместе, получаем скрипт, который можно скопировать в файл `deskew_and_ocr.py`:

```python
# deskew_and_ocr.py
from ocr import OcrEngine, EngineMode, ImageProcessingOptions, OcrResult

def main(image_path: str) -> None:
    # Initialize OCR engine with GPU acceleration
    ocr_engine = OcrEngine()
    ocr_engine.set_engine_mode(EngineMode.GPU)

    # Configure preprocessing: auto‑deskew + contrast boost
    opts = ImageProcessingOptions()
    opts.set_auto_deskew(True)
    opts.set_contrast_boost(30)  # Adjust if needed
    ocr_engine.set_image_processing_options(opts)

    # Perform OCR
    result: OcrResult = ocr_engine.recognize_image(image_path)

    # Print plain text
    print("Detected text:")
    print(result.get_text())

    # Print tables, if any
    if result.get_tables():
        for i, tbl in enumerate(result.get_tables(), start=1):
            print(f"\nTable {i}:")
            for row in tbl.get_rows():
                print("\t".join(cell.get_text() for cell in row.get_cells()))

if __name__ == "__main__":
    # Replace with your actual image location
    main("YOUR_DIRECTORY/receipt_skewed.jpg")
```

Запустите его с помощью:

```bash
python deskew_and_ocr.py
```

Вы должны увидеть очищенный текст и любые обнаруженные таблицы, выведенные в консоль.

## Распространённые граничные случаи и как с ними справиться

| Ситуация | Что делать |
|-----------|------------|
| **Изображение перевёрнуто вверх ногами** | Повысить уверенность `set_auto_deskew(True)`, также вызвав `set_rotation_correction(True)`, если SDK это поддерживает. |
| **Увеличение контраста делает изображение слишком ярким** | Уменьшить процент, передаваемый в `set_contrast_boost` (например, 15 %). |
| **GPU недоступен** | Переключить `EngineMode.GPU` на `EngineMode.CPU`; остальная часть конвейера остаётся без изменений. |
| **Таблицы не обнаружены** | Попробовать сканировать с более высоким разрешением или включить `set_table_detection(True)`, если библиотека предоставляет эту опцию. |

## Следующие шаги: от простого текста к структурированным данным

Теперь, когда вы знаете **как исправить наклон изображения**, **как увеличить контраст** и **как получить простой текст**, вы можете:

- Разбирать простой текст с помощью регулярных выражений, чтобы извлекать пары «ключ‑значение» (например, `total`, `date`).
- Сохранять результаты в базе данных SQLite или PostgreSQL для последующей отчётности.
- Подключить скрипт к безсерверной функции (AWS Lambda, Azure Functions) для автоматической обработки загрузок.

Все эти расширения опираются на ту же основу, которую мы рассмотрели здесь.

## Заключение

Мы прошли процесс **как исправить наклон изображения** с использованием OCR‑движка, ускоренного GPU, продемонстрировали **как увеличить контраст** для более чёткого распознавания, показали точно **как получить простой текст**, а также рассмотрели **как извлечь текст** из таблиц. Полный, готовый к запуску скрипт связывает всё вместе, так что вы можете вставить его в любой Python‑проект и сразу начать извлекать чистые данные из наклонённых, низкоконтрастных фотографий.

Попробуйте на нескольких своих чеках, отрегулируйте уровень контраста и позвольте OCR выполнить тяжёлую работу. Если столкнётесь с проблемами, обратитесь к таблице граничных случаев выше — большинство вопросов решаются небольшими настройками.

Счастливого кодинга, и пусть ваши изображения всегда будут ровными и яркими!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}