---
category: general
date: 2026-01-12
description: Быстро выполняйте OCR для PNG‑файлов с помощью Python. Узнайте, как извлекать
  текст из изображения и счета, а также загружать изображение для OCR с использованием
  Aspose.OCR.
draft: false
keywords:
- run OCR on PNG
- extract text from image
- extract text from invoice
- load image for OCR
- Aspose OCR Python
- JSON to CSV conversion
language: ru
og_description: Запустите OCR на PNG мгновенно. Это руководство показывает, как извлечь
  текст из изображения и счета, загрузить изображение для OCR и сохранить результаты
  в формате JSON и CSV.
og_title: Запуск OCR на PNG – Полный учебник по Python
tags:
- OCR
- Python
- Image Processing
title: Run OCR on PNG – Complete Python Guide to Extract Text from Images
url: /ru/python-java/general/run-ocr-on-png-complete-python-guide-to-extract-text-from-im/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на PNG – Полное руководство Python по извлечению текста из изображений

Когда‑то вам нужно было **запустить OCR на PNG**‑файлах, но вы не знали, какая библиотека даст чистый, структурированный результат? Вы не одиноки. Во многих реальных проектах — например, автоматизация обработки счетов или сканирование чеков — первый шаг — это **извлечение текста из изображения**, а PNG часто используется, потому что сохраняет без потерь.

В этом руководстве мы пройдем практический пример с пакетом Aspose.OCR для Python. К концу вы узнаете, как **загрузить изображение для OCR**, получить каждую строку текста, превратить данные в аккуратный JSON‑объект и даже сохранить их в CSV для дальнейшей обработки. Без лишних слов, только готовое к использованию решение.

## Что вы узнаете

- Как установить и импортировать библиотеку Aspose.OCR.  
- Точные шаги для **запуска OCR на PNG** и работы с объектом результата.  
- Способы **извлечения текста из счета** и форматирования вывода в JSON или CSV.  
- Советы по работе с изображениями низкого контраста, многоязычными документами и оценками уверенности.  
- Полный пример кода, который можно скопировать и выполнить сразу.

> **Prerequisite:** Python 3.8+ и базовое знакомство с pip. Если вы никогда не работали с Aspose, не переживайте — это руководство покрывает всё необходимое для старта.

---

## Шаг 1 – Установить Aspose.OCR и подготовить окружение

Прежде чем мы сможем **запустить OCR на PNG**, библиотека должна быть установлена в вашей системе.

```bash
pip install aspose-ocr
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv venv`), чтобы изолировать зависимости. Это предотвращает конфликты версий, если вы работаете над несколькими проектами одновременно.

После установки импортируйте необходимые модули:

```python
# Step 1: Import the OCR and JSON modules
import asposeocr as ocr
import json
```

Здесь мы подключаем `asposeocr` для основной работы и встроенную библиотеку `json` для последующей сериализации.

---

## Шаг 2 – Создать OCR‑движок и задать язык

OCR‑движок — это ядро, которое действительно читает пиксели. Для большинства английских счетов вам понадобится пакет английского языка:

```python
# Step 2: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Why this matters:** Указание языка сужает набор символов, что повышает точность и ускоряет обработку. Если понадобится поддержка нескольких языков, просто замените `ocr.Language.ENGLISH` на нужный enum.

---

## Шаг 3 – Загрузить изображение для OCR

Теперь мы **загружаем изображение для OCR**. Метод `Image.load` принимает путь к файлу и работает с PNG, JPEG, BMP и другими форматами.

```python
# Step 3: Load the image you want to analyze
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

> **Edge case:** Если PNG необычно большой (более 5 МБ), рассмотрите возможность предварительного изменения размера, чтобы снизить потребление памяти. Это можно сделать в одну строку с помощью Pillow:

```python
# Optional: Resize large PNGs
from PIL import Image as PilImage
pil_img = PilImage.open(image_path)
pil_img.thumbnail((2000, 2000), PilImage.ANTIALIAS)
pil_img.save("temp_resized.png")
image = ocr.Image.load("temp_resized.png")
```

---

## Шаг 4 – Запустить OCR на PNG и получить результат

Когда движок готов и изображение загружено, пришло время **запустить OCR на PNG** и получить структурированный результат.

```python
# Step 4: Run the OCR process on the loaded image
ocr_result = ocr_engine.process(image)
```

Объект `ocr_result` содержит коллекцию элементов `OcrRegion`, каждый из которых имеет распознанный текст и оценку уверенности (0‑100). Здесь вы получаете детальные данные, необходимые для **извлечения текста из счета**.

---

## Шаг 5 – Преобразовать результат в JSON и красиво вывести

Большинство downstream‑систем любят JSON, поэтому мы превратим вывод OCR в красиво отформатированную строку.

```python
# Step 5: Convert the OCR result to a formatted JSON string and display it
json_str = ocr_result.to_json()
ocr_data = json.loads(json_str)

# Pretty‑print with indentation
print(json.dumps(ocr_data, indent=2))
```

### Пример вывода

```json
{
  "pages": [
    {
      "regions": [
        {
          "text": "Invoice #12345",
          "confidence": 98.7,
          "bounds": { "x": 50, "y": 20, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2025‑12‑01",
          "confidence": 96.4,
          "bounds": { "x": 50, "y": 60, "width": 180, "height": 25 }
        },
        {
          "text": "Total Amount: $1,250.00",
          "confidence": 99.1,
          "bounds": { "x": 50, "y": 300, "width": 250, "height": 30 }
        }
      ]
    }
  ]
}
```

Обратите внимание, что каждая строка содержит метрику уверенности — это удобно для фильтрации записей с низкой уверенностью, если вы планируете **извлекать текст из счета** автоматически.

---

## Шаг 6 – Сохранить данные OCR в CSV (по одной строке текста + уверенность)

CSV — идеальный формат для таблиц или быстрой импорта данных. Aspose предлагает однострочник для выгрузки всего в CSV‑файл.

```python
# Step 6: Save the OCR result as a CSV file (each line → text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
ocr_result.save_as_csv(csv_path)
```

Сгенерированный CSV будет выглядеть так:

```
"Invoice #12345",98.7
"Date: 2025-12-01",96.4
"Total Amount: $1,250.00",99.1
```

Теперь его можно открыть в Excel, Google Sheets или загрузить в базу данных.

---

## Бонус – Обработка текста с низкой уверенностью и многостраничных PDF

### Фильтрация по уверенности

Если нужны только строки с высокой уверенностью, отфильтруйте JSON перед записью:

```python
high_confidence = [
    region for page in ocr_data["pages"]
    for region in page["regions"]
    if region["confidence"] >= 95
]
print(json.dumps(high_confidence, indent=2))
```

### Многостраничные документы

Aspose.OCR автоматически создаёт новую запись `page` для каждой страницы в многостраничном PNG или PDF. Пройдитесь по `ocr_data["pages"]`, чтобы обработать их все — дополнительный код не требуется.

---

## Полный рабочий пример

Ниже представлен **полный скрипт**, который можно скопировать, вставить и сразу запустить. Замените `YOUR_DIRECTORY` на папку, где хранится ваш PNG‑файл.

```python
import asposeocr as ocr
import json

# 1️⃣ Initialize OCR engine
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH

# 2️⃣ Load the PNG image
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)

# 3️⃣ Perform OCR
result = engine.process(image)

# 4️⃣ Convert to JSON and pretty‑print
json_str = result.to_json()
data = json.loads(json_str)
print("=== OCR JSON Output ===")
print(json.dumps(data, indent=2))

# 5️⃣ Save as CSV (text + confidence)
csv_path = "YOUR_DIRECTORY/invoice_output.csv"
result.save_as_csv(csv_path)
print(f"\n✅ CSV saved to {csv_path}")

# 6️⃣ (Optional) Filter high‑confidence lines
high_conf = [
    r for page in data["pages"]
    for r in page["regions"]
    if r["confidence"] >= 95
]
print("\n=== High‑Confidence Regions ===")
print(json.dumps(high_conf, indent=2))
```

Запустите скрипт командой `python run_ocr.py`, и вы увидите дамп JSON в консоли, CSV‑файл на диске и отфильтрованный список записей с высокой уверенностью.

---

## Часто задаваемые вопросы

**Q: Можно ли использовать это для извлечения текста из отсканированного чека вместо счета?**  
A: Конечно. Тот же процесс работает — просто укажите `image_path` на ваш PNG‑чек. Если чек на другом языке, поменяйте `engine.language` соответственно.

**Q: Что делать, если мой PNG содержит повернутый текст?**  
A: Aspose.OCR автоматически определяет ориентацию, но в упорных случаях вы можете вручную повернуть изображение с помощью Pillow перед передачей его движку.

**Q: Нужна ли платная лицензия для Aspose.OCR?**  
A: Библиотека предлагает бесплатный режим оценки с водяным знаком на выводе. Для продакшн‑использования потребуется лицензия, которую можно получить на сайте Aspose.

---

## Заключение

Мы рассмотрели всё, что нужно для **запуска OCR на PNG**‑файлах с помощью Python: установка SDK, загрузка изображения, извлечение структурированного текста и сохранение результата в JSON или CSV. Независимо от того, хотите ли вы **извлечь текст из изображения** для простого скрипта или **извлечь текст из счета** для автоматизированного бухгалтерского конвейера, приведённые шаги дают надёжную, готовую к продакшну основу.

Дальше вы можете:

- Интегрировать CSV‑вывод с базой данных для массового хранения счетов.  
- Добавить пост‑обработку с помощью регулярных выражений для извлечения дат, сумм или ИНН.  
- Использовать функцию `ocr_engine.recognize_barcode`, если в ваших счетах есть QR‑коды.

Попробуйте, отрегулируйте пороги уверенности и наблюдайте, как ваш процесс обработки документов становится лёгким. Есть вопросы или интересный кейс? Оставляйте комментарий ниже — приятного OCR!

![run OCR on PNG example](run-ocr-on-png.png "run OCR on PNG – визуальный пример результата OCR")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}