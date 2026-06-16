---
category: general
date: 2026-03-26
description: Узнайте, как вращать изображение и выполнять OCR в Python. Это руководство
  также показывает, как предварительно обрабатывать изображение для OCR и эффективно
  извлекать текст из изображения.
draft: false
keywords:
- how to rotate image
- how to perform ocr
- preprocess image for ocr
- recognize text from image
- how to extract text from image
language: ru
og_description: Как правильно повернуть изображение и затем распознать текст на нём
  с помощью Aspose OCR. Следуйте этому пошаговому руководству, чтобы предварительно
  обработать изображение для OCR и извлечь текст из изображения.
og_title: Как повернуть изображение и выполнить OCR – Полное руководство по Python
tags:
- Aspose
- Python
- Image Processing
- OCR
title: Как повернуть изображение и выполнить OCR с помощью Aspose в Python
url: /ru/python-java/general/how-to-rotate-image-and-perform-ocr-with-aspose-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как повернуть изображение и выполнить OCR с помощью Aspose на Python

Когда‑нибудь задумывались **как повернуть изображение**, чтобы OCR‑движок действительно смог прочитать текст? Может быть, вы отсканировали форму, которая получилась боковой, или снимок с камеры повернулся на 90° по часовой стрелке. В таком случае текст выглядит нормально для человеческого глаза, но OCR‑движок видит лишь беспорядок. Хорошая новость? Исправить ориентацию, обрезать нужный регион и извлечь текст можно легко, используя несколько строк кода на Python и библиотеки Aspose.

В этом руководстве мы пройдем весь процесс: от загрузки повернутого TIFF, исправления его ориентации, **предобработки изображения для OCR**, до **распознавания текста с изображения**. К концу вы узнаете **как выполнять OCR** на любом изображении и сможете **извлекать текст из изображений** с уверенностью.

## Что вам понадобится

- Python 3.8+ (код работает с любой современной версией)
- Пакеты `asposeocrjava` и `asposeimaging`, установленные через `pip`
- Пример изображения, требующего поворота (например, `rotated_form.tif`)
- Немного любопытства к обработке изображений

Никаких тяжёлых фреймворков не требуется — только два пакета Aspose и немного логики на Python.

---

## Шаг 1: Установите пакеты Aspose (Как выполнить OCR)

Прежде чем мы сможем **повернуть изображение** или **распознать текст с изображения**, нам нужны библиотеки, которые действительно делают тяжёлую работу.

```bash
pip install asposeocrjava asposeimaging
```

> **Pro tip:** Если вы работаете за корпоративным прокси, добавьте `--proxy http://proxy:port` к команде. Пакеты являются чистыми Python‑обёртками вокруг ядра Aspose .NET/Java, поэтому установка обычно мгновенна.

---

## Шаг 2: Загрузите исходный файл и поверните его – основной шаг «Как повернуть изображение»

```python
from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

# Load the original, incorrectly oriented image
source_image = Image.load("YOUR_DIRECTORY/rotated_form.tif")

# Rotate 90° clockwise – this fixes the orientation for OCR
rotated_image = source_image.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)
```

> **Почему поворачивать?** Большинство OCR‑движков предполагают, что текст читается слева направо и сверху вниз. Если bitmap повернут боком, движок вернёт бессмыслицу или ничего. Поворот выравнивает пиксельную сетку с ожидаемым порядком чтения, существенно повышая точность.

> **Особый случай:** Если вы не уверены, нужен ли поворот на 90°, 180° или 270°, можно сравнить `source_image.width` и `source_image.height` или использовать теги ориентации `exif`. Метод Aspose `rotate_flip` также поддерживает `ROTATE_180` и `ROTATE_270_CLOCKWISE`.

> **Предпросмотр изображения (по желанию):**  
> ![пример того, как повернуть изображение](/assets/rotate-demo.png "Как повернуть изображение – до и после поворота")

---

## Шаг 3: Обрезка области интереса – предобработка изображения для OCR

Часто нужен лишь небольшой фрагмент страницы — например, поле подписи или блок цифр. Обрезка удаляет шум и ускоряет **как выполнить OCR**.

```python
# Define the rectangle that encloses the text you care about
# (x=100, y=200, width=800, height=300) – adjust to your form
roi = Rectangle(100, 200, 800, 300)

# Crop the rotated image to that rectangle
roi_image = rotated_image.crop(roi)
```

> **Почему обрезать?** Уменьшение размера изображения ограничивает пространство поиска OCR‑движка, что снижает количество ложных срабатываний и сокращает время обработки. Это также помогает, если исходный файл содержит водяные знаки или другую графику, которая может запутать движок.

> **Подсказка:** Если у вас несколько полей, повторите шаг обрезки с разными прямоугольниками и запустите OCR для каждого фрагмента отдельно.

---

## Шаг 4: Инициализируйте OCR‑движок – ядро «Как выполнить OCR»

```python
# Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

> **Что происходит в фоне:** Aspose OCR использует комбинацию Tesseract и собственных методов анализа изображений. Создание экземпляра движка один раз и повторное его использование для нескольких изображений эффективнее, чем создание нового объекта каждый раз.

---

## Шаг 5: Передайте обрезанное изображение и распознайте текст – как извлечь текст из изображения

```python
# Set the cropped image as the input for OCR
ocr_engine.set_image(roi_image)

# Run the recognition process
result = ocr_engine.recognize()

# Extract the plain text
extracted_text = result.get_text()
print(extracted_text)
```

### Ожидаемый вывод

Если ROI содержит фразу «Invoice #12345 – Paid», вы увидите примерно следующее:

```
Invoice #12345 – Paid
```

Если OCR‑движок затрудняется, могут появиться лишние пробелы или неверно распознанные символы (например, «Invo1ce #I2345 – Pa1d»). Здесь в дело вступают приёмы **предобработки изображения для OCR** — корректировка контрастности или бинаризация. Aspose предлагает дополнительные фильтры, которые можно добавить перед шагом 5, но базовый поток выше работает для большинства чистых сканов.

---

## Шаг 6: Необязательно – тонкая настройка параметров OCR (Продвинутое «Как выполнить OCR»)

Если нужна более высокая точность для конкретного языка или нужно игнорировать определённые символы, можно подправить движок:

```python
# Example: Restrict recognition to English alphanumerics only
ocr_engine.get_recognition_settings().set_recognition_language("en")
ocr_engine.get_recognition_settings().set_characters_blacklist("!@#$%^&*()")
```

> **Когда использовать:** Применяйте, если документ содержит множество декоративных символов, которые вам не нужны. Чёрный список уменьшает количество ложных срабатываний.

---

## Полный скрипт от начала до конца

Объединив всё вместе, получаем готовый к запуску скрипт, который **как повернуть изображение**, **предобработать изображение для OCR** и, наконец, **распознать текст с изображения**:

```python
# -*- coding: utf-8 -*-
"""
Complete example: rotate, crop, and OCR an image with Aspose.
Author: Your Name
Date: 2026-03-26
"""

from asposeocrjava import OcrEngine, Rectangle
from asposeimaging import Image, RotateFlipType

def ocr_rotated_image(
    input_path: str,
    output_path: str = None,
    crop_rect: Rectangle = Rectangle(100, 200, 800, 300)
) -> str:
    """
    Loads an image, rotates it 90° clockwise, crops the region of interest,
    runs OCR, and returns the extracted text.

    Parameters
    ----------
    input_path : str
        Path to the original (possibly rotated) image file.
    output_path : str, optional
        If provided, saves the processed (rotated + cropped) image for inspection.
    crop_rect : Rectangle, optional
        Rectangle defining the ROI. Adjust to match your document layout.

    Returns
    -------
    str
        The plain text extracted from the ROI.
    """
    # Load and rotate
    src = Image.load(input_path)
    rotated = src.rotate_flip(RotateFlipType.ROTATE_90_CLOCKWISE)

    # Crop to region of interest
    roi = rotated.crop(crop_rect)

    # Optionally save the processed image for debugging
    if output_path:
        roi.save(output_path)

    # OCR
    engine = OcrEngine()
    engine.set_image(roi)
    result = engine.recognize()
    return result.get_text()

if __name__ == "__main__":
    text = ocr_rotated_image(
        "YOUR_DIRECTORY/rotated_form.tif",
        output_path="processed_roi.png"
    )
    print("=== Extracted Text ===")
    print(text)
```

Запуск этого скрипта выводит распознанный текст в консоль и сохраняет визуализацию обработанного ROI как `processed_roi.png`. Откройте этот PNG, чтобы убедиться, что поворот и обрезка выполнены корректно.

---

## Часто задаваемые вопросы и подводные камни

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если изображение уже правильно ориентировано?** | Шаг поворота идемпотентен — вращать уже правильно ориентированное изображение на 90° явно испортит его, поэтому перед вызовом `rotate_flip` следует проверять `source_image.width` и `height` или использовать данные EXIF ориентации. |
| **Мой OCR‑вывод содержит лишние переносы строк.** | Используйте `result.get_text().replace("\n", " ").strip()` для очистки или включите `ocr_engine.get_recognition_settings().set_remove_line_breaks(True)`. |
| **Можно ли обрабатывать PDF‑файлы напрямую?** | Да — Aspose Imaging может загружать страницы PDF как изображения (`Image.load("file.pdf")`), после чего применяются те же шаги поворота и OCR. |
| **Есть ли способ пакетно обрабатывать множество файлов?** | Оберните `ocr_rotated_image` в цикл по директории или используйте `concurrent.futures` в Python для параллелизации. |
| **Как работать с языками, отличными от английского?** | Установите язык распознавания через `ocr_engine.get_recognition_settings().set_recognition_language("fr")` для французского и т.д. |

---

## Заключение

Мы рассмотрели, **как правильно повернуть изображение**, **как предобработать изображение для OCR** путём обрезки, и, наконец, **как выполнить OCR**, чтобы **распознать текст с изображения** и **извлечь текст из изображений** с помощью библиотек Aspose для Python. Полный скрипт демонстрирует практический, готовый к продакшну процесс, который можно внедрить в любую автоматизационную цепочку.

Если хотите идти дальше, попробуйте поэкспериментировать с:

- **Улучшением изображения** (контраст, бинаризация) перед OCR
- **Извлечением нескольких ROI** для форм с несколькими полями
- **Пакетной обработкой** целых папок отсканированных документов
- **Интеграцией** с downstream‑системами (например, загрузкой извлечённых данных в базу)

Не стесняйтесь адаптировать код под свои задачи, и приятного кодинга! 🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}