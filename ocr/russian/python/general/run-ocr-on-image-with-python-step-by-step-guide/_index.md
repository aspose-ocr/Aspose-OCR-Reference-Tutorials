---
category: general
date: 2026-08-12
description: Запустите OCR на изображении с помощью Python и Aspose AI, чтобы извлечь
  текст из изображения и улучшить точность OCR с помощью постобработки, проверяющей
  орфографию.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract text from image
- OCR text correction
- improve OCR accuracy
- load image for OCR
language: ru
lastmod: 2026-08-12
og_description: Запустите OCR на изображении в Python и мгновенно извлеките текст,
  повышая точность распознавания с помощью постобработки Aspose AI.
og_image_alt: Diagram showing the run OCR on image workflow in Python
og_title: Запустите OCR на изображении с помощью Python – полный учебник
schemas:
- author: Aspose
  dateModified: '2026-08-12'
  description: Run OCR on image using Python and Aspose AI to extract text from image
    and improve OCR accuracy with a spell‑checking post‑processor.
  headline: Run OCR on image with Python – step‑by‑step guide
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Запустите OCR на изображении с помощью Python — пошаговое руководство
url: /ru/python/general/run-ocr-on-image-with-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении с помощью Python – пошаговое руководство

Если вам нужно **выполнить OCR на изображении** в Python, это руководство проведёт вас через весь процесс. Вы узнаете, как **извлекать текст из изображения**, применять **коррекцию текста OCR** и **повышать точность OCR** всего несколькими строками кода.

Обработка отсканированных документов, чеков или скриншотов часто приводит к шумному тексту. Подключив пост‑процессор проверки орфографии, вы можете превратить сырые результаты OCR в чистый, индексируемый контент без перехода к отдельному инструменту. Этот учебник охватывает всё, что вам нужно — от загрузки изображения до отображения скорректированного результата.

## Требования

Перед началом убедитесь, что у вас есть:

* Установлен Python 3.9 или новее.  
* Доступ к пакетам Aspose.OCR и Aspose.AI для Python (или их эквивалентным open‑source обёрткам).  
* Пример изображения (например, `sample.png`), размещённый в известном каталоге.  
* Базовое знакомство с функциями Python и объектно‑ориентированным кодом.

Вы можете установить необходимые библиотеки с помощью pip:

```bash
pip install aspose-ocr aspose-ai
```

> **Совет:** Используйте виртуальное окружение (`python -m venv .venv`), чтобы изолировать зависимости.

## Шаг 1: Запуск OCR на изображении – создание экземпляра движка

Первый шаг — создать объект `OcrEngine`. Этот объект инкапсулирует конфигурацию OCR‑движка и предоставляет методы для работы с изображениями и распознавания.

```python
from aspose.ocr import OcrEngine

# Initialize the OCR engine with default settings
ocr_engine = OcrEngine()
```

Создание движка один раз и повторное его использование для нескольких изображений уменьшает накладные расходы на запуск и обеспечивает согласованные настройки в течение всей сессии.

## Шаг 2: Загрузка изображения для OCR

Прежде чем может начаться распознавание, движок должен знать, какое изображение анализировать. Метод `load_image` принимает путь к файлу или бинарный поток.

```python
# Provide the full path to your image file
image_path = "YOUR_DIRECTORY/sample.png"
ocr_engine.load_image(image_path)
```

> **Почему это важно:** Правильная загрузка изображения — фундамент для точного OCR. Использование изображения высокого разрешения (300 dpi и выше) обычно **повышает точность OCR**, поскольку движок может более чётко различать символы.

## Шаг 3: Извлечение текста из изображения – базовое распознавание

После загрузки изображения вы можете вызвать `recognize()`, чтобы получить объект результата. Результат содержит сырой текст, оценки уверенности и, при необходимости, ограничивающие рамки для каждого слова.

```python
# Run the OCR process
plain_result = ocr_engine.recognize()   # returns a Result object

# The raw OCR output is accessible via the .text attribute
print("Raw OCR output:")
print(plain_result.text)
```

На этом этапе вы успешно **выполнили OCR на изображении** и извлекли сырые символы. Однако текст может содержать опечатки, особенно в случае низкокачественных сканов.

## Шаг 4: Коррекция текста OCR – подключение пост‑процессора проверки орфографии

Aspose AI предоставляет гибкий конвейер пост‑обработки. Подключив пользовательский проверщик орфографии, вы можете исправлять типичные ошибки OCR (например, «l» vs. «1», «O» vs. «0»).

```python
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker   # your own implementation

# Initialize the AI engine and set the post‑processor
ai_engine = AsposeAI()
ai_engine.set_post_processor(MySpellChecker())

# Run the post‑processor on the plain OCR result
corrected_result = ai_engine.run_postprocessor(plain_result)
```

**Как работает проверщик орфографии:** `MySpellChecker` должен реализовать метод `process(text: str) -> str`. Внутри вы можете использовать библиотеки такие как `pyspellchecker` или `symspellpy` для замены маловероятных последовательностей слов на варианты, подтверждённые словарём.

```python
# Example implementation (very simple)
from spellchecker import SpellChecker

class MySpellChecker:
    def __init__(self):
        self.spell = SpellChecker()

    def process(self, text: str) -> str:
        corrected = []
        for word in text.split():
            corrected.append(self.spell.correction(word))
        return " ".join(corrected)
```

## Шаг 5: Отображение оригинального и скорректированного текста OCR

Наконец, сравните сырые и исправленные результаты. Это поможет убедиться, что **коррекция текста OCR** действительно **повысила точность OCR** для вашего сценария.

```python
print("\nOriginal :", plain_result.text)
print("Corrected:", corrected_result.text)
```

### Ожидаемый вывод

```
Original : Th1s is a s4mpl3 rec3pt with som3 err0rs.
Corrected: This is a simple receipt with some errors.
```

Скорректированная строка показывает, что проверщик орфографии заменил типичные ошибки OCR (`Th1s` → `This`, `s4mpl3` → `simple`, `rec3pt` → `receipt`, `som3` → `some`, `err0rs` → `errors`).

## Шаг 6: Улучшение точности OCR – чек‑лист лучших практик

Даже при пост‑обработке вы можете повысить базовое качество OCR‑движка:

| Пункт чек‑листа | Почему это помогает |
|-----------------|----------------------|
| **Использовать изображения высокого разрешения (≥300 dpi)** | Большее количество пикселей уменьшает неоднозначность символов. |
| **Преобразовать цветные изображения в градации серого** | Убирает цветовой шум, который может сбивать движок с толку. |
| **Применять выравнивание изображения** | Выпрямляет наклонённый текст, предотвращая ошибки разрыва строк. |
| **Явно задавать язык/локаль** | Помогает распознавателю выбрать правильный набор символов. |
| **Включить языковую модель** (если библиотека её поддерживает) | Предоставляет предсказания с учётом контекста, дополнительно **повышая точность OCR**. |

Эти шаги предобработки можно реализовать с помощью Pillow или OpenCV перед передачей изображения в `ocr_engine`.

```python
from PIL import Image, ImageOps
import cv2
import numpy as np

def preprocess_image(path: str) -> str:
    # Load with Pillow, convert to grayscale, and increase contrast
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)

    # Save a temporary preprocessed file
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

# Use the preprocessor
preprocessed_path = preprocess_image(image_path)
ocr_engine.load_image(preprocessed_path)
```

## Полный исполняемый скрипт

Объединив всё вместе, следующий скрипт готов к копированию в файл `run_ocr.py` и запуску.

```python
# run_ocr.py
from aspose.ocr import OcrEngine
from aspose.ai import AsposeAI
from my_spellchecker import MySpellChecker
from PIL import Image, ImageOps

def preprocess_image(path: str) -> str:
    img = Image.open(path).convert("L")
    img = ImageOps.autocontrast(img, cutoff=2)
    temp_path = "temp_preprocessed.png"
    img.save(temp_path)
    return temp_path

def main():
    # 1️⃣ Initialize OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load and preprocess the image
    raw_path = "YOUR_DIRECTORY/sample.png"
    processed_path = preprocess_image(raw_path)
    ocr_engine.load_image(processed_path)

    # 3️⃣ Perform basic OCR
    plain_result = ocr_engine.recognize()

    # 4️⃣ Run OCR text correction
    ai_engine = AsposeAI()
    ai_engine.set_post_processor(MySpellChecker())
    corrected_result = ai_engine.run_postprocessor(plain_result)

    # 5️⃣ Show both results
    print("\nOriginal :", plain_result.text)
    print("Corrected:", corrected_result.text)

if __name__ == "__main__":
    main()
```

Запуск скрипта выводит оригинальный и исправленный текст, подтверждая, что вы успешно **выполнили OCR на изображении**, **извлекли текст из изображения** и **повысили точность OCR** через **коррекцию текста OCR**.

## Заключение

Теперь вы знаете, как **выполнять OCR на изображении** в Python, извлекать сырой текст и применять пост‑процессор проверки орфографии для получения более чистых результатов. Следуя чек‑листу по **улучшению точности OCR**, вы сможете адаптировать этот рабочий процесс к чекам, счетам, удостоверениям личности или любому отсканированному документу.

### Что дальше?

* Изучите **языко‑специфичные словари** для многоязычного OCR.  
* Интегрируйте конвейер с базой данных или поисковым индексом (например, Elasticsearch), чтобы сделать извлечённый текст индексируемым.  
* Замените простой проверщик орфографии на нейронную языковую модель (например, коррекцию на основе GPT) для ещё более высокой точности.

Экспериментируйте с различными методами предобработки изображений, разными пост‑процессорами или альтернативными OCR‑движками. Основная последовательность — **выполнить OCR на изображении → извлечь текст из изображения → коррекция текста OCR → улучшить точность OCR** — остаётся неизменной, предоставляя надёжную основу для любого проекта по оцифровке документов.

## Что следует изучить дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, помогающими вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Convert Image to Text: Extract Text from Image Using Aspose OCR (Python)](/ocr/english/python/general/convert-image-to-text-extract-text-from-image-using-aspose-o/)
- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}