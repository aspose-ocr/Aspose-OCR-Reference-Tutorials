---
category: general
date: 2026-03-28
description: Выполните OCR на изображении и получите чистый текст с координатами ограничивающих
  рамок. Узнайте, как извлекать OCR, очищать его и отображать результаты пошагово.
draft: false
keywords:
- perform OCR on image
- how to extract OCR
- how to clean OCR
- display bounding box coordinates
- OCR post‑processing
- OCR bounding boxes
language: ru
og_description: Выполните OCR на изображении, очистите вывод и отобразите координаты
  ограничивающих рамок в кратком руководстве.
og_title: Выполнить OCR на изображении — чистые результаты и ограничивающие рамки
tags:
- OCR
- Computer Vision
- Python
title: Выполнить OCR на изображении — очистить результаты и отобразить координаты
  ограничивающих рамок
url: /ru/python/general/perform-ocr-on-image-clean-results-and-show-bounding-box-coo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении – Очистить результаты и показать координаты ограничивающих рамок

Когда‑то вам нужно **выполнить OCR на изображении**, но вы получаете беспорядочный текст и не знаете, где каждое слово расположено на картинке? Вы не одиноки. Во многих проектах — оцифровка счетов, сканирование чеков или простое извлечение текста — получение «сырого» вывода OCR — лишь первая преграда. Хорошая новость: вы можете очистить этот вывод и мгновенно увидеть координаты ограничивающих рамок каждого региона без написания кучи шаблонного кода.

В этом руководстве мы пройдемся по **извлечению OCR**, запустим **пост‑обработку очистки OCR**, а затем **отобразим координаты ограничивающих рамок** для каждого очищенного региона. К концу вы получите один готовый к запуску скрипт, который превратит размытое фото в аккуратный, структурированный текст, готовый к дальнейшей обработке.

## Что понадобится

- Python 3.9+ (синтаксис ниже работает на 3.8 и новее)
- OCR‑движок, поддерживающий `recognize(..., return_structured=True)` — например, вымышленная библиотека `engine`, используемая в примере. Замените её на Tesseract, EasyOCR или любой SDK, возвращающий данные о регионах.
- Базовое знакомство с функциями и циклами в Python
- Файл изображения, который хотите просканировать (PNG, JPG и т.д.)

> **Pro tip:** Если вы используете Tesseract, функция `pytesseract.image_to_data` уже возвращает ограничивающие рамки. Вы можете обернуть её результат в небольшой адаптер, имитирующий API `engine.recognize`, показанный ниже.

---

![perform OCR on image example](image-placeholder.png "perform OCR on image example")

*Alt text: диаграмма, показывающая, как выполнить OCR на изображении и визуализировать координаты ограничивающих рамок*

## Шаг 1 – Выполнить OCR на изображении и получить структурированные регионы

Первое, что нужно сделать, — попросить OCR‑движок вернуть не просто простой текст, а структурированный список текстовых регионов. Этот список содержит исходную строку и прямоугольник, который её охватывает.

```python
import engine   # replace with your actual OCR library
from pathlib import Path

# Load the image you want to process
image_path = Path("sample_invoice.jpg")
image = engine.load_image(image_path)

# Step 1: Perform OCR and request a structured list of text regions
raw_result = engine.recognize(image, return_structured=True)
```

**Почему это важно:**  
Когда вы запрашиваете только простой текст, вы теряете пространственный контекст. Структурированные данные позволяют позже **отобразить координаты ограничивающих рамок**, выравнивать текст с таблицами или передавать точные позиции в downstream‑модель.

## Шаг 2 – Как очистить вывод OCR с помощью пост‑процессора

OCR‑движки хорошо распознают символы, но часто оставляют лишние пробелы, артефакты разрывов строк или ошибочно распознанные символы. Пост‑процессор нормализует текст, исправляет типичные ошибки OCR и обрезает пробелы.

```python
# Step 2: Clean the plain‑text of each region using the post‑processor
processed_result = engine.run_postprocessor(raw_result)
```

Если вы создаёте собственный очиститель, учитывайте следующее:

- Удаление не‑ASCII символов (`re.sub(r'[^\x00-\x7F]+',' ', text)`)
- Сведение нескольких пробелов к одному
- Применение проверяющего орфографии, например `pyspellchecker`, для исправления очевидных опечаток

**Почему это важно:**  
Аккуратная строка делает поиск, индексацию и последующие NLP‑конвейеры гораздо надёжнее. Иными словами, **как очистить OCR** часто является разницей между пригодным набором данных и головной болью.

## Шаг 3 – Отобразить координаты ограничивающих рамок для каждого очищенного региона

Теперь, когда текст уже чистый, мы проходим по каждому региону, выводя его прямоугольник и очищенную строку. Это та часть, где мы наконец **отображаем координаты ограничивающих рамок**.

```python
# Step 3 – Iterate over the cleaned regions and display their bounding box and text
for text_region in processed_result.regions:
    # Each region has a .bounding_box attribute (x, y, width, height)
    bbox = text_region.bounding_box
    print(f"[{bbox}] {text_region.text}")
```

**Пример вывода**

```
[(34, 120, 210, 30)] Invoice #12345
[(34, 160, 420, 28)] Date: 2026‑03‑01
[(34, 200, 380, 28)] Total Amount: $1,254.00
```

Теперь вы можете передать эти координаты в библиотеку рисования (например, OpenCV), чтобы наложить рамки на оригинальное изображение, либо сохранить их в базе данных для последующих запросов.

## Полный готовый к запуску скрипт

Ниже представлена полная программа, связывающая все три шага. Замените вызовы заглушки `engine` на ваш реальный OCR‑SDK.

```python
#!/usr/bin/env python3
"""
Perform OCR on image → clean results → display bounding box coordinates.
Author: Your Name
Date: 2026‑03‑28
"""

import engine               # <-- replace with your OCR library
from pathlib import Path
import sys

def main(image_path: str):
    # Load image
    image = engine.load_image(Path(image_path))

    # 1️⃣ Perform OCR and ask for structured output
    raw_result = engine.recognize(image, return_structured=True)

    # 2️⃣ Clean the raw text using the built‑in post‑processor
    processed_result = engine.run_postprocessor(raw_result)

    # 3️⃣ Show each region's bounding box and cleaned text
    print("\n=== Cleaned OCR Regions ===")
    for region in processed_result.regions:
        bbox = region.bounding_box  # (x, y, w, h)
        print(f"[{bbox}] {region.text}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python perform_ocr.py <image_file>")
        sys.exit(1)
    main(sys.argv[1])
```

### Как запустить

```bash
python perform_ocr.py sample_invoice.jpg
```

Вы должны увидеть список ограничивающих рамок, сопоставленных с очищенным текстом, точно как в примере вывода выше.

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если OCR‑движок не поддерживает `return_structured`?** | Напишите лёгкую оболочку, которая преобразует «сырой» вывод движка (обычно список слов с координатами) в объекты с атрибутами `text` и `bounding_box`. |
| **Можно ли получить оценки уверенности?** | Многие SDK предоставляют метрику confidence для каждого региона. Добавьте её к оператору печати: `print(f"[{bbox}] {region.text} (conf: {region.confidence:.2f})")`. |
| **Как обрабатывать повернутый текст?** | Предобработайте изображение с помощью `cv2.minAreaRect` из OpenCV, чтобы исправить наклон перед вызовом `recognize`. |
| **А если нужен вывод в JSON?** | Сериализуйте `processed_result.regions` через `json.dumps([r.__dict__ for r in processed_result.regions], indent=2)`. |
| **Есть ли способ визуализировать рамки?** | Используйте OpenCV: `cv2.rectangle(img, (x, y), (x+w, y+h), (0,255,0), 2)` внутри цикла, затем `cv2.imwrite("annotated.jpg", img)`. |

## Подведение итогов

Вы только что узнали, **как выполнить OCR на изображении**, очистить «сырой» вывод и **отобразить координаты ограничивающих рамок** для каждого региона. Трёхшаговый поток — распознавание → пост‑обработка → итерация — это переиспользуемый шаблон, который можно внедрить в любой Python‑проект, требующий надёжного извлечения текста.

### Что дальше?

- **Исследуйте разные OCR‑бэкенды** (Tesseract, EasyOCR, Google Vision) и сравните точность.
- **Интегрируйте с базой данных** для хранения данных регионов в поисковых архивах.
- **Добавьте определение языка**, чтобы направлять каждый регион в соответствующий проверяющий орфографии.
- **Наложите рамки на оригинальное изображение** для визуальной проверки (см. фрагмент кода OpenCV выше).

Если столкнётесь с нюансами, помните, что главный выигрыш приходит от надёжного шага пост‑обработки; чистая строка гораздо проще в работе, чем «сырой» набор символов.

Счастливого кодинга, и пусть ваши OCR‑конвейеры всегда остаются аккуратными!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}