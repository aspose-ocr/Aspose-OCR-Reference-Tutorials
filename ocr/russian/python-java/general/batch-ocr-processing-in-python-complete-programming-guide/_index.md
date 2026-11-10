---
category: general
date: 2026-06-25
description: Пакетная обработка OCR в Python стала простой. Узнайте, как извлекать
  текст из группы изображений и освоить пакетное извлечение текста из изображений
  с помощью параллельных потоков.
draft: false
keywords:
- batch OCR processing
- extract text from image batch
- batch image text extraction
language: ru
og_description: Пакетная обработка OCR в Python позволяет быстро извлекать текст из
  набора изображений. Этот учебник проведёт вас через параллельный OCR с понятными
  примерами кода.
og_title: Пакетная обработка OCR в Python — Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  headline: Batch OCR Processing in Python – Complete Programming Guide
  type: TechArticle
- description: Batch OCR processing in Python made easy. Learn how to extract text
    from image batch and master batch image text extraction with parallel threads.
  name: Batch OCR Processing in Python – Complete Programming Guide
  steps:
  - name: Missing or Corrupt Images
    text: If an image can’t be opened, most OCR libraries raise an exception that
      aborts the whole batch. Wrap the call in a `try/except` inside the batch function
      or filter out problematic files beforehand (see the sanity check in Step 1).
  - name: Language & DPI Settings
    text: For multilingual documents, pass a `langs` parameter (e.g., `langs=['en',
      'de']`). If your scans are low‑resolution, consider pre‑processing with `Pillow`
      to upscale to 300 DPI before OCR—this often boosts accuracy.
  - name: Memory Constraints
    text: 'Eight threads can eat RAM, especially with large images. If you hit memory
      errors, lower `max_threads` or process the list in smaller chunks:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: Пакетная обработка OCR в Python — Полное руководство по программированию
url: /ru/python-java/general/batch-ocr-processing-in-python-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Пакетная обработка OCR в Python — Полное руководство по программированию

Когда‑то вам понадобилась **пакетная обработка OCR**, но вы не знали, как выполнить её эффективно на десятках отсканированных страниц? Вы не одиноки — разработчики часто сталкиваются с проблемой, пытаясь извлечь текст из пакета изображений, не перегружая процессор.  

В этом руководстве мы покажем простой способ **извлечения текста из пакета изображений** с помощью OCR‑движка Python, запустим работу до восьми потоков и в конце подсчитаем, сколько символов принёс каждый файл. К концу вы получите переиспользуемый скрипт, который обрабатывает **пакетное извлечение текста из изображений** как профессионал.

## Что покрывает этот учебник

Мы пройдём три практических шага:

1. Сформировать список файлов‑изображений, которые нужно распознать.  
2. Запустить OCR‑движок параллельно с `max_threads=8`.  
3. Пройтись по результатам и вывести лаконичное резюме.

Никаких внешних сервисов, никаких экзотических библиотек — только чистый Python и типичный OCR‑обёртка (например, `ocr` из `easyocr` или кастомная обёртка). Если у вас установлен Python 3.8+ и OCR‑пакет, вы готовы копировать‑вставлять и запускать.

---

## Шаг 1: Подготовьте список файлов‑изображений для пакетной обработки OCR

Первое, что нужно — собрать пути к изображениям. Представьте это как список покупок для OCR‑движка; каждая запись указывает на PNG, JPEG или TIFF, содержащий текст, который вы хотите прочитать.

```python
# Step 1: Prepare a list of image files to be recognized
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.png",
    "YOUR_DIRECTORY/page3.png",
    "YOUR_DIRECTORY/page4.png",
    "YOUR_DIRECTORY/page5.png"
]

# Quick sanity check – make sure the files exist
import os
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"These files are missing: {missing}")
```

**Почему это важно:**  
Создание списка заранее позволяет OCR‑движку работать в истинном пакетном режиме. Это также даёт единственное место, где можно добавить или удалить файлы, не меняя логику обработки позже. Проверка существования файлов предотвращает печально известный краш «файл не найден» посередине длительного запуска.

---

## Шаг 2: Запустите OCR на пакете с параллельными потоками (Extract Text from Image Batch)

Теперь передаём список OCR‑движку. Большинство современных OCR‑обёрток предоставляют метод `recognize_batch`, принимающий параметр `max_threads`. Установив его в `8`, мы говорим библиотеке поднять восемь рабочих потоков, что на четырёхъядерном процессоре с гипертрейдингом может значительно сократить время обработки.

```python
# Step 2: Run OCR on the batch, allowing up to 8 parallel threads
# Assuming `ocr` is a module that provides OcrEngine with recognize_batch()
import ocr

batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# batch_results is a list of Result objects, each with a .text attribute
```

**Почему параллелизм помогает:**  
OCR требует много процессорных ресурсов; каждое изображение проходит через нейронную сеть или устаревший движок. Обрабатывать их последовательно может быть мучительно медленно, особенно для сканов высокого разрешения. Параллельные потоки задействуют все ядра, превращая 5‑минутную задачу в 1‑минутную на типичном железе.

**Совет:** Если вы используете `easyocr`, вызов выглядит как `reader.readtext(image_path, detail=0)` внутри цикла. Наша абстракция `recognize_batch` скрывает эту сложность, но при желании вы можете заменить её собственным `ThreadPoolExecutor`, если библиотека не поддерживает пакетный режим.

---

## Шаг 3: Пройдитесь по результатам и подведите итог пакетного извлечения текста из изображений

После завершения OCR у вас будет список объектов‑результатов. Сопоставим оригинальные пути файлов с соответствующим выводом OCR и выведем аккуратную строку для каждого изображения, указывая, сколько символов было распознано.

```python
# Step 3: Iterate through the results and display character counts
for file_path, result in zip(image_files, batch_results):
    # result.text holds the raw extracted string
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Что вы увидите:**  

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

**Зачем нужен этот шаг:**  
Быстрый подсчёт символов сразу показывает, обработано ли изображение корректно. Неожиданно низкое значение может указывать на размытый скан, неверную настройку языка или повреждённый файл — проблемы, которые можно решить до перехода к дальнейшему анализу.

---

## Бонус: Обработка граничных случаев и распространённых подводных камней

### Отсутствующие или повреждённые изображения  
Если изображение не может быть открыто, большинство OCR‑библиотек бросают исключение, которое прерывает весь пакет. Оберните вызов в `try/except` внутри функции пакетной обработки или отфильтруйте проблемные файлы заранее (см. проверку в Шаге 1).

### Настройки языка и DPI  
Для многоязычных документов передайте параметр `langs` (например, `langs=['en', 'de']`). Если ваши сканы низкого разрешения, рассмотрите предобработку с помощью `Pillow` для увеличения до 300 DPI перед OCR — это часто повышает точность.

### Ограничения памяти  
Восемь потоков могут съедать ОЗУ, особенно при больших изображениях. Если возникнут ошибки памяти, уменьшите `max_threads` или обрабатывайте список небольшими порциями:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(image_files, 3):  # process three images at a time
    results = ocr.OcrEngine.recognize_batch(chunk, max_threads=3)
    # handle results...
```

---

## Полный рабочий скрипт

Объединив всё вместе, получаем полностью готовый к запуску пример. Замените `"YOUR_DIRECTORY"` на путь к папке с вашими PNG‑файлами и убедитесь, что установлен модуль `ocr`.

```python
#!/usr/bin/env python3
"""
Batch OCR Processing Script
Extracts text from an image batch using parallel threads and prints character counts.
"""

import os
import ocr  # Replace with your OCR library import, e.g., from easyocr import Reader

# -------------------------------------------------
# Step 1: Define the list of image files
# -------------------------------------------------
image_dir = "YOUR_DIRECTORY"
image_files = [
    os.path.join(image_dir, f"page{i}.png") for i in range(1, 6)
]

# Verify that all files exist
missing = [p for p in image_files if not os.path.isfile(p)]
if missing:
    raise FileNotFoundError(f"Missing image files: {missing}")

# -------------------------------------------------
# Step 2: Run OCR in parallel (max 8 threads)
# -------------------------------------------------
# The OcrEngine is a placeholder – adapt to your library's API
batch_results = ocr.OcrEngine.recognize_batch(image_files, max_threads=8)

# -------------------------------------------------
# Step 3: Report how many characters each image yielded
# -------------------------------------------------
for file_path, result in zip(image_files, batch_results):
    char_count = len(result.text)
    print(f"{file_path} → {char_count} characters recognized")
```

**Ожидаемый вывод** (числа будут другими):

```
YOUR_DIRECTORY/page1.png → 1245 characters recognized
YOUR_DIRECTORY/page2.png → 987 characters recognized
YOUR_DIRECTORY/page3.png → 1103 characters recognized
YOUR_DIRECTORY/page4.png → 1320 characters recognized
YOUR_DIRECTORY/page5.png → 845 characters recognized
```

Запустите скрипт командой `python batch_ocr.py` и наблюдайте, как терминал заполняется лаконичной статистикой.

---

## Визуальный обзор

![Batch OCR processing flow diagram](image-placeholder.png "Diagram illustrating batch OCR processing steps")

*Текст alt изображения:* *Диаграмма потоков пакетной обработки OCR, показывающая создание списка файлов, параллельное выполнение OCR и суммирование результатов.*

---

## Заключение

Теперь у вас есть надёжная база для **пакетной обработки OCR** в Python. Подготовив чистый список изображений, используя параллельные потоки для **extract text from image batch** и подводя итоги, вы превращаете утомительную ручную задачу в быструю, повторяемую конвейерную обработку.  

Дальше вы можете:

- Сохранять каждый `result.text` в файл `.txt` для последующего NLP.  
- Сочетать подсчёт символов с оценками уверенности, чтобы отфильтровать низкокачественные страницы.  
- Интегрировать скрипт в более крупный процесс ingest‑а документов, возможно, наполняя поисковый индекс.

Будь то оцифровка архивов, создание приложения для сканирования чеков или подготовка обучающих данных для языковой модели, описанные здесь концепции масштабируются до сотен и тысяч файлов с минимальными доработками.

Есть вопросы о настройках языка, предобработке изображений или развертывании в облаке? Оставляйте комментарий или смотрите связанные учебники по *Python image preprocessing* и *asynchronous OCR with asyncio*. Приятного кодинга!

## Что вам стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}