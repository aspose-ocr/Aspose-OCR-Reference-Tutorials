---
category: general
date: 2026-03-26
description: Как эффективно выполнять пакетное OCR с помощью Python — изучите извлечение
  текста из изображений и PDF, конвертацию OCR с параллельной обработкой.
draft: false
keywords:
- how to batch ocr
- extract text from images
- pdf ocr conversion
- batch ocr processing
- parallel ocr processing
language: ru
og_description: как эффективно выполнять пакетное OCR — пошаговое руководство по извлечению
  текста из изображений, конвертации PDF в OCR и пакетной обработке OCR с использованием
  Python.
og_title: 'Как пакетно выполнять OCR: быстрое параллельное извлечение текста'
tags:
- OCR
- Python
- Parallel Computing
title: 'Как пакетно выполнять OCR: быстрое параллельное извлечение текста'
url: /ru/python-java/general/how-to-batch-ocr-fast-parallel-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как выполнять пакетный OCR: быстрое параллельное извлечение текста

Когда‑то задавались вопросом **how to batch ocr**, имея десятки отсканированных страниц, скриншотов и PDF‑файлов? Вы не одиноки — большинство разработчиков сталкиваются с тем же препятствием: обработка каждого файла по отдельности становится болезненным узким местом.  

Хорошая новость в том, что можно запустить несколько рабочих потоков, передать им все файлы и наблюдать, как OCR‑движок обрабатывает пакет параллельно. В этом руководстве мы пройдём полный, готовый к запуску пример, показывающий **extract text from images**, выполнение **pdf ocr conversion** и использование **parallel ocr processing** для ускорения.

> **What you’ll walk away with**  
> * Полностью рабочий скрипт на Python, который обрабатывает смешанный список файлов PNG, TIFF, PDF и JPG за один проход.  
> * Понимание того, почему пул потоков ускоряет I/O‑зависимые задачи OCR.  
> * Советы по обработке ошибок, большим PDF и настройке количества потоков.  

## Предварительные требования

Перед тем как начать, убедитесь, что у вас есть:

| Требование | Причина |
|------------|---------|
| Python 3.8+ | Современный синтаксис & `concurrent.futures` |
| `ocr` library (or any compatible OCR wrapper) | Предоставляет `OcrBatchProcessor` и объекты‑результаты |
| Небольшой набор образцов (PNG, TIFF, PDF, JPG) | Чтобы увидеть **extract text from images** в действии |
| Базовое знакомство с потоками (опционально) | Полезно, но не обязательно |

Если вы ещё не установили пакет `ocr`, выполните:

```bash
pip install ocr-lib   # replace with the actual package name
```

Теперь, когда окружение готово, разберём задачу по частям.

## Шаг 1: Импортировать вспомогательные функции и создать процессор пакетов

Первое, что нам нужно — место для сбора всех OCR‑задач. Класс `OcrBatchProcessor` делает именно это — ставит задачи в очередь и возвращает список объектов `Future`.

```python
# Step 1 – set up imports and create the batch processor
from concurrent.futures import as_completed   # helps us retrieve results as they finish
import ocr                                      # the OCR library you installed

# Create a processor that will manage the whole batch
ocr_batch = ocr.OcrBatchProcessor()
```

*Why this matters*: Импорт `as_completed` позволяет реагировать на каждую завершённую задачу мгновенно, вместо ожидания самого медленного файла. Это ядро **batch ocr processing**.

## Шаг 2: Настроить пул рабочих потоков для параллельного выполнения

По умолчанию процессор может использовать один поток, что нивелирует смысл пакетной обработки. Мы явно запрашиваем четыре рабочих — при желании увеличьте это число до количества ядер CPU.

```python
# Step 2 – configure parallelism (four threads in this example)
ocr_batch.set_thread_count(4)   # Adjust based on your machine’s capabilities
```

*Pro tip*: Для I/O‑bound задач, таких как OCR, возврат от вложения обычно наблюдается после `CPU cores * 2`. Протестируйте несколько значений и выберите оптимальное.

## Шаг 3: Добавить в очередь каждый файл, который нужно OCR‑ить

Здесь мы добавляем смесь изображений и PDF‑файлов. Метод `add` просто фиксирует путь; реальная работа начнётся только после отправки пакета.

```python
# Step 3 – add files to the batch (feel free to glob a directory instead)
ocr_batch.add("YOUR_DIRECTORY/page1.png")
ocr_batch.add("YOUR_DIRECTORY/page2.tif")
ocr_batch.add("YOUR_DIRECTORY/page3.pdf")
ocr_batch.add("YOUR_DIRECTORY/page4.jpg")
```

Если нужно обработать всю папку, простой цикл `glob` справится:

```python
import pathlib, fnmatch
for path in pathlib.Path("YOUR_DIRECTORY").rglob("*"):
    if fnmatch.fnmatch(path.suffix.lower(), ".png") or \
       fnmatch.fnmatch(path.suffix.lower(), ".tif") or \
       fnmatch.fnmatch(path.suffix.lower(), ".pdf") or \
       fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
        ocr_batch.add(str(path))
```

## Шаг 4: Запустить задачи и собрать futures

Вызов `submit_all` даёт процессору зелёный свет. Он возвращает список объектов `Future` — своего рода заполнители для результатов, которые появятся позже.

```python
# Step 4 – submit all jobs at once; get back a list of futures
ocr_futures = ocr_batch.submit_all()
```

На данном этапе OCR‑движок работает в фоне, каждый поток «пережёвывает» свой файл.

## Шаг 5: Получать результаты сразу же после их завершения

С помощью `as_completed` мы перебираем futures в порядке их завершения, а не в порядке отправки. Это делает скрипт более отзывчивым, особенно когда некоторые PDF занимают больше времени, чем простые PNG.

```python
# Step 5 – retrieve each result as it completes
for future in as_completed(ocr_futures):
    try:
        ocr_result = future.result()          # May raise if the job failed
        print("Batch result:\n", ocr_result.get_text())
    except Exception as exc:
        # Graceful error handling – you can log or retry here
        print(f"An OCR job failed: {exc}")
```

**Expected output** (truncated for brevity):

```
Batch result:
 The quick brown fox jumps over the lazy dog.
...
Batch result:
 Invoice #12345
 Date: 2026-03-01
 Total: $1,234.56
...
```

Каждый блок соответствует текстовому представлению исходного файла. Если вы делаете **pdf ocr conversion**, текст будет включать всё, что OCR‑движок смог расшифровать со страниц.

## Обработка граничных случаев и распространённых подводных камней

| Ситуация | На что обратить внимание | Быстрое решение |
|----------|--------------------------|-----------------|
| Повреждённое изображение | `future.result()` бросает `OSError` | Обернуть в `try/except` (см. код выше) |
| Очень большие PDF ( > 100 MB ) | Давление на память, замедление потоков | Умеренно увеличить `thread_count` или разбить PDF на главы |
| Документы на нескольких языках | Стандартная модель OCR может ошибаться | Передать подсказки о языке в `OcrBatchProcessor`, если библиотека поддерживает |
| Необходимо сохранить макет | Обычный `get_text()` теряет колонки | Использовать `ocr_result.get_hocr()` или аналогичный метод, учитывающий макет |

### Pro tip: Пользовательское количество потоков в зависимости от типа файла

Если вы знаете, что большинство нагрузки — PDF, можно выделить больше потоков для них и меньше для небольших PNG. Некоторые библиотеки позволяют задавать `priority` для каждой задачи; иначе можно создать два отдельных пакета — один для изображений, другой для PDF — и запускать их одновременно.

## Визуальный обзор (опционально)

![how to batch ocr workflow diagram](https://example.com/ocr-workflow.png "how to batch ocr workflow")

*Диаграмма иллюстрирует поток от обнаружения файлов → создания пакета → параллельного выполнения → агрегации результатов.*

## Полный скрипт, который можно скопировать и вставить

Ниже представлен весь код, готовый к размещению в файле `.py`. Он включает все приведённые выше фрагменты, а также небольшую вспомогательную функцию, автоматически находящую поддерживаемые файлы в каталоге.

```python
#!/usr/bin/env python3
"""
How to Batch OCR – Complete Example
-----------------------------------
This script demonstrates parallel OCR processing of mixed image and PDF files.
It shows how to extract text from images, perform pdf ocr conversion, and
handle errors gracefully.
"""

from concurrent.futures import as_completed
import pathlib, fnmatch, sys
import ocr  # replace with your actual OCR library import

def discover_files(root_dir):
    """Yield paths of supported OCR files under *root_dir*."""
    for path in pathlib.Path(root_dir).rglob("*"):
        if fnmatch.fnmatch(path.suffix.lower(), ".png") \
           or fnmatch.fnmatch(path.suffix.lower(), ".tif") \
           or fnmatch.fnmatch(path.suffix.lower(), ".pdf") \
           or fnmatch.fnmatch(path.suffix.lower(), ".jpg"):
            yield str(path)

def main(directory, workers=4):
    # 1️⃣ Initialise batch processor
    ocr_batch = ocr.OcrBatchProcessor()
    ocr_batch.set_thread_count(workers)

    # 2️⃣ Queue every discovered file
    for file_path in discover_files(directory):
        ocr_batch.add(file_path)

    # 3️⃣ Submit all jobs
    futures = ocr_batch.submit_all()

    # 4️⃣ Process results as they arrive
    for fut in as_completed(futures):
        try:
            result = fut.result()
            print("=== OCR RESULT ===")
            print(result.get_text())
            print("\n---\n")
        except Exception as e:
            print(f"[ERROR] OCR failed for a job: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python batch_ocr.py <directory-with-files>")
        sys.exit(1)
    main(sys.argv[1])
```

Сохраните его как `batch_ocr.py`, укажите папку с вашими сканами и наблюдайте, как консоль заполняется извлечённым текстом.  

### Почему это работает

* **Thread pool** – OCR в основном ждёт ввода‑вывода и внешних вызовов движка, поэтому несколько потоков держат процессор занятым.  
* **`as_completed`** – Вы получаете результаты сразу, как только они готовы, что идеально для обратной связи UI или потоковых конвейеров.  
* **Error isolation** – Одна плохая файл не остановит весь пакет; блок `try/except` изолирует сбои.

## Заключение

В двух словах, теперь вы знаете **how to batch ocr** с помощью `concurrent.futures` в Python совместно с OCR‑библиотекой, поддерживающей пакетную обработку. Настроив умеренный пул потоков, поставив в очередь каждый поддерживаемый файл и получая результаты по мере их готовности, вы достигаете быстрой **parallel ocr processing** без потери надёжности.  

Отсюда вы можете:

* Подключить вывод к поисковому индексу для быстрого поиска по документам.  
* Расширить скрипт, чтобы записывать каждый результат в файл `.txt` рядом с оригиналом.  
* Заменить встроенный пул потоков на `asyncio`, если ваша OCR‑библиотека предоставляет асинхронные API.  

Продолжайте экспериментировать — замените Tesseract, Azure Cognitive Services или Google Vision, и вы увидите, что тот же шаблон применим. Счастливого OCR‑инга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}