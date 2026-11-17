---
category: general
date: 2026-09-19
description: Учебник по OCR на Python показывает, как преобразовать PNG в текст с
  помощью Aspose OCR. Изучите извлечение текста OCR в Python и извлекайте текст из
  отсканированных изображений.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- python OCR tutorial
- convert PNG to text
- OCR text extraction python
- extract text image python
- extract text scanned image
language: ru
lastmod: 2026-09-19
og_description: Учебник по OCR на Python проведёт вас через процесс преобразования
  PNG в текст с помощью Aspose OCR. Овладейте извлечением текста OCR в Python и извлекайте
  текст из отсканированных изображений.
og_image_alt: Screenshot of Python OCR code extracting text from a PNG image
og_title: Учебник по OCR в Python — преобразование PNG в текст с помощью Aspose
schemas:
- author: Aspose
  dateModified: '2026-09-19'
  description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  headline: 'Python OCR tutorial: convert PNG to text with Aspose'
  type: TechArticle
- description: Python OCR tutorial shows how to convert PNG to text using Aspose OCR.
    Learn OCR text extraction python and extract text from scanned images.
  name: 'Python OCR tutorial: convert PNG to text with Aspose'
  steps:
  - name: Expected output
    text: 'If `sample.png` contains the sentence “Hello, world!”, the console will
      show:'
  - name: 1. Non‑PNG formats
    text: Even though this tutorial focuses on **convert PNG to text**, you might
      receive JPEG or TIFF files. The same code works; just change the file extension
      in `load_image`.
  - name: 2. Low‑resolution images
    text: 'OCR accuracy drops below 150 dpi. If you encounter poor results, upscale
      the image first using Pillow:'
  - name: 3. Extracting text from a scanned image with multiple languages
    text: 'Set a comma‑separated list of language codes:'
  - name: 4. Large documents
    text: 'Processing many pages in a single run can exhaust memory. Process each
      page individually:'
  type: HowTo
tags:
- python
- OCR
- image processing
title: 'Учебник по OCR на Python: преобразование PNG в текст с помощью Aspose'
url: /ru/python/general/python-ocr-tutorial-convert-png-to-text-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial: конвертация PNG в текст с Aspose

Если вам нужен **python OCR tutorial**, который преобразует PNG‑изображение в редактируемый текст, это руководство предоставляет полное, готовое к запуску решение. Вы увидите, как установить библиотеку Aspose OCR, загрузить изображение, запустить движок распознавания и вывести результаты — всё за несколько лаконичных шагов.

Сканирование документа и извлечение из него текста может быть утомительным, особенно когда приходится работать с разными форматами изображений и настройками языка. Это руководство убирает догадки, показывая точно, какие методы вызывать и почему они важны, чтобы вы могли сосредоточиться на интеграции OCR в свои приложения.

Вы также узнаете, как **convert PNG to text**, справляться с распространёнными подводными камнями и адаптировать код для других типов изображений, таких как JPEG или TIFF. К концу вы сможете уверенно извлекать текст из любого отсканированного изображения.

## Prerequisites

Перед началом убедитесь, что у вас есть:

* Python 3.8 или новее установлен.
* Подключение к интернету для загрузки пакета Aspose OCR.
* PNG‑изображение (или любой поддерживаемый формат), содержащее читаемый текст.

Вам **не** требуется отдельный OCR‑движок или внешние бинарные файлы — Aspose OCR включает всё необходимое.

## Step 1: Install the Aspose OCR package

Первый шаг — добавить библиотеку в вашу среду. Aspose предоставляет чисто‑Python пакет, который можно установить через pip.

```bash
pip install aspose-ocr
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv venv`), чтобы изолировать зависимости от других проектов.

Установка пакета делает доступным модуль `aspose.ocr`, который содержит класс `OcrEngine`, используемый на протяжении всего руководства.

## Step 2: Import the OCR engine class

Теперь, когда пакет установлен, импортируйте класс, управляющий процессом распознавания.

```python
# Step 2: Import the OCR engine class
from aspose.ocr import OcrEngine
```

`OcrEngine` инкапсулирует всю логику загрузки изображений, настройки языка и извлечения текста. Импортировать его в начале скрипта — стандартная практика в Python, которая делает код аккуратным.

## Step 3: Create an instance of the OCR engine

Создание экземпляра даёт вам свежий движок с настройками по умолчанию. Позже вы сможете изменить свойства, такие как язык или предобработку изображения.

```python
# Step 3: Create an instance of the OCR engine
engine = OcrEngine()
```

Объект `engine` представляет одну OCR‑сессию. Повторное использование того же экземпляра для нескольких изображений может повысить производительность, так как внутренние ресурсы кэшируются.

## Step 4: Load the image you want to process

Укажите путь к PNG‑файлу, который хотите конвертировать. Метод `load_image` принимает любой формат, поддерживаемый Aspose OCR, поэтому вы также можете передать JPEG, BMP или TIFF файлы.

```python
# Step 4: Load the image you want to process
engine.load_image("YOUR_DIRECTORY/sample.png")
```

Если файл не найден, `load_image` выбрасывает `FileNotFoundError`. Для продакшн‑кода оберните вызов в блок try/except, чтобы вывести понятное сообщение об ошибке.

## Step 5: Perform OCR to extract text from the image

Вызов `recognize` запускает конвейер распознавания и возвращает извлечённую строку. Метод автоматически обрабатывает анализ макета, сегментацию символов и определение языка (по умолчанию — English).

```python
# Step 5: Perform OCR to extract text from the image
text = engine.recognize()
```

Вы можете изменить язык перед вызовом `recognize`:

```python
engine.language = "fr"   # for French text
```

Эта гибкость полезна, когда вам нужен **OCR text extraction python** для многоязычных документов.

## Step 6: Output the recognized text

Наконец, выведите или сохраните результат. Для быстрой проверки `print` отображает необработанную строку в консоли.

```python
# Step 6: Output the recognized text
print(text)
```

### Expected output

Если `sample.png` содержит предложение «Hello, world!», консоль покажет:

```
Hello, world!
```

Вывод может включать переносы строк или лишние пробелы в зависимости от оригинального макета. Вы можете пост‑обработать строку с помощью `str.strip()` или регулярных выражений, чтобы очистить её.

## Handling common edge cases

### 1. Non‑PNG formats

Несмотря на то, что в этом руководстве основной упор делается на **convert PNG to text**, вы можете получать JPEG или TIFF файлы. Тот же код работает; просто измените расширение файла в `load_image`.

```python
engine.load_image("scanned_page.tiff")
```

### 2. Low‑resolution images

Точность OCR падает ниже 150 dpi. Если результаты неудовлетворительные, сначала увеличьте изображение с помощью Pillow:

```python
from PIL import Image

img = Image.open("sample.png")
high_res = img.resize((img.width * 2, img.height * 2), Image.LANCZOS)
high_res.save("sample_high_res.png")
engine.load_image("sample_high_res.png")
```

### 3. Extracting text from a scanned image with multiple languages

Установите список кодов языков, разделённых запятыми:

```python
engine.language = "en,es,de"
```

Aspose OCR попытается распознать символы всех указанных языков.

### 4. Large documents

Обработка большого количества страниц за один запуск может исчерпать память. Обрабатывайте каждую страницу отдельно:

```python
for page_path in ["page1.png", "page2.png", "page3.png"]:
    engine.load_image(page_path)
    print(engine.recognize())
```

## Full, runnable script

Собрав все шаги вместе, вы получаете автономную программу, которую можно скопировать, вставить и выполнить.

```python
# python_ocr_tutorial.py
# Complete script for extracting text from a PNG image using Aspose OCR

# Install the library first:
# pip install aspose-ocr

from aspose.ocr import OcrEngine

def extract_text(image_path: str) -> str:
    """
    Loads an image and returns the recognized text.
    Parameters:
        image_path: Path to the PNG (or other supported) image.
    Returns:
        Recognized text as a string.
    """
    engine = OcrEngine()          # Create OCR engine instance
    engine.load_image(image_path) # Load the target image
    return engine.recognize()     # Perform OCR and return result

if __name__ == "__main__":
    # Replace with the actual path to your image
    path = "YOUR_DIRECTORY/sample.png"
    try:
        result = extract_text(path)
        print("=== Recognized Text ===")
        print(result)
    except Exception as e:
        print(f"Error during OCR processing: {e}")
```

Запустите скрипт командой:

```bash
python python_ocr_tutorial.py
```

Вы должны увидеть извлечённый текст, выведенный в консоль.

## Conclusion

Это **python OCR tutorial** продемонстрировало, как **convert PNG to text** с помощью Aspose OCR, охватив установку, загрузку изображений, распознавание и вывод результатов. Теперь у вас есть надёжный шаблон для **OCR text extraction python**, и вы можете адаптировать код для **extract text image python** из любого отсканированного документа.

Дальше можно рассмотреть:

* Интеграцию скрипта в веб‑сервис (например, Flask) для предоставления OCR в виде API.
* Сохранение извлечённого текста в базе данных для поисковых архивов.
* Эксперименты с различными настройками языка для обработки многоязычных сканов.

Счастливого кодинга и приятного превращения изображений в поисковый, редактируемый текст!

## What Should You Learn Next?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Конвертация изображения в текст: извлечение текста из изображения с помощью Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Python OCR Tutorial: извлечение текста таблиц из изображений](/ocr/english/python-java/general/python-ocr-tutorial-extract-table-text-from-images/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}