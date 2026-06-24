---
category: general
date: 2026-06-22
description: Получайте координаты ограничивающего прямоугольника из изображений с
  помощью Python. Узнайте, как извлекать текст из изображения на Python с помощью
  Aspose OCR и парсинга JSON за считанные минуты.
draft: false
keywords:
- get bounding box coordinates
- extract text from image python
- Aspose OCR Python
- OCR layout data JSON
- Python image processing OCR
language: ru
og_description: Получите координаты ограничивающих рамок из изображений с помощью
  Python. Это руководство показывает, как извлечь текст из изображения с помощью Aspose
  OCR в Python и разобрать данные о макете.
og_title: Получите координаты ограничивающего прямоугольника из OCR в Python – Полный
  учебник
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  headline: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  type: TechArticle
- description: Get bounding box coordinates from images using Python. Learn how to
    extract text from image python with Aspose OCR and JSON parsing in minutes.
  name: Get Bounding Box Coordinates from OCR in Python – Complete Guide
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed on your machine. - An active Aspose.OCR for Python
      license or a free trial (the library works without a license but adds a watermark).
      - `pip install aspose-ocr` (the package name on PyPI). - A sample image called
      `invoice.png` placed in a folder you can reference.'
  - name: 1. Convert Bounding Boxes to Simple Rectangles
    text: 'If your downstream tool expects `(x, y, width, height)` instead of eight
      points, add a helper:'
  - name: 2. Handle Multi‑Page PDFs
    text: 'Aspose OCR can accept PDF streams. Replace the image loading line with:'
  - name: 3. Visualize Bounding Boxes
    text: 'If you want to see the boxes drawn on the original image, use Pillow:'
  type: HowTo
- questions:
  - answer: For large documents, consider streaming the JSON or processing page‑by‑page
      to keep memory usage low.
    question: What if the JSON is huge?
  - answer: Low contrast or handwritten text often trips OCR engines. Pre‑process
      the image (increase contrast, binarize) before feeding it to Aspose.
    question: Why are some words missing?
  - answer: Yes—set `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`
      to receive a `"characters"` array with its own `boundingBox`.
    question: Can I get character‑level coordinates?
  - answer: Absolutely. (0, 0) is the top‑left corner of the image.
    question: Is the coordinate system zero‑based?
  type: FAQPage
tags:
- OCR
- Python
- JSON
- Image Processing
title: Получение координат ограничивающего прямоугольника из OCR в Python – Полное
  руководство
url: /ru/python-java/general/get-bounding-box-coordinates-from-ocr-in-python-complete-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Получение координат ограничивающего прямоугольника из OCR в Python – Полное руководство

Когда‑нибудь вам нужно было **получить координаты ограничивающего прямоугольника** для каждого слова в отсканированном счете, но вы не знали, с чего начать? Вы не одиноки. Во многих проектах автоматизации необходимо определить расположение текста на изображении, чтобы выделить, замазать или передать его в последующий анализ. Хорошая новость? С несколькими строками кода на Python и Aspose.OCR вы можете получить как текст, **так и** его точное положение за один проход.

В этом руководстве мы пройдем пошаговый пример, показывающий, как **извлечь текст из изображения в стиле Python**, а затем погрузиться в данные JSON‑разметки, чтобы получить эти ограничивающие прямоугольники. Без лишних слов, только работающий скрипт, объяснения, почему каждый шаг важен, и советы по избежанию распространенных ошибок.

---

## Что вы создадите

К концу этого руководства у вас будет готовый к запуску скрипт на Python, который:

1. Загружает изображение (например, PNG‑счет) в Aspose OCR.  
2. Настраивает движок для вывода информации о разметке в формате JSON.  
3. Разбирает JSON в словарь Python.  
4. Проходит по каждому распознанному слову, выводя его текст **и** координаты ограничивающего прямоугольника.  

Вы также увидите, как адаптировать код для многостраничных PDF, различных форматов изображений и пользовательских систем координат.

### Предварительные требования

- Установленный Python 3.8+ на вашем компьютере.  
- Действующая лицензия Aspose.OCR для Python или бесплатная пробная версия (библиотека работает без лицензии, но добавляет водяной знак).  
- `pip install aspose-ocr` (имя пакета в PyPI).  
- Пример изображения с именем `invoice.png`, размещённый в папке, к которой вы можете обратиться.  

Вот и всё — без тяжёлых фреймворков, без внешних сервисов. Приступим.

---

## Шаг 1: Установите и импортируйте необходимые библиотеки

Сначала убедитесь, что пакет Aspose OCR и встроенный модуль `json` доступны. Модуль `json` поставляется с Python, поэтому нужно установить только Aspose.

```bash
pip install aspose-ocr
```

Теперь импортируйте их в ваш скрипт:

```python
# Step 1: Import the OCR library and the JSON module
import aspose.ocr as ocr
import json
```

> **Почему это важно:** импорт `aspose.ocr` предоставляет доступ к высокопроизводительному OCR‑движку, а `json` позволяет преобразовать сырую строку разметки в нативный словарь Python для удобного обхода.

---

## Шаг 2: Создайте OCR‑движок и загрузите изображение

Движок — сердце процесса. Вы создаёте его экземпляр, а затем указываете изображение, которое нужно просканировать.

```python
# Step 2: Create an OCR engine instance and load the image to be processed
engine = ocr.OcrEngine()
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/invoice.png"))
```

> **Совет профессионала:** замените `"YOUR_DIRECTORY/invoice.png"` на абсолютный или относительный путь к вашему реальному файлу. Если файл не найден, Aspose выдаст `FileNotFoundError`, поэтому проверьте правильность написания.

---

## Шаг 3: Настройте движок для вывода данных разметки в формате JSON

Aspose OCR может возвращать простой текст, JSON только OCR или полный JSON разметки, включающий координаты слов, строк и даже отдельных символов. Для **получения координат ограничивающего прямоугольника** нам нужен JSON разметки.

```python
# Step 3: Configure the engine to output results in JSON format (includes layout data)
engine.get_settings().set_output_format(ocr.OutputFormat.JSON)
```

> **Почему JSON?** JSON независим от языка, читаем человеком и легко преобразуется в словари Python. JSON разметки содержит массив `"words"`, где каждая запись хранит текст и массив `boundingBox` из восьми чисел (четыре точки углов).

---

## Шаг 4: Выполните распознавание и получите сырую строку JSON

Теперь мы действительно запускаем OCR. Метод `recognize()` возвращает объект `OcrResult`, из которого мы можем извлечь строку JSON.

```python
# Step 4: Perform recognition and obtain the raw JSON string with words, lines, and bounding boxes
result = engine.recognize()
layout_json = result.get_json()
```

Если вывести `layout_json`, вы увидите что‑то вроде:

```json
{
  "words": [
    {
      "text": "Invoice",
      "boundingBox": [12, 34, 112, 34, 112, 58, 12, 58]
    },
    {
      "text": "#12345",
      "boundingBox": [130, 34, 210, 34, 210, 58, 130, 58]
    }
    // ... more words ...
  ]
}
```

> **Пограничный случай:** некоторые изображения могут давать пустой массив `"words"`, если OCR‑движок не может обнаружить текст. В таком случае проверьте качество изображения (контраст, разрешение) перед продолжением.

---

## Шаг 5: Разберите JSON в словарь Python

Работа с нативными структурами Python гораздо проще, чем манипуляции со строками. Используйте функцию `json.loads()` для преобразования строки.

```python
# Step 5: Parse the JSON string into a Python dictionary for easy access
layout_data = json.loads(layout_json)
```

Теперь `layout_data["words"]` — это список словарей, каждый из которых представляет слово и его ограничивающий прямоугольник.

---

## Шаг 6: Пройдитесь по словам и **получите координаты ограничивающего прямоугольника**

Вот ядро нашего руководства: цикл по каждому слову, извлечение текста и вывод координат. Именно здесь мы **получаем координаты ограничивающего прямоугольника**.

```python
# Step 6: Iterate through each recognized word and display its text and bounding box coordinates
for word in layout_data["words"]:
    text = word["text"]
    box = word["boundingBox"]  # Format: [x1, y1, x2, y2, x3, y3, x4, y4]
    print(f"'{text}' at {box}")
```

**Пример вывода** (ваши числа будут отличаться в зависимости от изображения):

```
'Invoice' at [12, 34, 112, 34, 112, 58, 12, 58]
'#12345' at [130, 34, 210, 34, 210, 58, 130, 58]
'Date' at [12, 70, 60, 70, 60, 94, 12, 94]
'01/01/2024' at [70, 70, 150, 70, 150, 94, 70, 94]
```

> **Почему формат из восьми точек?** Четыре угла (верхний‑левый, верхний‑правый, нижний‑правый, нижний‑левый) позволяют нарисовать полигон вокруг слова, даже если текст наклонён. Если нужен простой прямоугольник, можно вычислить `x_min = min(x1, x2, x3, x4)`, `y_min = min(y1, y2, y3, y4)`, `width = max(x…) - x_min`, и `height = max(y…) - y_min`.

---

## Дополнительные улучшения

### 1. Преобразовать ограничивающие прямоугольники в простые прямоугольники

Если ваш последующий инструмент ожидает `(x, y, width, height)` вместо восьми точек, добавьте вспомогательную функцию:

```python
def box_to_rect(box):
    xs = box[0::2]  # extract x coordinates
    ys = box[1::2]  # extract y coordinates
    x_min, x_max = min(xs), max(xs)
    y_min, y_max = min(ys), max(ys)
    return (x_min, y_min, x_max - x_min, y_max - y_min)

for word in layout_data["words"]:
    rect = box_to_rect(word["boundingBox"])
    print(f"'{word['text']}' rectangle {rect}")
```

### 2. Обрабатывать многостраничные PDF

Aspose OCR может принимать потоки PDF. Замените строку загрузки изображения на:

```python
engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/document.pdf"))
engine.get_settings().set_page_number(1)  # change for each page in a loop
```

Итерируйте `set_page_number` для каждой страницы, собирая координаты по страницам.

### 3. Визуализировать ограничивающие прямоугольники

Если хотите увидеть прямоугольники, нарисованные на оригинальном изображении, используйте Pillow:

```python
from PIL import Image, ImageDraw

img = Image.open("YOUR_DIRECTORY/invoice.png")
draw = ImageDraw.Draw(img)

for word in layout_data["words"]:
    box = word["boundingBox"]
    # Pillow expects a list of tuples [(x1,y1), (x2,y2), ...]
    polygon = [(box[i], box[i+1]) for i in range(0, len(box), 2)]
    draw.line(polygon + [polygon[0]], fill="red", width=2)

img.show()
```

Теперь вы увидите красные контуры вокруг каждого распознанного слова — идеально для отладки или наложения в пользовательском интерфейсе.

---

## Часто задаваемые вопросы и подводные камни

- **Что делать, если JSON огромный?** Для больших документов рассмотрите потоковую обработку JSON или обработку постранично, чтобы снизить использование памяти.  
- **Почему некоторые слова отсутствуют?** Низкий контраст или рукописный текст часто сбивают OCR‑движки. Предобработайте изображение (увеличьте контраст, бинаризуйте) перед передачей в Aspose.  
- **Можно ли получить координаты на уровне символов?** Да — установите `engine.get_settings().set_output_format(ocr.OutputFormat.JSON_CHAR)`, чтобы получить массив `"characters"` со своим `boundingBox`.  
- **Система координат начинается с нуля?** Да. (0, 0) — это верхний‑левый угол изображения.

---

## Полный скрипт — готов к копированию и запуску

Ниже приведён полный, готовый к запуску пример, объединяющий все шаги. Сохраните его как `extract_bboxes.py` и выполните `python extract_bboxes.py`.



## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, помогающими освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения с Aspose OCR — пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как использовать Aspose OCR для получения результата в формате JSON при распознавании изображений](/ocr/english/net/text-recognition/get-result-as-json/)
- [Как извлечь текст из изображения, подготовив прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}