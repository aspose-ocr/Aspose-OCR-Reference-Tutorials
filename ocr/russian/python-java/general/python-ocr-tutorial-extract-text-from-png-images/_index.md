---
category: general
date: 2026-06-25
description: Учебник по OCR на Python, показывающий, как извлекать текст из PNG‑файлов,
  читать текстовые изображения и распознавать текст на изображениях с помощью простого,
  не требующего лицензии движка.
draft: false
keywords:
- python ocr tutorial
- extract text png
- read text image
- recognize image text
- load image for ocr
language: ru
og_description: Учебник по OCR на Python научит вас загружать изображение для OCR,
  извлекать текст из PNG‑файлов и распознавать текст на изображениях всего в несколько
  строк кода.
og_title: Учебник по OCR в Python – извлечение текста из PNG
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  headline: 'Python OCR Tutorial: Extract Text from PNG Images'
  type: TechArticle
- description: Python OCR tutorial that shows you how to extract text PNG files, read
    text image, and recognize image text using a simple, license‑free engine.
  name: 'Python OCR Tutorial: Extract Text from PNG Images'
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer (the library works with 3.7+ but 3.8+ is recommended).
      - Basic familiarity with pip and virtual environments. - An image file named
      `sample.png` (or any PNG you’d like to test) saved in a folder you can reference.'
  - name: 1. Low Contrast or Dark Backgrounds
    text: '```python # Increase contrast before recognition (optional step) image
      = image.adjust_contrast(1.5) # 1.0 = no change, >1 = higher contrast result
      = engine.recognize(image) ```'
  - name: 2. Skewed Text Lines
    text: '```python # Auto‑deskew the image image = image.deskew() result = engine.recognize(image)
      ```'
  - name: 3. Non‑English Characters
    text: 'If your PNG contains accented letters or non‑Latin scripts, initialise
      the engine with the appropriate language pack:'
  - name: 4. Very Large Images
    text: 'Processing a 4000×3000 PNG can be slow. Downscale it while preserving readability:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- Tutorial
title: 'Учебник по OCR в Python: извлечение текста из PNG‑изображений'
url: /ru/python-java/general/python-ocr-tutorial-extract-text-from-png-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Извлечение текста из PNG‑изображений

Когда‑то задавались вопросом, как **python ocr tutorial** может превратить скриншот чека в редактируемый текст? Вы не одиноки. Во многих реальных проектах нам нужно быстро *read text image* файлы, и делать это самостоятельно лучше, чем каждый раз копировать‑вставлять из графического интерфейса.  

В этом руководстве мы пройдём практический пример, который **extracts text PNG** файлы, покажет, как *load image for OCR*, и в конце выведет результат *recognize image text* — всё с бесплатным OCR‑движком только для оценки. Без лицензионных ключей, без тяжёлых зависимостей — только чистый Python и пара небольших пакетов.

## Что вы узнаете

- Как установить и импортировать лёгкую OCR‑библиотеку.  
- Точные шаги для **load image for OCR** и как избежать распространённых подводных камней.  
- Способы *read text image* файлов разного качества.  
- Советы по повышению точности при **extract text png** файлах.  
- Как отобразить распознанную строку и при желании записать её на диск.

К концу этого урока у вас будет переиспользуемый скрипт, который можно добавить в любой проект, требующий **recognize image text** «на лету». Никакой магии, только понятный код и объяснения.

### Предварительные требования

- Python 3.8 или новее (библиотека работает с 3.7+, но рекомендуется 3.8+).  
- Базовое знакомство с pip и виртуальными окружениями.  
- Файл изображения `sample.png` (или любой PNG, который хотите протестировать), сохранённый в папке, к которой есть доступ.

Если что‑то из этого вам незнакомо, сделайте паузу и настройте — поверьте, результат того стоит.

---

## Python OCR Tutorial – Настройка движка

Первым делом нам нужен объект OCR‑движка. Библиотека, которую мы будем использовать, представляет собой небольшую оболочку вокруг нативного OCR‑движка, работающего «из коробки» для оценки. Она не требует лицензионного ключа, что делает *python ocr tutorial* идеальным для быстрых прототипов.

```python
# Step 1: Install the OCR package (run once in your terminal)
# pip install simple-ocr-lib

# Step 2: Import the library and create an engine instance
import ocr

# No license needed for evaluation mode – the engine is ready to go
engine = ocr.OcrEngine()
```

**Почему это важно:** Создание движка изолирует OCR‑рантайм от остального кода, позволяя переиспользовать его для нескольких изображений без повторной инициализации тяжёлых ресурсов каждый раз.

---

## Load Image for OCR – Чтение PNG‑файла

Теперь, когда движок существует, нам нужно *load image for OCR*. Метод `Image.load` библиотеки принимает путь и автоматически декодирует PNG, JPEG, BMP и несколько других форматов.

```python
# Step 3: Load the PNG you want to process
image_path = "YOUR_DIRECTORY/sample.png"   # replace with your actual path
image = ocr.Image.load(image_path)
```

> **Pro tip:** Если ваш PNG содержит альфа‑канал, библиотека автоматически его отбросит. Однако для лучших результатов в задачах *read text image* держите изображение в градациях серого — это уменьшает шум и ускоряет распознавание.

---

## Recognize Image Text – Запуск OCR‑движка

Когда объект изображения готов, мы наконец можем **recognize image text**. Это ядро *python ocr tutorial* и требует всего одну строку кода.

```python
# Step 4: Perform OCR on the loaded image
result = engine.recognize(image)
```

**Что происходит «под капотом»?** Движок применяет серию предобработок (выравнивание, бинаризация), а затем передаёт битмап в нейронную сеть, обученную на миллионах символов. Поэтому вы часто получаете удивительно точный вывод даже на низкоразрешённых PNG‑изображениях.

---

## Отображение и сохранение извлечённого текста

Получить результат — здорово, но, скорее всего, вы захотите увидеть его или сохранить где‑то. Объект `result` раскрывает атрибут `text`, содержащий обычную строку.

```python
# Step 5: Print the recognized text to the console
print("Eval-mode result:", result.text)

# Optional: Save the text to a .txt file for later use
with open("extracted_text.txt", "w", encoding="utf-8") as f:
    f.write(result.text)
```

**Ожидаемый вывод** (при условии, что `sample.png` содержит «Hello, OCR!»):

```
Eval-mode result: Hello, OCR!
```

Если вместо читаемых символов вы получаете «мусор», см. следующий раздел с типичными исправлениями.

---

## Обработка типичных проблем при Extract Text PNG

Даже лучшие OCR‑движки спотыкаются о некоторые изображения. Ниже перечислены типичные препятствия и способы их преодоления.

### 1. Низкий контраст или тёмный фон

```python
# Increase contrast before recognition (optional step)
image = image.adjust_contrast(1.5)   # 1.0 = no change, >1 = higher contrast
result = engine.recognize(image)
```

### 2. Наклонённые строки текста

```python
# Auto‑deskew the image
image = image.deskew()
result = engine.recognize(image)
```

### 3. Неанглийские символы

Если ваш PNG содержит буквы с диакритическими знаками или нелатинские скрипты, инициализируйте движок с соответствующим языковым пакетом:

```python
engine = ocr.OcrEngine(languages=["eng", "spa"])   # English + Spanish
```

### 4. Очень большие изображения

Обработка PNG 4000×3000 может быть медленной. Уменьшите масштаб, сохранив читаемость:

```python
image = image.resize(width=1024)   # keep aspect ratio
result = engine.recognize(image)
```

Эти настройки являются частью надёжного *python ocr tutorial*, работающего за пределами «счастливого пути».

---

## Полный скрипт – Решение в одном файле

Ниже представлен полностью готовый к запуску скрипт, включающий все шаги и опциональные улучшения, обсуждённые выше. Скопируйте его в `ocr_extract.py` и выполните `python ocr_extract.py`.

```python
# ocr_extract.py
# Complete Python OCR tutorial – extract text from PNG images

import ocr
import sys
import os

def main(image_path):
    # Verify the file exists
    if not os.path.isfile(image_path):
        print(f"Error: File not found → {image_path}")
        sys.exit(1)

    # 1️⃣ Create the OCR engine (evaluation mode, no license needed)
    engine = ocr.OcrEngine()

    # 2️⃣ Load the image – this is the "load image for OCR" step
    image = ocr.Image.load(image_path)

    # Optional preprocessing for better accuracy
    # Uncomment any of the following lines as needed:
    # image = image.adjust_contrast(1.5)   # boost contrast
    # image = image.deskew()               # correct skew
    # image = image.resize(width=1024)     # downscale large images

    # 3️⃣ Recognize the text
    result = engine.recognize(image)

    # 4️⃣ Output the result
    print("Eval-mode result:", result.text)

    # 5️⃣ Save to a .txt file (useful for batch processing)
    txt_path = os.path.splitext(image_path)[0] + "_extracted.txt"
    with open(txt_path, "w", encoding="utf-8") as out_file:
        out_file.write(result.text)
    print(f"Extracted text saved to {txt_path}")

if __name__ == "__main__":
    # Pass the image path as a command‑line argument, e.g.:
    # python ocr_extract.py ./samples/sample.png
    if len(sys.argv) < 2:
        print("Usage: python ocr_extract.py <path_to_png>")
        sys.exit(1)
    main(sys.argv[1])
```

**Запуск:**  
```bash
python ocr_extract.py ./sample.png
```

Вы должны увидеть распознанную строку в консоли и файл `sample_extracted.txt`, созданный рядом с изображением.

---

## Визуальный обзор

![Python OCR tutorial – load image for OCR and extract text from PNG](/images/python-ocr-flow.png)

*Alt text:* *Python OCR tutorial diagram showing the flow from loading an image for OCR to extracting text PNG.*

Диаграмма иллюстрирует линейную последовательность: **load image for OCR** → **recognize image text** → **extract text PNG** и подчёркивает места, где можно добавить шаги предобработки.

---

## Заключение

Мы только что завершили **python ocr tutorial**, демонстрирующий, как *load image for OCR*, *recognize image text* и, наконец, **extract text png** файлы с помощью нескольких команд Python. Скрипт полностью рабочий, учитывает типичные граничные случаи и может быть расширен для пакетной обработки или поддержки нескольких языков.

Готовы к следующему вызову? Попробуйте подавать в движок PDF‑файлы, преобразованные в изображения, поэкспериментируйте с разными языковыми пакетами или интегрируйте шаг OCR в Flask‑API, чтобы ваше веб‑приложение могло читать загруженные скриншоты «на лету». Возможности автоматизации *read text image* практически безграничны.

Есть вопросы или «упрямое» изображение, которое не поддаётся? Оставляйте комментарий ниже, и будем разбираться вместе. Счастливого кодинга!

## Что вам стоит изучить дальше?

Следующие уроки охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}