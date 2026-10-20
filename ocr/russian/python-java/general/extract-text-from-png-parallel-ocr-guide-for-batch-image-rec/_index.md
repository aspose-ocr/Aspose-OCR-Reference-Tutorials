---
category: general
date: 2026-03-18
description: Извлеките текст из PNG с помощью Python и Aspose OCR. Узнайте, как загрузить
  изображение для OCR, выполнить OCR нескольких файлов и реализовать пакетное OCR
  изображений с параллельным распознаванием.
draft: false
keywords:
- extract text from png
- ocr multiple files
- batch ocr images
- load image for OCR
- parallel image recognition
language: ru
og_description: Извлечение текста из PNG с помощью Aspose OCR в Python. Этот учебник
  показывает, как загрузить изображение для OCR, обработать несколько файлов OCR и
  выполнить пакетное распознавание изображений с использованием параллельного распознавания.
og_title: Извлечение текста из PNG – Руководство по параллельному OCR
tags:
- OCR
- Python
- threading
- Aspose
- image-processing
title: Извлечение текста из PNG – Параллельное руководство по OCR для пакетного распознавания
  изображений
url: /ru/python-java/general/extract-text-from-png-parallel-ocr-guide-for-batch-image-rec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PNG – Руководство по параллельному OCR для пакетного распознавания изображений

Когда‑нибудь вам нужно было **извлечь текст из PNG** файлов, но вы застряли на этапе, когда обработка одного изображения занимает вечность? Вы не одиноки. Во многих реальных проектах — подумайте о сканерах счетов, оцифровщиках чеков или архивационных инструментах — скорость имеет значение, и обработка каждого PNG по отдельности просто не подходит.  

В этом руководстве мы пройдемся по полностью готовому к запуску решению, которое **загружает изображение для OCR**, выполняет **ocr multiple files** в режиме **batch OCR images**, и использует **параллельное распознавание изображений** с модулем `threading` в Python. К концу у вас будет скрипт, извлекающий текст из любого количества PNG за секунды, а не за минуты.

## Что понадобится

- Python 3.8 или новее (показанный синтаксис работает и на 3.10+).  
- Пакет Aspose OCR для Java/​Python (`aspose-ocr`). Его можно установить через `pip`.  
- Папка с несколькими PNG‑файлами, которые вы хотите обработать.  
- Умеренное количество ОЗУ — каждый поток держит небольшую копию OCR‑движка, поэтому даже ноутбук может запустить десятки рабочих потоков.

Никаких внешних сервисов, облачных ключей и загадочных файлов конфигурации. Просто чистый Python‑код, который вы можете скопировать‑вставить и запустить.

## Почему извлекать текст из PNG параллельно?

Обработка PNG ограничена процессором: OCR‑движок выполняет серию алгоритмов анализа изображения, которые перебирают пиксельные данные. Когда у вас есть десять, двадцать или сто изображений, общее время выполнения по сути равно сумме времени каждого отдельного запуска.  

Создавая поток для каждого файла, мы позволяем операционной системе планировать эти процессороёмкие задачи одновременно. На многопроцессорной машине это часто сокращает реальное время вдвое — а иногда и вчетверо. Недостаток — немного больший объём памяти, но для большинства пакетных задач выигрыш в скорости того стоит.

> **Pro tip:** Если вы работаете с сотнями мегабайт изображений, рассмотрите возможность использования `concurrent.futures.ProcessPoolExecutor` вместо `threading`. Процессы обеспечивают истинный параллелизм в ограниченном GIL интерпретаторе CPython, ценой небольших дополнительных накладных расходов.

## Шаг 1: Установите Aspose OCR для Python

Сначала всё самое важное — установим OCR‑библиотеку в вашу систему.

```bash
pip install aspose-ocr
```

Эта единственная строка загружает последние бинарные файлы Aspose OCR и их Python‑обёртки. Если возникнет ошибка доступа, попробуйте добавить `--user` или использовать виртуальное окружение.

## Шаг 2: Загрузка изображения для OCR — функция‑рабочий

Теперь мы определяем основную процедуру, которая будет выполняться в каждом потоке. Она **загружает изображение для OCR**, запускает распознавание и выводит предварительный просмотр извлечённого текста.

```python
import threading
from asposeocrjava import OcrEngine, OcrResult

def ocr_task(image_path: str):
    """
    Loads a PNG, runs OCR, and prints the first 100 characters of the result.
    Each thread creates its own OcrEngine instance to avoid state clashes.
    """
    # Initialise a fresh engine – this is cheap and thread‑safe.
    engine = OcrEngine()
    # Load image for OCR
    engine.setImageFromFile(image_path)

    # Perform the recognition – this is the CPU‑intensive part.
    result: OcrResult = engine.recognize()

    # Show a preview of the recognized text (first 100 characters)
    preview = result.getText()[:100].replace("\n", " ")
    print(f"[{image_path}] -> {preview}...")
```

Несколько замечаний:

- **Почему новый `OcrEngine` на каждый поток?** Движок содержит внутренние буферы; совместное использование одной копии приведёт к состояниям гонки и искажённому выводу.  
- **Зачем удалять переносы строк?** При выводе в консоль это сохраняет строку аккуратной.  
- **Обработка ошибок?** В продакшене вы бы обернули тело в `try/except` и, возможно, записывали в файл — об этом мы расскажем позже.

## Шаг 3: Список PNG‑файлов, которые нужно обработать

Вы могли бы жёстко прописать список, но более гибкий подход — сканировать каталог. Ниже мы вручную перечисляем три файла для наглядности; замените пути на свои.

```python
image_files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.png"
]
```

Если вы предпочитаете автоматическое обнаружение:

```python
import pathlib

image_dir = pathlib.Path("YOUR_DIRECTORY")
image_files = sorted(str(p) for p in image_dir.glob("*.png"))
```

Эта небольшая правка позволяет **извлекать текст из PNG** файлов пакетно, не меняя исходный код каждый раз.

## Шаг 4: Настройка ocr multiple files с batch OCR images

Теперь мы создаём поток для каждого изображения. Это ядро шаблона **batch OCR images**.

```python
# Create a thread for each image to run OCR concurrently
thread_list = [
    threading.Thread(target=ocr_task, args=(path,))
    for path in image_files
]
```

Генератор списка делает код лаконичным, и каждый объект `Thread` хранит целевую функцию и её аргумент (`image_path`).  

> **Side note:** Модуль `threading` в Python использует нативные потоки ОС, поэтому на ноутбуке с 4‑ядерным процессором обычно одновременно работает до четырёх потоков; остальные планируются по мере освобождения ядер.

## Шаг 5: Запуск параллельного распознавания изображений

Запуск рабочих потоков прост: пройтись по списку и вызвать `start()`. После этого ждём завершения каждого потока с помощью `join()`.

```python
# Step 5: Start all threads
for thread in thread_list:
    thread.start()

# Step 6: Wait for every thread to finish before exiting
for thread in thread_list:
    thread.join()
```

Когда скрипт завершится, вы увидите серию строк вроде:

```
[YOUR_DIRECTORY/doc1.png] -> Invoice #12345 Date: 2024-07-01 Total: $...
[YOUR_DIRECTORY/doc2.png] -> Receipt from Store XYZ Items: 3 Subtotal: $...
[YOUR_DIRECTORY/doc3.png] -> ...
```

Этот вывод подтверждает, что каждый PNG был обработан, а извлечённый текст доступен для дальнейшей обработки (например, сохранения в базе данных или передачи в NLP‑конвейер).

## Шаг 6: Проверка результатов и обработка граничных случаев

### Проверка пустых результатов

Иногда изображение слишком шумное, или OCR‑движок не обнаруживает символов. Быстрая проверка может спасти от последующих ошибок.

```python
def ocr_task(image_path: str):
    engine = OcrEngine()
    engine.setImageFromFile(image_path)

    result: OcrResult = engine.recognize()
    text = result.getText().strip()

    if not text:
        print(f"[{image_path}] -> No text detected.")
    else:
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")
```

### Ограничение количества одновременно работающих потоков

Если вы запускаете это на скромной виртуальной машине, создание сотен потоков может перегрузить планировщик. Вы можете ограничить параллелизм с помощью семафора:

```python
max_workers = 8
sema = threading.Semaphore(max_workers)

def ocr_task(image_path: str):
    with sema:
        # ... same body as before ...
```

### Сохранение результатов в файл

Вместо вывода в консоль вы можете захотеть CSV‑файл с именем файла и извлечённым текстом:

```python
import csv
output_path = "ocr_results.csv"

with open(output_path, "w", newline="", encoding="utf-8") as csvfile:
    writer = csv.writer(csvfile)
    writer.writerow(["filename", "extracted_text"])

    def ocr_task(image_path: str):
        engine = OcrEngine()
        engine.setImageFromFile(image_path)
        text = engine.recognize().getText().strip()
        writer.writerow([image_path, text])
```

Убедитесь, что CSV открывается **один раз** вне функции потока, чтобы избежать состояний гонки; запись `csv`‑модуля потокобезопасна для простых записей.

## Полный рабочий пример

Объединив всё вместе, вот единственный скрипт, который вы можете сохранить в файл `batch_ocr.py` и запустить:

```python
import threading
import pathlib
import csv
from asposeocrjava import OcrEngine, OcrResult

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_DIR = pathlib.Path("YOUR_DIRECTORY")   # <-- change this
OUTPUT_CSV = "ocr_results.csv"
MAX_WORKERS = 8                               # adjust based on your CPU

# ----------------------------------------------------------------------
# Helper: OCR worker
# ----------------------------------------------------------------------
sema = threading.Semaphore(MAX_WORKERS)

def ocr_task(image_path: str, writer):
    """
    Extract text from a single PNG using Aspose OCR.
    This function is designed to run inside a thread.
    """
    with sema:                     # limit concurrent threads
        engine = OcrEngine()
        engine.setImageFromFile(image_path)

        result: OcrResult = engine.recognize()
        text = result.getText().strip()

        # Write to CSV (thread‑safe because writer is shared)
        writer.writerow([image_path, text])

        # Also print a short preview for quick debugging
        preview = text[:100].replace("\n", " ")
        print(f"[{image_path}] -> {preview}...")

# ----------------------------------------------------------------------
# Main routine
# ----------------------------------------------------------------------
def main():
    # Discover all PNG files
    image_files = sorted(str(p) for p in IMAGE_DIR.glob("*.png"))
    if not image_files:
        print("No PNG files found in", IMAGE_DIR)
        return

    # Open CSV once, share the writer with all threads
    with open(OUTPUT_CSV, "w", newline="", encoding="utf-8") as csvfile:
        writer = csv.writer(csvfile)
        writer.writerow(["filename", "extracted_text"])

        # Create a thread for each image
        threads = [
            threading.Thread(target=ocr_task, args=(path, writer))
            for path in image_files

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}