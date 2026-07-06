---
category: general
date: 2026-06-19
description: Извлекайте текст из изображений в Python с помощью простого OCR‑движка.
  Узнайте, как преобразовать отсканированные изображения в текст, распознавать текст
  на фотографиях и эффективно перечислять файлы изображений в Python.
draft: false
keywords:
- extract text from images
- convert scanned images to text
- recognize text from pictures
- list image files python
language: ru
og_description: Извлекайте текст из изображений в Python с помощью лёгкого OCR‑движка.
  Это руководство покажет, как преобразовать отсканированные изображения в текст,
  распознать текст на фотографиях и перечислить файлы изображений в Python за несколько
  шагов.
og_title: Извлечение текста из изображений в Python — Полное руководство по пакетному
  OCR
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Extract text from images in Python with a simple OCR engine. Learn
    how to convert scanned images to text, recognize text from pictures, and list
    image files python efficiently.
  headline: Extract Text from Images in Python – Full Batch OCR Guide
  type: TechArticle
tags:
- Python
- OCR
- Image Processing
title: Извлечение текста из изображений в Python – Полное руководство по пакетному
  OCR
url: /ru/python-java/general/extract-text-from-images-in-python-full-batch-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображений в Python – Полное руководство по пакетному OCR

Когда‑то вам нужно **извлечь текст из изображений**, но вы не знали, с чего начать? Вы не одиноки — разработчики постоянно сталкиваются с задачей преобразования отсканированных PDF, сфотографированных чеков или скриншотов в поисковый текст. В этом руководстве мы пройдём через полностью готовый к запуску пример, показывающий, как **преобразовать отсканированные изображения в текст**, распознавать текст на картинках и даже **list image files python**‑style. К концу вы получите переиспользуемый скрипт, который обрабатывает всю папку за один проход.

Мы охватим всё необходимое: требуемые библиотеки, почему важен каждый шаг, обработку граничных случаев и небольшие советы по отладке. Не нужно искать внешнюю документацию; код ниже самодостаточен, а пояснения отвечают на вопросы «как» *и* «почему». Откройте ваш любимый IDE и приступим.

---

## Что вы построите

- Инициализировать OCR‑движок (для иллюстрации мы используем пакет `ocr`).
- Просканировать каталог и **list image files python**‑style, отфильтровав PNG, JPG и TIFF.
- Выполнить **batch OCR** над всеми найденными изображениями.
- Вывести извлечённый текст для каждого файла, чётко помеченный.

> **Pro tip:** Если у вас не установлен пакет `ocr`, его можно заменить на `pytesseract` с несколькими небольшими изменениями — основная логика останется той же.

---

## Предварительные требования

- Python 3.8+ (скрипт использует f‑строки и подсказки типов).
- OCR‑библиотека, предоставляющая `OcrEngine` с методом `recognize_batch`. В этом руководстве мы предполагаем вымышленный пакет `ocr`, но шаблон работает и с реальными библиотеками.
- Папка, содержащая изображения, которые вы хотите обработать (`.png`, `.jpg`, `.tif`).

---

## Шаг 1 – Установить и импортировать необходимые модули

Сначала убедитесь, что OCR‑пакет доступен. Если вы используете реальную библиотеку, например `pytesseract`, замените импорт соответствующим образом.

```python
# Install the fictional OCR package (skip if using pytesseract)
# pip install ocr-package

import os
import ocr  # <-- replace with your actual OCR library
from typing import List
```

> **Почему это важно:** Импорт `os` даёт кроссплатформенную работу с путями, а `typing.List` помогает автодополнению в IDE и делает код более устойчивым к будущим изменениям.

---

## Шаг 2 – **Extract Text from Images**: Инициализировать OCR‑движок

Создание движка — первый шаг к любой работе с OCR. Мы также задаём язык автоопределения, чтобы движок мог обрабатывать документы с несколькими языками.

```python
def create_engine() -> ocr.OcrEngine:
    """
    Initializes the OCR engine with automatic language detection.
    Returns:
        An instance of ocr.OcrEngine ready for batch processing.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto  # Auto‑detect language
    return engine
```

> **Пояснение:** Обёртывание создания движка в функцию делает код модульным. Если позже понадобится изменить DPI или режим OCR, править нужно будет только в одном месте.

---

## Шаг 3 – **List Image Files Python**: Сбор файлов из каталога

Теперь нужно найти каждую картинку, которую будем обрабатывать. Ниже приведён list comprehension, отражающий типичный паттерн «list image files python».

```python
def get_image_files(input_dir: str) -> List[str]:
    """
    Scans `input_dir` and returns a list of absolute paths
    for files ending with .png, .jpg, or .tif (case‑insensitive).
    """
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]
```

> **Обработка граничных случаев:** Функция игнорирует подпапки (рекурсию можно добавить позже) и автоматически отбрасывает скрытые файлы, поскольку они обычно не заканчиваются поддерживаемыми расширениями.

---

## Шаг 4 – **Convert Scanned Images to Text**: Выполнить пакетный OCR

Большинство OCR‑библиотек предоставляют пакетный метод, который работает гораздо быстрее, чем обработка по одному изображению. Вот как его вызвать.

```python
def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    """
    Sends a list of image file paths to the OCR engine for batch recognition.
    Returns a list of OcrResult objects, preserving order.
    """
    # The fictional `recognize_batch` returns a list of results matching input order
    return engine.recognize_batch(image_paths)
```

> **Почему пакетный режим?** Передача всех изображений сразу уменьшает накладные расходы (например, повторную загрузку модели OCR) и часто даёт лучшую загрузку CPU/GPU.

---

## Шаг 5 – **Recognize Text from Pictures**: Вывести результаты

Наконец, мы проходим по парам имён файлов и результатов OCR, печатая чистый заголовок для каждого изображения.

```python
def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    """
    Prints the extracted text for each image, prefixed with the file name.
    """
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        # Some OCR engines store the plain text in a `.text` attribute
        print(result.text.strip())
        print()  # Blank line for readability
```

> **Совет:** `strip()` удаляет начальные и конечные пробелы, которые OCR часто добавляет.

---

## Полный скрипт – собрать всё вместе

Ниже полностью готовая к запуску программа. Сохраните её как `batch_ocr.py` и запустите `python batch_ocr.py <your_folder>`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – extracts text from images in a given folder.
Usage: python batch_ocr.py /path/to/images
"""

import sys
import os
import ocr  # Replace with your OCR library if different
from typing import List

def create_engine() -> ocr.OcrEngine:
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.Auto
    return engine

def get_image_files(input_dir: str) -> List[str]:
    supported_exts = ('.png', '.jpg', '.jpeg', '.tif', '.tiff')
    return [
        os.path.join(input_dir, f)
        for f in os.listdir(input_dir)
        if f.lower().endswith(supported_exts)
    ]

def run_batch_ocr(engine: ocr.OcrEngine, image_paths: List[str]) -> List[ocr.OcrResult]:
    return engine.recognize_batch(image_paths)

def display_results(image_paths: List[str], ocr_results: List[ocr.OcrResult]) -> None:
    for file_path, result in zip(image_paths, ocr_results):
        print(f"--- {os.path.basename(file_path)} ---")
        print(result.text.strip())
        print()

def main() -> None:
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <input_directory>")
        sys.exit(1)

    input_dir = sys.argv[1]

    if not os.path.isdir(input_dir):
        print(f"Error: '{input_dir}' is not a valid directory.")
        sys.exit(1)

    engine = create_engine()
    image_files = get_image_files(input_dir)

    if not image_files:
        print("No supported image files found in the directory.")
        sys.exit(0)

    ocr_results = run_batch_ocr(engine, image_files)
    display_results(image_files, ocr_results)

if __name__ == "__main__":
    main()
```

### Ожидаемый вывод

Если в папке находятся `invoice1.png` и `receipt.jpg`, вы можете увидеть следующее:

```
--- invoice1.png ---
Invoice #12345
Date: 2024‑04‑01
Total: $256.78

--- receipt.jpg ---
Store: Coffee Corner
Item: Latte
Price: $4.50
```

Каждый блок чётко помечен, что упрощает последующую обработку (например, сохранение в базу данных).

---

## Обработка распространённых проблем

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Текст не появляется** | Язык OCR не определён или изображение слишком низкоконтрастное. | Принудительно задать язык (`engine.language = ocr.Language.English`) или предварительно обработать изображения (увеличить контраст). |
| **Ошибка памяти при больших пакетах** | Движок пытается загрузить все изображения сразу. | Разделить `image_files` на части (`batch_size = 20`) и вызывать `recognize_batch` последовательно. |
| **Неподдерживаемый формат файла** | Вы добавили `.gif` или `.bmp`. | Расширить кортеж `supported_exts` или предварительно конвертировать изображения в PNG/JPG. |
| **Искажение Unicode** | OCR возвращает байты вместо строк. | Убедиться, что библиотека выводит Unicode (`result.text.decode('utf‑8')`, если нужно). |

---

## Расширение рабочего процесса

Теперь, когда вы умеете **extract text from images**, рассмотрите следующие шаги:

- **Экспорт в CSV** – Записать каждое имя файла и извлечённый текст в таблицу для аналитики.
- **Параллельная обработка** – Использовать `concurrent.futures.ThreadPoolExecutor` для одновременной обработки нескольких пакетов.
- **Интеграция с облачным OCR** – Заменить локальный движок на Google Vision или Azure OCR для более высокой точности при сложных макетах.
- **Добавить предобработку изображений** – Библиотеки вроде Pillow или OpenCV могут выпрямлять, удалять шум или применять пороговую обработку перед OCR, повышая качество результатов.

Все эти идеи естественно используют те же базовые функции, которые мы построили, так что начинать с нуля не придётся.

---

## Заключение

Мы только что прошли через полное решение для **extract text from images** в Python, охватив всё от **list image files python** до **recognize text from pictures** и, наконец, **convert scanned images to text** в удобном пакетном режиме. Скрипт преднамеренно прост, но достаточно гибок, чтобы служить основой для более крупных проектов — будь то оцифровка чеков, создание поискового архива или построение конвейера извлечения данных.

Попробуйте его, подправьте шаги предобработки и наблюдайте, как растёт точность OCR. Если возникнут трудности, вернитесь к таблице «Обработка распространённых проблем» — большинство вопросов решается небольшими изменениями конфигурации.

Готовы к следующему вызову? Попробуйте добавить шаг конвертации PDF в изображения с помощью `pdf2image`, а затем передать полученные изображения в тот же конвейер. Возможности безграничны, когда OCR сочетается с богатой экосистемой Python.

Счастливого кодинга, и пусть ваш текст всегда будет читаемым!


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}