---
category: general
date: 2026-03-28
description: Быстро извлекайте текст из PNG с помощью Aspose OCR в Python. Узнайте,
  как преобразовать текст отсканированных страниц с использованием параллельного распознавания
  изображений в Python для получения высокопроизводительных результатов.
draft: false
keywords:
- extract text from png
- convert scanned pages text
- parallel image recognition python
- recognize image text python
- async OCR batch processing
- Aspose OCR Python
language: ru
og_description: Быстро извлекайте текст из PNG с помощью Aspose OCR в Python. Это
  руководство показывает, как преобразовать текст отсканированных страниц с использованием
  параллельного распознавания изображений в Python, обеспечивая высокоскоростные результаты.
og_title: Извлечение текста из PNG – быстрый параллельный OCR с Python
tags:
- OCR
- Python
- Image Processing
- Concurrency
title: Извлечение текста из PNG — быстрый параллельный OCR с Python и Aspose
url: /ru/python-java/general/extract-text-from-png-fast-parallel-ocr-with-python-and-aspo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PNG – Быстрый параллельный OCR с Python

Когда‑нибудь вам нужно было **извлечь текст из PNG** файлов, но однопоточный OCR оказался мучительно медленным? Вы не одиноки. Будь то оцифровка стопки отсканированных чеков или преобразование слайдов лекций в поисковые PDF, узким местом обычно является сам шаг OCR.  

В этом руководстве мы покажем вам полное, готовое к запуску решение, которое **конвертирует текст отсканированных страниц** параллельно, используя асинхронный пакетный режим Aspose OCR совместно с `ThreadPoolExecutor` из Python. К концу вы сможете **распознавать текст на изображениях в стиле python**, обрабатывая десятки изображений за долю времени, которое потребовал бы наивный цикл.

> **Что вы получите**  
> * Полностью рабочий скрипт, который извлекает текст из PNG‑изображений одновременно.  
> * Понимание того, почему асинхронный пакетный режим ускоряет процесс.  
> * Советы по масштабированию решения для более крупных нагрузок.

## Что вам понадобится

| Требование | Причина |
|------------|---------|
| Python 3.9+ | Современный синтаксис и подсказки типов. |
| `aspose-ocr` и `aspose-storage` пакеты | Предоставляют OCR‑движок и загрузчик изображений. |
| Папка с PNG‑файлами (например, отсканированные страницы) | Исходные материалы, которые вы хотите обработать. |
| Базовые знания о параллелизме в Python | Полезно, но не обязательно; мы всё объясним. |

Вы можете установить библиотеки Aspose с помощью:

```bash
pip install aspose-ocr aspose-storage
```

> **Pro tip:** Держите пакеты в актуальном состоянии (`pip list --outdated`), чтобы воспользоваться последними улучшениями производительности.

## Шаг 1: Инициализировать OCR‑движок Aspose в асинхронном пакетном режиме

Первое, что мы делаем, — создаём экземпляр `OcrEngine` и переключаем его в **асинхронный пакетный режим**. Этот режим ставит запросы распознавания в очередь внутри движка, позволяя обрабатывать несколько изображений без блокировки вашего Python‑потока.

```python
import aspose.ocr as aocr
import aspose.storage as storage

# Create the OCR engine
ocr_engine = aocr.OcrEngine()
# Enable async batch processing – crucial for parallel speed‑up
ocr_engine.batch_mode = aocr.BatchMode.ASYNC
```

*Почему async?*  
Когда вы вызываете `recognize` в синхронном режиме, вызов блокируется до полного завершения обработки изображения. В асинхронном режиме движок может начать работать над следующим изображением, пока текущее ещё декодируется, эффективно перекрывая операции ввода‑вывода и процессорные задачи.

## Шаг 2: Список PNG‑файлов, которые нужно обработать

Здесь мы определяем набор изображений. В реальном проекте вы, возможно, будете генерировать этот список динамически (например, `glob.glob("*.png")`), но явное указание упрощает понимание примера.

```python
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]
```

> **Note:** Замените `YOUR_DIRECTORY` на реальный путь, где находятся ваши PNG‑сканы. Если файлов сотни, рассмотрите использование `os.listdir` с фильтрацией по расширению `.png`.

## Шаг 3: Написать вспомогательную функцию, которая загружает изображение и возвращает его текст

Вспомогательная функция инкапсулирует двухшаговый процесс загрузки файла через **Aspose Storage** и последующей передачи его OCR‑движку. Добавление небольшого docstring делает функцию самодокументирующейся — полезно для будущего обслуживания.

```python
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the recognized text.
    """
    # Load the image using Aspose Storage (handles many formats)
    img = storage.Image.load(path)
    # Perform OCR; the result object contains the extracted text
    result = ocr_engine.recognize(img)
    return result.text
```

*Почему отдельная функция?*  
Она делает код пула потоков чище и позволяет переиспользовать логику в других местах (например, в Flask‑endpoint). Кроме того, изоляция ввода‑вывода упрощает отладку — если конкретный файл не удаётся обработать, имя файла появится в трассировке исключения.

## Шаг 4: Запустить параллельное распознавание изображений в Python с помощью пула потоков

Теперь подключаем `ThreadPoolExecutor`. По умолчанию мы создаём четыре рабочих потока, но вы можете настроить `max_workers` в зависимости от количества ядер процессора и размера набора изображений.

```python
from concurrent.futures import ThreadPoolExecutor, as_completed

with ThreadPoolExecutor(max_workers=4) as pool:
    # Submit each image to the pool; map futures back to filenames
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    
    # Process results as they finish (order may differ from input order)
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)
```

### Как это обеспечивает параллельное распознавание изображений в Python

* **ThreadPoolExecutor** создаёт пул рабочих потоков, каждый из которых вызывает `recognize_image`.  
* Поскольку OCR‑движок находится в асинхронном пакетном режиме, каждый поток может передать работу движку и при этом оставаться отзывчивым.  
* `as_completed` возвращает будущие объекты в порядке их завершения, так что вы получаете результаты сразу же, как только они готовы — идеально для потоковой обработки больших партий.

> **Common pitfall:** Использование `max_workers=1` нейтрализует смысл параллелизма. На машине с 8‑ядерным процессором `max_workers=8` часто даёт лучшую пропускную способность, но протестируйте несколько значений, чтобы найти оптимальный режим для вашего железа.

## Шаг 5: Проверить вывод и обработать граничные случаи

При запуске скрипта вы должны увидеть блок текста для каждого PNG, предварённый его именем файла:

```
--- YOUR_DIRECTORY/page1.png ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

--- YOUR_DIRECTORY/page2.png ---
Sed do eiusmod tempor incididunt ut labore et dolore...

--- YOUR_DIRECTORY/page3.png ---
Ut enim ad minim veniam, quis nostrud exercitation...
```

Если какое‑либо изображение не удалось обработать (повреждённый файл, неподдерживаемый формат), блок `except` выводит полезное сообщение об ошибке вместо того, чтобы аварийно завершить всю партию.

### Расширение решения

| Сценарий | Предлагаемое изменение |
|----------|------------------------|
| **Тысячи страниц** | Перейдите на `ProcessPoolExecutor`, чтобы задействовать несколько процессов CPU, либо разбейте список на части и обрабатывайте партии последовательно. |
| **Другие форматы изображений (JPG, TIFF)** | Метод `storage.Image.load` автоматически определяет формат, так что просто добавьте файлы в `input_images`. |
| **Необходимо сохранять результаты** | Записывайте `text` в файл `.txt` или вставляйте в базу данных внутри блока `else`. |
| **Мониторинг производительности** | Оберните `recognize_image` таймером (`time.perf_counter`) и логируйте длительность обработки каждого файла. |

## Полный рабочий пример (готовый к копированию)

Ниже представлен полный скрипт, готовый к размещению в файле `parallel_ocr.py`. Ничего не упущено — всё, что вам нужно, находится здесь.

```python
# parallel_ocr.py
import aspose.ocr as aocr
import aspose.storage as storage
from concurrent.futures import ThreadPoolExecutor, as_completed

# -------------------------------------------------
# Step 1: Initialize OCR engine in async batch mode
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.batch_mode = aocr.BatchMode.ASYNC   # enable asynchronous batch processing

# -------------------------------------------------
# Step 2: Define the PNG files you want to recognize
# -------------------------------------------------
input_images = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png"
]

# -------------------------------------------------
# Step 3: Helper that loads an image and returns the recognized text
# -------------------------------------------------
def recognize_image(path: str) -> str:
    """
    Load a PNG image from `path` and return the OCR‑extracted text.
    """
    img = storage.Image.load(path)
    result = ocr_engine.recognize(img)
    return result.text

# -------------------------------------------------
# Step 4: Run OCR on all images concurrently using a thread pool
# -------------------------------------------------
with ThreadPoolExecutor(max_workers=4) as pool:
    future_to_file = {pool.submit(recognize_image, f): f for f in input_images}
    for future in as_completed(future_to_file):
        file_name = future_to_file[future]
        try:
            text = future.result()
        except Exception as exc:
            print(f"--- {file_name} ---")
            print(f"Error during OCR: {exc}")
        else:
            print(f"--- {file_name} ---")
            print(text)

# -------------------------------------------------
# Step 5: Output is printed to the console.
# -------------------------------------------------
```

Сохраните файл, замените плейсхолдер `YOUR_DIRECTORY` на ваш путь и запустите:

```bash
python parallel_ocr.py
```

Вы должны увидеть извлечённый текст для каждого PNG в консоли, как показано ранее.

## Заключение

Мы только что продемонстрировали, как **извлекать текст из PNG** файлов эффективно, комбинируя асинхронный пакетный режим Aspose OCR с `ThreadPoolExecutor` из Python. Скрипт конвертирует текст отсканированных страниц параллельно, предоставляя масштабируемый способ **распознавать текст на изображениях в стиле python** без написания собственного пула потоков с нуля.  

Если вы готовы пойти дальше, попробуйте:

* Сохранять результаты в поисковую базу SQLite.  
* Добавить предобработку изображений (выравнивание, шумоподавление) с помощью OpenCV перед OCR.  
* Развернуть скрипт как микросервис за Flask или FastAPI endpoint.

Помните, ключ к высокопроизводительному OCR — это не только быстрый движок, но и способ подачи задач, максимально использующий параллелизм. С показанным шаблоном вы сможете обрабатывать десятки и даже сотни PNG‑сканов с минимальными изменениями кода.

Счастливого кодинга, и пусть ваши PDF всегда будут поисковыми!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}