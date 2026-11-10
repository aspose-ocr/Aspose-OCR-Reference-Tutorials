---
category: general
date: 2026-06-19
description: Выполните OCR на изображении с помощью библиотеки OCR для Python. Узнайте,
  как обнаруживать текст на изображении, распознавать текст из JPEG и эффективно извлекать
  текст из отсканированного изображения.
draft: false
keywords:
- perform OCR on image
- recognize text from jpeg
- detect text from image
- extract text from scanned image
- load image for OCR
language: ru
og_description: Выполняйте OCR изображения с помощью Python и извлекайте текст из
  отсканированных файлов. Это руководство пошагово проведёт вас через загрузку изображений,
  исправление наклона и распознавание текста.
og_title: Выполните OCR изображения в Python — Полное руководство по извлечению текста
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  headline: Perform OCR on Image in Python – Full Text Extraction Guide
  type: TechArticle
- description: Perform OCR on image using Python's ocr library. Learn how to detect
    text from image, recognize text from jpeg, and extract text from scanned image
    efficiently.
  name: Perform OCR on Image in Python – Full Text Extraction Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed (the example uses the `ocr` package available via
      `pip install ocr-lib` – replace with your actual library name). - Basic familiarity
      with Python functions and virtual environments. - An image file (JPEG, PNG,
      TIFF) you want to process; we’ll use `skewed_page.jpg` as a placeh'
  - name: Recognize Text from JPEG vs PNG
    text: 'Both formats are supported, but JPEG compression can introduce artifacts
      that confuse the engine. If you notice frequent mis‑recognitions, try converting
      the JPEG to PNG first:'
  - name: Detect Text from Image with Multiple Languages
    text: 'If your document mixes English and Spanish, set a multilingual mode:'
  - name: Extract Text from Scanned PDFs
    text: 'For PDFs, you need to rasterize each page into an image first. Libraries
      like `pdf2image` make this painless:'
  type: HowTo
- questions:
  - answer: Absolutely. The library works without a GUI; just ensure the necessary
      native binaries (e.g., Tesseract) are installed on the server.
    question: Can I run this on a headless server?
  - answer: Consider adding a sharpening filter before `engine.recognize`. Many OCR
      libraries expose `image_preprocessing.sharpen = True` or you can use OpenCV’s
      `cv2.GaussianBlur` in reverse.
    question: What if the image is blurry?
  - answer: 'Yes. Wrap `perform_ocr` in a loop over a list of file paths, ## What
      Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
      - [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
      - [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

      {{< /blocks/products/pf/tutorial-page-section >}} {{< /blocks/products/pf/main-container
      >}} {{< /blocks/products/pf/main-wrap-class >}} {{< blocks/products/products-backtop-button
      >}}'
    question: Does the script support batch processing?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Выполнить OCR изображения в Python – Полное руководство по извлечению текста
url: /ru/python-java/general/perform-ocr-on-image-in-python-full-text-extraction-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении в Python – Полное руководство по извлечению текста

Когда‑то вам нужно **выполнить OCR на изображении**, но код выглядел непонятно? Вы не одиноки. Будь то преобразование кучи отсканированных чеков в поисковые PDF или извлечение подписей из JPEG для проекта по data‑science, умение распознавать текст из JPEG и других форматов — обязательный навык для любого разработчика сегодня.

В этом руководстве мы пройдём через полностью рабочий пример, показывающий, как **обнаружить текст на изображениях**, **извлечь текст из отсканированных изображений**, и даже **загрузить изображение для OCR** всего в несколько строк. К концу вы получите готовый к продакшну фрагмент кода, который можно вставить в свои проекты — без пропущенных импортов и неопределённых «см. документацию» сокращений.

## Что вы построите

- Маленький скрипт на Python, который создаёт OCR‑движок, включает авто‑выравнивание, загружает JPEG (или любой поддерживаемый формат) и выводит распознанный текст.
- Объяснения **почему** каждое настройка важна, а не только **как** её написать.
- Советы по работе с многостраничными PDF, нелатинскими языками и типичными проблемами, такими как размытые сканы.

### Предпосылки

- Установлен Python 3.8+ (в примере используется пакет `ocr`, доступный через `pip install ocr-lib` — замените на название вашей библиотеки).
- Базовое знакомство с функциями Python и виртуальными окружениями.
- Файл изображения (JPEG, PNG, TIFF), который вы хотите обработать; в примере используется `skewed_page.jpg` как заполнитель.

> **Pro tip:** Если вы работаете в Windows, запустите терминал от имени администратора при установке OCR‑библиотеки, чтобы избежать проблем с правами доступа.

---

## Выполнить OCR на изображении – Настройка и конфигурация

Первое, что нужно — чистый экземпляр OCR‑движка. Считайте его мозгом операции; без правильной конфигурации даже самое чёткое изображение вернёт бессмыслицу.

```python
# Step 1: Import the OCR library and create an engine
import ocr

engine = ocr.OcrEngine()
# Set the recognition language – English works for most cases
engine.language = ocr.Language.English
```

**Почему это важно:**  
Установка `engine.language` ограничивает набор символов, которые ожидает OCR‑движок, что резко повышает точность. Если пропустить этот шаг, движок будет угадывать, часто ошибаясь даже в простых словах.

---

## Включить автоматическое выравнивание – исправление наклонённых сканов

Отсканированные страницы редко бывают идеально ровными. Небольшой наклон может нарушить сегментацию символов, превратив “Hello” в “H3llo”. Флаг `auto_deskew` делает всю тяжёлую работу за вас.

```python
# Step 2: Turn on automatic deskew to straighten tilted images
engine.image_preprocessing.auto_deskew = True
```

**Пограничный случай:** Если вы знаете, что ваши изображения уже выровнены, отключение выравнивания может сэкономить несколько миллисекунд времени обработки — полезно при работе с тысячами страниц в пакетном режиме.

---

## Загрузить изображение для OCR – поддержка JPEG, PNG, TIFF

Теперь мы действительно **загружаем изображение для OCR**. Метод `ocr.Image.load` гибок; он принимает путь к любому поддерживаемому растровому формату.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/skewed_page.jpg"
image = ocr.Image.load(image_path)
```

> **Почему этот шаг критичен:** Библиотека читает файл во внутренний bitmap, при необходимости преобразуя цветовое пространство. Пропуск этого шага и передача необработанного потока байтов вызовет `FileNotFoundError` или, что ещё хуже, тихо вернёт пустой результат.

Если вам нужно **распознать текст из JPEG** файлов, просто убедитесь, что расширение файла `.jpeg` или `.jpg`. Тот же вызов работает и для PNG (`.png`) или TIFF (`.tif`) без изменений.

---

## Выполнить OCR на изображении – запуск движка

С движком, подготовленным и изображением в памяти, пришло время **выполнить OCR на изображении**. Эта одна строка делает всю тяжёлую работу: предобработку, сегментацию, классификацию и сборку текста.

```python
# Step 4: Run OCR and capture the result object
result = engine.recognize(image)
```

**Что происходит «под капотом»?**  
- Движок применяет трансформацию выравнивания (если включена).  
- Запускает нейронную сеть или бекенд Tesseract для идентификации символов.  
- Наконец, склеивает символы в слова и строки, возвращая богатый объект `result`.

---

## Извлечь текст из отсканированного изображения – вывод результатов

Последний шаг — **извлечь текст из отсканированного изображения** и отобразить его. Атрибут `result.text` содержит текстовое представление.

```python
# Step 5: Print the detected text to the console
print("Detected text:")
print(result.text)
```

Типичный вывод выглядит так:

```
Detected text:
Invoice #12345
Date: 2023‑09‑01
Total: $1,234.56
Thank you for your business!
```

Если OCR‑движок не найдёт ни одного символа, `result.text` будет пустой строкой. В этом случае проверьте качество изображения или попробуйте отрегулировать свойство `engine.confidence_threshold` (если ваша библиотека поддерживает его).

---

## Обработка распространённых вариантов

### Распознавать текст из JPEG vs PNG

Оба формата поддерживаются, но сжатие JPEG может добавить артефакты, сбивающие движок. Если вы замечаете частые ошибки распознавания, попробуйте сначала конвертировать JPEG в PNG:

```python
from PIL import Image
Image.open(image_path).save("temp.png", format="PNG")
image = ocr.Image.load("temp.png")
```

### Обнаружить текст на изображении с несколькими языками

Если ваш документ содержит английский и испанский, включите многоязычный режим:

```python
engine.language = ocr.Language.English | ocr.Language.Spanish
```

Движок тогда будет учитывать оба алфавита при распознавании.

### Извлечь текст из отсканированных PDF

Для PDF необходимо сначала растеризовать каждую страницу в изображение. Библиотеки вроде `pdf2image` делают это без труда:

```python
from pdf2image import convert_from_path

pages = convert_from_path("document.pdf", dpi=300)
for i, page_image in enumerate(pages):
    image = ocr.Image.from_pil(page_image)   # assuming the library accepts a PIL image
    result = engine.recognize(image)
    print(f"Page {i+1} text:")
    print(result.text)
```

---

## Полный рабочий пример

Ниже полный скрипт, который можно скопировать в файл `ocr_demo.py`. В нём есть обработка ошибок и небольшой помощник для измерения времени выполнения.

```python
import ocr
import time
import sys
from pathlib import Path

def perform_ocr(image_path: str) -> str:
    """
    Perform OCR on a given image file and return the extracted text.
    Handles auto‑deskew and basic error reporting.
    """
    if not Path(image_path).exists():
        sys.exit(f"❌ Error: File not found – {image_path}")

    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.image_preprocessing.auto_deskew = True

    try:
        image = ocr.Image.load(image_path)
    except Exception as e:
        sys.exit(f"❌ Failed to load image: {e}")

    start = time.time()
    result = engine.recognize(image)
    elapsed = time.time() - start

    if not result.text.strip():
        print("⚠️ No text detected. Try a higher‑resolution image or adjust preprocessing.")
    else:
        print(f"✅ OCR completed in {elapsed:.2f}s")
        print("Detected text:")
        print(result.text)

    return result.text

if __name__ == "__main__":
    # Replace with the path to your JPEG/PNG/TIFF file
    perform_ocr("YOUR_DIRECTORY/skewed_page.jpg")
```

**Ожидаемый вывод** (при чистом скане):

```
✅ OCR completed in 0.87s
Detected text:
Lorem ipsum dolor sit amet,
consectetur adipiscing elit.
```

---

## Часто задаваемые вопросы

**В: Можно ли запускать это на сервере без графического интерфейса?**  
О: Конечно. Библиотека работает без GUI; просто убедитесь, что необходимые нативные бинарники (например, Tesseract) установлены на сервере.

**В: Что делать, если изображение размыто?**  
О: Попробуйте добавить фильтр резкости перед `engine.recognize`. Многие OCR‑библиотеки предоставляют `image_preprocessing.sharpen = True` или можно использовать обратный `cv2.GaussianBlur` из OpenCV.

**В: Поддерживает ли скрипт пакетную обработку?**  
О: Да. Оберните `perform_ocr` в цикл по списку путей к файлам,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}