---
category: general
date: 2026-06-25
description: Извлеките текст из изображения с помощью Python OCR. Узнайте, как загрузить
  изображение для OCR, выполнить OCR в Python и преобразовать чек в JSON за несколько
  простых шагов.
draft: false
keywords:
- extract text from image
- load image for OCR
- perform OCR in Python
- convert receipt to JSON
language: ru
og_description: Извлеките текст из изображения с помощью OCR в Python. Этот учебник
  пошагово покажет, как загрузить изображение для OCR, выполнить OCR в Python и преобразовать
  чек в JSON.
og_title: Извлечение текста из изображения в Python – Полное руководство по OCR
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  headline: Extract Text from Image in Python – Full OCR Guide
  type: TechArticle
- description: Extract text from image using Python OCR. Learn how to load image for
    OCR, perform OCR in Python, and convert receipt to JSON in a few simple steps.
  name: Extract Text from Image in Python – Full OCR Guide
  steps:
  - name: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
    text: '**Create an OCR engine instance** – the entry point for all recognition
      work.'
  - name: '**Load an image for OCR** – tell the engine which file to read.'
    text: '**Load an image for OCR** – tell the engine which file to read.'
  - name: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
    text: '**Choose the export format** – JSON or XML, we’ll pick JSON because it’s
      easier to consume.'
  - name: '**Run the recognition** – actually perform OCR in Python.'
    text: '**Run the recognition** – actually perform OCR in Python.'
  - name: '**Print or store the result** – convert receipt to JSON and see the output.'
    text: '**Print or store the result** – convert receipt to JSON and see the output.'
  - name: Sends the image through a pre‑trained convolutional network.
    text: Sends the image through a pre‑trained convolutional network.
  - name: Decodes the network output into readable characters.
    text: Decodes the network output into readable characters.
  - name: Packages everything into the selected format (JSON in our case).
    text: Packages everything into the selected format (JSON in our case).
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- JSON
title: Извлечение текста из изображения в Python — Полное руководство по OCR
url: /ru/python/general/extract-text-from-image-in-python-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображения в Python – Полное руководство по OCR

Когда‑нибудь вам нужно было **извлечь текст из изображения**, но вы не знали, с чего начать? В этом руководстве мы покажем, как **загрузить изображение для OCR**, **выполнить OCR в Python** и **преобразовать чек в JSON** — всё это с помощью всего лишь нескольких строк кода.

Если вы когда‑либо создавали приложение для сканирования чеков, трекер расходов или просто хотите автоматизировать ввод данных, вы поймёте, почему освоение этого процесса меняет правила игры. К концу вы получите рабочий скрипт, который читает фотографию чека и выдаёт чистый JSON‑payload, готовый для дальнейших сервисов.

## Что вы узнаете

Мы рассмотрим каждый шаг от установки библиотеки `aocr` до обработки необработанного результата. В частности, вы узнаете, как:

1. **Create an OCR engine instance** – точка входа для всей работы по распознаванию.  
2. **Load an image for OCR** – укажите движку, какой файл читать.  
3. **Choose the export format** – JSON или XML, мы выберем JSON, потому что его проще использовать.  
4. **Run the recognition** – фактически выполнить OCR в Python.  
5. **Print or store the result** – преобразовать чек в JSON и увидеть результат.

Предыдущий опыт работы с OCR не требуется; достаточно базовой установки Python и файла изображения (чек, листовка, что угодно).  

---

![Diagram showing the flow of extracting text from image using Python OCR](extract-text-from-image-python-ocr.png){alt="извлечение текста из изображения с помощью Python OCR"}

## Извлечение текста из изображения – пошаговый Python OCR

Ниже представлен полный готовый к запуску скрипт. Смело скопируйте его в файл с именем `receipt_ocr.py` и запустите `python receipt_ocr.py`.

```python
# receipt_ocr.py

# 1️⃣ Import the aocr package (make sure it's installed via `pip install aocr`)
import aocr

# 2️⃣ Create an OCR engine instance – this object orchestrates the whole process
engine = aocr.OcrEngine()

# 3️⃣ Load the image you want to process.
#    Replace the path with the location of your receipt or any image.
engine.load_image("YOUR_DIRECTORY/receipt.png")

# 4️⃣ Choose the output format. JSON is handy for APIs and downstream services.
engine.export_format = aocr.ExportFormat.JSON

# 5️⃣ Run the recognition and obtain the raw result.
json_result = engine.recognize()

# 6️⃣ Output the raw JSON string – you can also write it to a file if you prefer.
print(json_result)
```

### Почему это работает

- **Engine instance** – `aocr.OcrEngine()` инкапсулирует всю тяжёлую работу (загрузка модели, предобработка и т.д.).  
- **Loading the image** – `engine.load_image()` указывает библиотеке, какой именно битмап анализировать; вы можете передать JPEG, PNG или даже многостраничные PDF.  
- **Export format** – Установка `engine.export_format` в `aocr.ExportFormat.JSON` делает результат структурированной строкой, идеальной для API, ожидающих JSON.  
- **Recognition call** – `engine.recognize()` запускает вывод нейронной сети за кулисами; он возвращает JSON‑строку, содержащую обнаруженные текстовые блоки, оценки уверенности и информацию о разметке.  

---

## Загрузка изображения для OCR с aocr

Если вы задаётесь вопросом, требуется ли изображению специальная предобработка, короткий ответ — **нет** — `aocr` автоматически обрабатывает большинство типичных случаев (регулировка контраста, выравнивание). Тем не менее, вы можете повысить точность, сделав следующее:

- Убедитесь, что изображение имеет минимум 300 dpi.  
- Обрезайте лишние границы.  
- Преобразуйте в градации серого перед передачей (по желанию, `engine.load_image()` сделает это за вас).  

```python
# Optional preprocessing example using Pillow
from PIL import Image, ImageOps

original = Image.open("YOUR_DIRECTORY/receipt.png")
# Convert to grayscale and increase contrast
processed = ImageOps.autocontrast(original.convert("L"))
processed.save("processed_receipt.png")
engine.load_image("processed_receipt.png")
```

*Pro tip:* Если чек содержит много шума, вышеуказанный дополнительный шаг может заметно повысить точность **perform OCR in Python**.

---

## Выбор формата экспорта и преобразование чека в JSON

Вы можете спросить: «Почему бы просто не получить обычный текст?» Потому что JSON сохраняет иерархическую структуру (строки, слова, ограничивающие рамки). Это значительно упрощает сопоставление полей, таких как *общая сумма* или *дата*, позже.

```python
engine.export_format = aocr.ExportFormat.JSON   # Switch to XML with aocr.ExportFormat.XML if needed
```

Когда вы запустите скрипт, `json_result` будет выглядеть примерно так (усечено для краткости):

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "bbox": [12, 34, 210, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.96,
          "bbox": [15, 400, 190, 420]
        }
      ]
    }
  ]
}
```

Теперь у вас есть payload **convert receipt to JSON**, который можно сразу передать в базу данных, REST‑endpoint или модель машинного обучения.

---

## Запуск распознавания и получение результатов

Последний шаг — фактическое выполнение OCR — так же прост, как вызов `recognize()`. За кулисами библиотека:

1. Отправляет изображение через предварительно обученную сверточную сеть.  
2. Декодирует вывод сети в читаемые символы.  
3. Упаковывает всё в выбранный формат (JSON в нашем случае).  

```python
json_result = engine.recognize()
print(json_result)   # <-- This prints the JSON string to stdout
```

Если вам нужно сохранить вывод вместо печати, просто запишите его в файл:

```python
with open("receipt_output.json", "w", encoding="utf-8") as f:
    f.write(json_result)
```

*Edge case:* Некоторые чеки содержат не‑ASCII символы (например, “€”). Убедитесь, что открываете файл с кодировкой UTF‑8, как показано выше, чтобы избежать искажённого текста.

---

## Полный рабочий пример (все шаги в одном скрипте)

Объединив всё вместе, представляем финальный скрипт, который можно запустить от начала до конца:

```python
import aocr
from PIL import Image, ImageOps

# Create engine
engine = aocr.OcrEngine()

# Optional: preprocess image for better accuracy
raw = Image.open("YOUR_DIRECTORY/receipt.png")
processed = ImageOps.autocontrast(raw.convert("L"))
processed.save("processed_receipt.png")

# Load the (processed) image
engine.load_image("processed_receipt.png")

# Choose JSON output
engine.export_format = aocr.ExportFormat.JSON

# Run OCR
json_result = engine.recognize()

# Save result
with open("receipt_output.json", "w", encoding="utf-8") as out_file:
    out_file.write(json_result)

print("OCR complete! JSON saved to receipt_output.json")
```

Запустите его с помощью:

```bash
python receipt_ocr.py
```

Вы должны увидеть строку подтверждения и, в той же папке, файл `receipt_output.json`, содержащий структурированные данные.

---

## Заключение

Теперь вы знаете **как извлекать текст из изображения** с помощью Python, как **загружать изображение для OCR**, как **perform OCR in Python**, и как **convert receipt to JSON** для дальнейшего использования. Этот сквозной процесс лёгок, требует только пакета `aocr` и может быть внедрён в любой конвейер автоматизации.

Что дальше? Попробуйте переключить формат экспорта на XML, поэкспериментировать с различными методами предобработки изображений или создать небольшой Flask‑API, который принимает загруженный чек и мгновенно возвращает JSON‑payload. Возможности безграничны, как только вы освоите основы.

Есть вопросы или возникли проблемы? Оставьте комментарий ниже, и удачной разработки!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, опирающиеся на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в собственных проектах.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)
- [Как извлечь таблицу из изображения с помощью Aspose.OCR для .NET](/ocr/english/net/text-recognition/recognize-table/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}