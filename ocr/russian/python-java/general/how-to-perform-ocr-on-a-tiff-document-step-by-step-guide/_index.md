---
category: general
date: 2026-01-12
description: Как быстро и точно выполнять OCR. Узнайте, как запускать OCR на документе,
  извлекать текст из TIFF, загружать изображение для OCR и задавать язык OCR в Python.
draft: false
keywords:
- how to perform ocr
- run ocr on document
- extract text from tiff
- load image for ocr
- set OCR language
language: ru
og_description: Как выполнить OCR в Python. Этот учебник покажет, как запустить OCR
  на документе, извлечь текст из TIFF, загрузить изображение для OCR и установить
  язык OCR.
og_title: Как выполнить OCR в TIFF‑документе – Полное руководство
tags:
- OCR
- Python
- Image Processing
title: Как выполнить OCR в TIFF‑документе – пошаговое руководство
url: /ru/python-java/general/how-to-perform-ocr-on-a-tiff-document-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR на TIFF‑документе – Полное руководство

Когда‑нибудь задумывались **как выполнить OCR** на отсканированном TIFF‑файле, не тратя часы на поиски подходящей библиотеки? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно извлечь текст из TIFF‑изображений, особенно если важны производительность и настройки языка.

В этом руководстве мы пройдем всё, что вам нужно знать: от установки OCR‑пакета, загрузки изображения для OCR, установки языка OCR, до окончательного **запуска OCR на документе** и получения чистого текста. К концу вы получите готовый к запуску скрипт, который можно добавить в любой проект.

> **Совет:** Хотя в примере используется общий модуль `ocr`, те же концепции применимы к Tesseract, EasyOCR или любому современному OCR‑движку, предоставляющему Python API.

---

## Что понадобится

- Python 3.8+ (подойдёт любая современная версия)
- Библиотека OCR, предоставляющая класс `OcrEngine` (в примере используется вымышленный пакет `ocr`; замените его на ваш реальный)
- Многостраничный TIFF‑файл, который вы хотите обработать (назовём его `big_document.tif`)
- Компьютер с минимум 4‑ядерным процессором, если планируете задавать количество потоков

Никаких внешних сервисов, без облачных ключей — только локальный код, который работает за секунды.

![пример выполнения OCR](/images/ocr-example.png "как выполнить OCR на TIFF‑документе")

*Текст alt изображения: как выполнить OCR на TIFF‑документе — предварительный просмотр извлечённого текста.*

## Шаг 1: Установить и импортировать OCR‑библиотеку

Сначала необходимо получить библиотеку на ваш компьютер. Большинство OCR‑пакетов находятся в PyPI, поэтому простая команда `pip install` решит задачу.

```bash
pip install ocr‑engine   # replace with the actual package name, e.g., pytesseract
```

Теперь импортируйте необходимые классы. Если вы используете Tesseract, строка импорта будет выглядеть иначе, но остальной код останется тем же.

```python
# Step 1: Import the OCR engine and image helper
import ocr                       # fictional package – swap with your real one
from ocr import OcrEngine, Image
```

*Почему это важно:* ранний импорт нужных символов предотвращает конфликты имён позже и делает скрипт более читаемым.

## Шаг 2: Создать и настроить OCR‑движок (установить язык OCR)

Настройка движка — это место, где вы **устанавливаете язык OCR** для точного распознавания. По умолчанию — английский, но вы можете переключиться на французский, немецкий или даже многоязычный режим одной строкой.

```python
# Step 2: Initialize the engine and set language
ocr_engine = OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH   # set OCR language to English
ocr_engine.set_thread_count(4)               # limit processing to 4 CPU cores
ocr_engine.set_memory_limit(512 * 1024 * 1024)  # 512 MB internal buffer
```

> **Зачем 4 потока?** На большинстве современных ноутбуков минимум четыре ядра, и ограничение количества потоков не позволяет процессу OCR захватывать весь компьютер — особенно полезно, когда скрипт работает на общем сервере.

Если нужен другой язык, просто замените `ocr.Language.ENGLISH` на `ocr.Language.FRENCH`, `ocr.Language.SPANISH` и т.д.

## Шаг 3: Загрузить изображение для OCR (Load Image for OCR)

Теперь мы **загружаем изображение для OCR**. Метод `Image.load` читает TIFF‑файл в память, автоматически обрабатывая многостраничные документы.

```python
# Step 3: Load the TIFF image you want to process
image_path = "YOUR_DIRECTORY/big_document.tif"
image = Image.load(image_path)   # load image for OCR
```

*Пограничный случай:* Если файл огромный, может закончиться оперативная память. В таком случае рассмотрите загрузку по одной странице с помощью `Image.load_page(page_number)` (если библиотека поддерживает это).

## Шаг 4: Запустить OCR на документе

Когда движок готов и изображение загружено, пора **запустить OCR на документе**. Метод `process` выполняет основную работу и возвращает объект результата.

```python
# Step 4: Execute OCR
ocr_result = ocr_engine.process(image)
```

Внутри движок разбивает изображение на текстовые блоки, запускает модель распознавания и объединяет результаты. Вызов блокирующий, то есть скрипт ждёт, пока весь TIFF будет обработан — идеально для пакетных задач.

## Шаг 5: Извлечь текст из TIFF и проверить вывод

Наконец, мы **извлекаем текст из TIFF**, обращаясь к атрибуту `text` результата. Выведем первые 200 символов для быстрой проверки.

```python
# Step 5: Show a preview of the recognized text
preview = ocr_result.text[:200]   # first 200 characters
print("Preview of OCR output:\n", preview)
```

**Ожидаемый вывод (пример):**

```
Preview of OCR output:
 In the United States, the Constitution guarantees the ...
```

Если нужен полный текст, просто используйте `ocr_result.text`. Для последующей обработки вы можете записать его в файл `.txt`:

```python
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(ocr_result.text)
```

## Полный рабочий пример

Объединив всё вместе, получаем готовый к запуску скрипт. Замените имя пакета‑заполнителя на то, которое вы действительно установили.

```python
# -*- coding: utf-8 -*-
"""
How to Perform OCR on a TIFF Document – Complete Example
"""

# Install the OCR library first:
# pip install ocr-engine   # adjust to your actual package

import ocr
from ocr import OcrEngine, Image

def main():
    # 1️⃣ Initialize and configure the engine
    engine = OcrEngine()
    engine.language = ocr.Language.ENGLISH
    engine.set_thread_count(4)
    engine.set_memory_limit(512 * 1024 * 1024)

    # 2️⃣ Load the TIFF image
    img_path = "YOUR_DIRECTORY/big_document.tif"
    img = Image.load(img_path)

    # 3️⃣ Run OCR on the loaded image
    result = engine.process(img)

    # 4️⃣ Show a short preview and save the full text
    print("First 200 chars of OCR output:")
    print(result.text[:200])

    with open("extracted_text.txt", "w", encoding="utf-8") as out_file:
        out_file.write(result.text)

    print("\n✅ Extraction complete – see 'extracted_text.txt' for full output.")

if __name__ == "__main__":
    main()
```

Запустите скрипт командой:

```bash
python ocr_tiff_example.py
```

Вы должны увидеть предварительный просмотр, выведенный в консоль, и файл `extracted_text.txt`, содержащий полную транскрипцию.

## Часто задаваемые вопросы и пограничные случаи

- **Что если TIFF содержит несколько страниц?**  
  Большинство OCR‑движков рассматривают каждую страницу как отдельное изображение. `ocr_result.text` будет содержать перевод строки между страницами. Если требуется обработка по страницам, используйте цикл с `Image.load_page(page_number)`.

- **Можно ли обработать PNG или JPEG вместо TIFF?**  
  Конечно. Метод `Image.load`, как правило, принимает любой формат, поддерживаемый Pillow или базовой библиотекой. Просто измените расширение файла.

- **Текст искажён — стоит ли менять язык?**  
  Да. Шаг `set OCR language` критически важен для неанглийских документов. Убедитесь, что языковой пакет установлен (например, `tesseract‑lang‑fra` для французского).

- **Не хватает памяти?**  
  Уменьшите `set_memory_limit` или обрабатывайте страницы по одной. Некоторые движки также позволяют уменьшать масштаб изображения перед распознаванием.

## Заключение

Вот и всё — лаконичное, полностью рабочее руководство о **как выполнить OCR** на TIFF‑файле с помощью Python. Мы рассмотрели всё: от установки библиотеки, настройки движка (включая **set OCR language**), **load image for OCR**, **run OCR on document**, и наконец **extract text from tiff**.  

Не стесняйтесь экспериментировать: изменять количество потоков, переключать языки или передавать вывод OCR в конвейер обработки естественного языка. Возможности безграничны, как только вы освоите основы.

Есть дополнительные вопросы? Оставьте комментарий ниже, и счастливого кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}