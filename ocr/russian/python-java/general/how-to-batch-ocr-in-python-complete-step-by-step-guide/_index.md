---
category: general
date: 2026-06-28
description: Как выполнять пакетное OCR с помощью Python. Узнайте, как распознавать
  несколько изображений, извлекать текст из PNG и преобразовывать изображение в текст
  с полным руководством по OCR на Python.
draft: false
keywords:
- how to batch OCR
- ocr multiple images
- extract text from png
- convert image to text
- python ocr tutorial
language: ru
og_description: Как выполнять пакетное OCR в Python, объяснено в первом предложении.
  Следуйте этому руководству по OCR на Python, чтобы эффективно извлекать текст из
  PNG‑файлов.
og_title: Как выполнять пакетное OCR в Python – Полное руководство по программированию
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  headline: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: How to batch OCR using Python. Learn to OCR multiple images, extract
    text from PNG, and convert image to text with a full Python OCR tutorial.
  name: How to Batch OCR in Python – Complete Step‑by‑Step Guide
  steps:
  - name: '**Why set the language?**'
    text: '**Why set the language?**'
  - name: '**Why use a batch operation?**'
    text: '**Why use a batch operation?**'
  - name: '**Why a ThreadPoolExecutor?**'
    text: '**Why a ThreadPoolExecutor?**'
  - name: '**Why enumerate the results?**'
    text: '**Why enumerate the results?**'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Как выполнять пакетное OCR в Python — полное пошаговое руководство
url: /ru/python-java/general/how-to-batch-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять пакетный OCR в Python – Полное пошаговое руководство

Когда‑нибудь задумывались **как выполнить пакетный OCR** для стопки отсканированных страниц без написания цикла, блокирующего ваш UI? Вы не одиноки. Обрабатывать десятки PNG‑файлов один за другим может быть так же скучно, как смотреть, как сохнет краска, особенно когда каждый образ требует секунду‑две на декодирование.  

В этом руководстве мы покажем чистый, неблокирующий способ **OCR нескольких изображений** одновременно, **извлекать текст из PNG**‑файлов и **преобразовывать изображение в текст** с помощью современного Python‑движка OCR. К концу вы получите готовый к запуску скрипт, который можно вставить в любой проект – идеально для быстрого *python ocr tutorial* или производственного пакетного задания.

## Что вы построите

- Инициализируете OCR‑движок и зададите ему язык — латинский (или любой другой, который вам нужен).  
- Передадите список путей к изображениям (PNG в нашем примере) движку.  
- Запустите пакетную операцию, которая возвращает объект, похожий на Future.  
- Получите все результаты одновременно с помощью пула потоков, оставив основной поток свободным.  
- Выведите распознанный текст для каждой страницы, красиво разделив их.

Никакой скрытой магии, только чистый Python и сторонняя OCR‑библиотека (для иллюстрации мы используем вымышленный пакет `pyocr`).  

**Предварительные требования**  
- Установлен Python 3.8+.  
- Базовое знакомство с функциями Python и `concurrent.futures`.  
- Доступ к OCR‑библиотеке, предоставляющей класс `OcrEngine` (например, `pip install pyocr`).  

Если чего‑то не хватает, установите сейчас — это проще, чем кажется.

---

## Как выполнять пакетный OCR в Python – Основные концепции

Прежде чем перейти к коду, ответим на вопрос «почему» для каждого шага.

1. **Зачем задавать язык?**  
   Точность OCR резко возрастает, когда движок знает, какие символы ожидать. Латинский подходит для английского, французского, испанского и т.д. При необходимости переключитесь на `Language.Japanese` или `Language.Arabic`.

2. **Зачем использовать пакетную операцию?**  
   Пакетный вызов позволяет движку планировать работу внутри себя, часто используя нативные потоки или ускорение GPU. Он возвращает дескриптор, который можно запросить позже, что избавляет от блокировки во время обработки каждого изображения.

3. **Зачем ThreadPoolExecutor?**  
   Объект Future, который мы получаем, *ленивый* — он начинает извлекать результаты только по запросу. Передавая пул потоков в `getAll`, мы позволяем Python получать текст каждой страницы параллельно, что значительно сокращает общее время выполнения.

4. **Зачем перечислять (enumerate) результаты?**  
   Порядок результатов соответствует порядку входных путей, поэтому мы можем безопасно помечать каждый номер страницы.

Понимание этих «почему» поможет адаптировать шаблон под другие библиотеки или более крупные наборы данных.

---

## Шаг 1: Установите и импортируйте необходимые пакеты

Сначала убедитесь, что OCR‑библиотека установлена. В примере используется общий пакет `pyocr`; замените его на реальную библиотеку по вашему выбору (например, `pytesseract`, `easyocr`).

```bash
pip install pyocr
```

Теперь импортируем всё, что понадобится.

```python
# Standard library imports
import concurrent.futures
from pathlib import Path

# Third‑party OCR library (hypothetical)
from pyocr import OcrEngine, Language
```

> **Pro tip:** Использование `Path` из `pathlib` делает ваш скрипт независимым от ОС и легче читаемым.

---

## Шаг 2: Создайте OCR‑движок и задайте язык

Создание движка простое. Мы зафиксируем его на латинском для этой демонстрации.

```python
# Step 2: Initialise the OCR engine
engine = OcrEngine()
engine.setLanguage(Language.Latin)   # Change to Language.YourChoice if needed
```

Вызов `setLanguage` опционален для некоторых движков, но это хорошая привычка. Он сообщает OCR‑модели, на какой набор символов сосредоточиться, улучшая и скорость, и точность.

---

## Шаг 3: Составьте список файлов изображений для обработки (Extract Text from PNG)

Соберите все PNG‑файлы, которые хотите конвертировать. Использование `Path.glob` позволяет просто указать папку без правок скрипта.

```python
# Step 3: Gather PNG images – this is the “extract text from png” part
image_dir = Path("YOUR_DIRECTORY")   # Replace with your actual folder
image_paths = sorted(image_dir.glob("*.png"))   # Returns a list of Path objects

# Convert Path objects to strings for the OCR library (if required)
image_paths = [str(p) for p in image_paths]

if not image_paths:
    raise FileNotFoundError("No PNG files found in the specified directory.")
```

> **Почему это важно:** Сортируя список, мы гарантируем детерминированный порядок, который позже сопоставит каждый результат с правильным номером страницы.

---

## Шаг 4: Запустите пакетную OCR‑операцию (Convert Image to Text)

Теперь передаём список движку. Метод возвращает контейнер, похожий на Future, который мы опросим позже.

```python
# Step 4: Start batch OCR – returns a Future‑like object
batch_future = engine.ocrBatch(image_paths)
```

Внутри движок может запускать собственные рабочие потоки или даже конвейер GPU. Нас интересует лишь то, что у нас есть дескриптор (`batch_future`), умеющий получать отдельные результаты.

---

## Шаг 5: Получите все результаты одновременно (OCR Multiple Images)

Здесь мы действительно *пакетируем* работу. Передавая `ThreadPoolExecutor` в `getAll`, текст каждой страницы извлекается в отдельном потоке.

```python
# Step 5: Pull results using a thread pool – this speeds up OCR multiple images
with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    # getAll returns a list of Result objects in the same order as image_paths
    results = batch_future.getAll(executor)
```

Вы можете настроить `max_workers` в зависимости от количества ядер CPU или рекомендаций OCR‑библиотеки. Больше воркеров ≠ всегда быстрее — следите за загрузкой процессора.

---

## Шаг 6: Выведите распознанный текст (Python OCR Tutorial Finale)

Наконец, печатаем текст каждой страницы. Объект `Result` предоставляет `getText()` — при необходимости замените на метод вашей библиотеки.

```python
# Step 6: Display the recognised text for each page
for i, result in enumerate(results):
    print(f"--- Page {i + 1} ---")
    print(result.getText())
    print()   # Blank line for readability
```

**Ожидаемый вывод (пример)**

```
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna...

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco...
```

Если какое‑то изображение не удалось обработать, большинство движков возвращают пустую строку или бросают исключение — вы можете обернуть цикл в `try/except`, чтобы аккуратно обработать такие случаи.

---

## Полный скрипт – готов к запуску

Ниже полный, автономный скрипт. Скопируйте его в файл `batch_ocr.py`, замените `YOUR_DIRECTORY` и выполните `python batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script – processes all PNG files in a directory.
Demonstrates how to batch OCR, OCR multiple images, extract text from PNG,
and convert image to text using a Python OCR engine.
"""

import concurrent.futures
from pathlib import Path

# Replace with your actual OCR library import
from pyocr import OcrEngine, Language

def main():
    # Initialise OCR engine
    engine = OcrEngine()
    engine.setLanguage(Language.Latin)

    # Locate PNG files
    image_dir = Path("YOUR_DIRECTORY")          # <‑‑ change this
    image_paths = sorted(image_dir.glob("*.png"))
    image_paths = [str(p) for p in image_paths]

    if not image_paths:
        raise FileNotFoundError("No PNG files found in the specified directory.")

    # Start batch OCR
    batch_future = engine.ocrBatch(image_paths)

    # Retrieve results concurrently
    with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
        results = batch_future.getAll(executor)

    # Print each page's recognised text
    for i, result in enumerate(results):
        print(f"--- Page {i + 1} ---")
        print(result.getText())
        print()

if __name__ == "__main__":
    main()
```

Сохраните, запустите и наблюдайте, как консоль заполняется извлечённым текстом. Просто, быстро и полностью асинхронно.

---

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Как исправить |
|----------|-------------------|---------------|
| **Нет вывода** – пустые строки | Движок не нашёл текст (изображение слишком шумное) | Предобработайте изображения: бинаризация, исправление наклона, увеличение DPI |
| **FileNotFoundError** | Неправильный путь к директории или отсутствуют PNG‑файлы | Проверьте `YOUR_DIRECTORY` и убедитесь, что файлы имеют расширение `.png` |
| **Высокая загрузка CPU** | `max_workers` установлен слишком высоко для вашей машины | Уменьшите `max_workers` или включите ускорение GPU, если поддерживается |
| **Иероглифы вместо текста** | Движок по умолчанию использовал другой язык | Вызовите `engine.setLanguage(Language.Latin)` (или нужный) перед пакетным OCR |

Раннее решение этих вопросов сэкономит часы отладки.

---

## Расширение руководства – дальнейшие шаги

- **OCR нескольких изображений** в других форматах (JPEG, TIFF) — просто измените шаблон `glob`.  
- **Extract text from PNG** и загрузите его в поисковый индекс (например, Elasticsearch).  
- **Convert image to text** для генерации PDF с помощью `reportlab` или `PyPDF2`.  
- **Параллелизация на нескольких машинах** с помощью `multiprocessing` или очереди задач, такой как Celery, для огромных наборов данных.  

Каждая из этих тем естественно продолжает **python ocr tutorial**, который вы только что завершили.

---

## Заключение

Мы прошли процесс **batch OCR** коллекции PNG‑файлов, продемонстрировали мощность API, ориентированного на пакетную обработку, и показали, как **extract text from PNG** с помощью подхода на основе пула потоков. Полный скрипт выше готов к использованию в продакшене, а вы получили надёжную основу для любого OCR‑интенсивного проекта на Python.

Попробуйте, поиграйте с настройками языка и, возможно, замените `pyocr` на `pytesseract` — шаблон остаётся тем же. Есть вопросы или хотите поделиться интересным кейсом? Оставляйте комментарий, и будем обсуждать дальше.

*Счастливого кодинга!*


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гиде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}