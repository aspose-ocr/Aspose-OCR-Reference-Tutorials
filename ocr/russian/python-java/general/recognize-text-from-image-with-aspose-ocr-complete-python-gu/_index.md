---
category: general
date: 2026-06-28
description: Узнайте, как распознавать текст на изображении и выполнять OCR с помощью
  Aspose OCR для Python. Включает шаги по установке языка OCR и извлечению оценок
  уверенности.
draft: false
keywords:
- recognize text from image
- perform ocr on image
- how to set OCR language
language: ru
og_description: Распознавать текст на изображении с помощью Aspose OCR в Python. Это
  руководство показывает, как установить язык OCR, выполнить распознавание текста
  на изображении и прочитать уровни уверенности.
og_title: Распознавание текста с изображения – Полный учебник по OCR на Python
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  headline: recognize text from image with Aspose OCR – Complete Python Guide
  type: TechArticle
- description: Learn how to recognize text from image and perform OCR on image using
    Aspose OCR for Python. Includes steps to set OCR language and extract confidence
    scores.
  name: recognize text from image with Aspose OCR – Complete Python Guide
  steps:
  - name: What if my image contains multiple languages?
    text: 'Aspose OCR supports multi‑language detection, but you need to pass a **combined
      language flag**. For example, to handle both Latin and Cyrillic:'
  - name: How do I improve accuracy on low‑resolution images?
    text: '- **Pre‑process** the image: increase contrast, apply binarization, or
      upscale using a library like Pillow. - **Set the correct DPI** if you know it;
      Aspose respects the image metadata. - **Choose the right language**—the more
      specific you are, the better the model performs.'
  - name: Can I extract only certain regions of the image?
    text: Yes. Use the `recognizeRegion` method (not shown in the basic example) and
      pass a rectangle object defining the area of interest. This is handy when you
      only need a table or a specific block of text.
  type: HowTo
tags:
- OCR
- Python
- Aspose
title: Распознавание текста с изображения с помощью Aspose OCR — Полное руководство
  по Python
url: /ru/python-java/general/recognize-text-from-image-with-aspose-ocr-complete-python-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# распознавание текста с изображения с помощью Aspose OCR – Полное руководство на Python

Когда‑то вам нужно **распознать текст с изображения**, но не было уверенности, какая библиотека обеспечит и скорость, и точность? Вы не одиноки. В мире автоматизации документов возможность **выполнять OCR на изображениях** является ежедневной потребностью — будь то оцифровка чеков, сканирование паспортов или извлечение данных из многоязычных вывесок.

В этом руководстве мы пошагово покажем, как **распознавать текст с изображения** с помощью Aspose OCR для Python, а также разберём, **как задать язык OCR**, чтобы движок знал, имеет ли дело с латиницей, кириллицей или любой другой письменностью. К концу вы получите готовый к запуску скрипт, который выводит полный текст, уровень уверенности построчно и даже ограничивающие рамки для каждого слова.

## Что понадобится

- **Python 3.8+** (код работает на любой современной версии)
- Пакет **Aspose.OCR for Python via Java** – установите его командой `pip install aspose-ocr`
- Файл изображения (например, `mixed_script.png`), содержащий текст, который нужно извлечь
- Любая простая IDE или редактор — VS Code, PyCharm или даже обычный текстовый редактор подойдут

Никаких тяжёлых зависимостей, никаких нативных бинарных файлов для компиляции. Достаточно установить пакет через pip — и всё готово.

## Шаг 1: Установить и импортировать OCR‑движок

Сначала загрузим библиотеку на ваш компьютер и импортируем необходимые классы.

```python
# Install the package (run this once in your terminal)
# pip install aspose-ocr

# Import the OCR engine and the language enumeration
from asposeocrjava import OcrEngine, Language
```

> **Полезный совет:** Если вы работаете за корпоративным прокси, добавьте флаг `--proxy` к команде pip. Это сэкономит вам кучу времени на отладке.

## Шаг 2: Создать движок и **как задать язык OCR**

Создание экземпляра `OcrEngine` так же просто, как вызов его конструктора, но настоящая сила раскрывается, когда вы указываете движку, какой язык ожидать. Именно здесь отвечает на вопрос «**как задать язык OCR**».

```python
# Instantiate the OCR engine
ocr_engine = OcrEngine()

# Tell the engine we’re dealing with Latin script (you can pick others like Language.Cyrillic)
ocr_engine.setLanguage(Language.Latin)
```

Почему это важно? Алгоритмы OCR используют языко‑специфичные модели символов; правильный язык значительно повышает точность, особенно для письменностей с похожими глифами (например, «0» vs «O» в латинице против «О» в кириллице).

## Шаг 3: **выполнить OCR на изображении** – распознать текст

Теперь передаём движку путь к изображению и позволяем ему выполнить магию. Метод возвращает объект `RecognitionResult`, содержащий всё, что может понадобиться.

```python
# Path to the image you want to process
image_path = "YOUR_DIRECTORY/mixed_script.png"

# Run the OCR operation
recognition_result = ocr_engine.recognizeImage(image_path)
```

Если файл не найден, Aspose выбросит `FileNotFoundError`. Оберните вызов в блок `try/except` в продакшн‑коде — ничто так не портит сервис, как необработанное исключение.

## Шаг 4: Вывести полностью распознанный текст

Самый частый запрос — просто «дай мне текст». Метод `getText()` объединяет все найденные строки в одну строку.

```python
# Print the complete text extracted from the image
print("Full text:", recognition_result.getText())
```

Вы получите что‑то вроде:

```
Full text: Hello World!
This is a sample mixed‑script image.
```

Это и есть ядро **распознавания текста с изображения** — однострочник, возвращающий всё, что движок смог расшифровать.

## Шаг 5: (Опционально) Показать уверенность для каждой найденной строки

Оценки уверенности позволяют оценить надёжность. Строки с оценкой ниже, скажем, 0.70, могут потребовать ручной проверки.

```python
print("\n--- Line‑by‑Line Confidence ---")
for line in recognition_result.getLines():
    # Each line object provides its text and a confidence value between 0 and 1
    print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")
```

Пример вывода:

```
Line: 'Hello World!'  Confidence: 0.98
Line: 'This is a sample mixed‑script image.'  Confidence: 0.85
```

## Шаг 6: (Опционально) Получить ограничивающие рамки для каждого слова — полезно для UI‑подсветки

Если вы создаёте просмотрщик, где пользователь может кликнуть по слову и увидеть данные OCR, координаты рамок — настоящая ценность.

```python
print("\n--- Word Bounding Boxes ---")
for word in recognition_result.getWords():
    bbox = word.getBoundingBox()   # Returns (x, y, width, height)
    print(f"Word '{word.getText()}' at {bbox}")
```

Пример вывода:

```
Word 'Hello' at (12, 34, 58, 20)
Word 'World' at (78, 34, 60, 20)
```

Эти координаты указаны в пикселях относительно оригинального изображения, так что их можно напрямую накладывать на канвас.

## Полный рабочий скрипт

Объединив всё вместе, получаем готовый к запуску скрипт, который можно вставить в любой проект. Просто замените `YOUR_DIRECTORY/mixed_script.png` на реальный путь к вашему изображению.

```python
# ocr_demo.py
from asposeocrjava import OcrEngine, Language

def main(image_path: str, language: Language = Language.Latin):
    """
    Recognize text from an image using Aspose OCR.
    Parameters:
        image_path (str): Full path to the image file.
        language (Language): OCR language to use (default: Latin).
    """
    # Create the OCR engine and set the desired language
    ocr_engine = OcrEngine()
    ocr_engine.setLanguage(language)

    try:
        # Perform OCR
        result = ocr_engine.recognizeImage(image_path)

        # Full text output
        print("Full text:", result.getText())

        # Optional: line confidence
        print("\n--- Line‑by‑Line Confidence ---")
        for line in result.getLines():
            print(f"Line: '{line.getText()}'  Confidence: {line.getConfidence():.2f}")

        # Optional: word bounding boxes
        print("\n--- Word Bounding Boxes ---")
        for word in result.getWords():
            bbox = word.getBoundingBox()
            print(f"Word '{word.getText()}' at {bbox}")

    except FileNotFoundError:
        print(f"Error: Image file not found at {image_path}")
    except Exception as e:
        print(f"An unexpected error occurred: {e}")

if __name__ == "__main__":
    # Change the path below to point at your own test image
    IMAGE_PATH = "YOUR_DIRECTORY/mixed_script.png"
    main(IMAGE_PATH, Language.Latin)
```

Запустите его командой:

```bash
python ocr_demo.py
```

Вы увидите полностью извлечённый текст, оценки уверенности и координаты ограничивающих рамок, выведенные в консоль.

## Часто задаваемые вопросы и особые случаи

### Что делать, если изображение содержит несколько языков?

Aspose OCR поддерживает многоязычное распознавание, но необходимо передать **объединённый флаг языка**. Например, чтобы обрабатывать одновременно латиницу и кириллицу:

```python
ocr_engine.setLanguage(Language.Latin | Language.Cyrillic)
```

Оператор `|` объединяет перечисления. Это отвечает на требование «**выполнить OCR на изображении**» в многоязычных сценариях.

### Как улучшить точность на изображениях низкого разрешения?

- **Предобработать** изображение: увеличить контраст, применить бинаризацию или увеличить масштаб с помощью библиотеки Pillow.
- **Установить правильный DPI**, если он известен; Aspose учитывает метаданные изображения.
- **Выбрать правильный язык** — чем точнее указать язык, тем лучше работает модель.

### Можно ли извлекать только определённые области изображения?

Да. Используйте метод `recognizeRegion` (не показан в базовом примере) и передайте объект прямоугольника, определяющий интересующую область. Это удобно, когда нужен только таблица или конкретный блок текста.

## Заключение

Мы прошли полный сквозной пример того, как **распознавать текст с изображения** с помощью Aspose OCR для Python. Теперь вы знаете, как **выполнять OCR на изображении**, правильно **задать язык OCR** и получать как оценки уверенности, так и ограничивающие рамки на уровне слов для дальнейшей работы в UI.

Дальше вы можете:

- Поэкспериментировать с другими языками (`Language.Arabic`, `Language.Japanese` и т.д.)
- Интегрировать скрипт в веб‑сервис (Flask/Django), чтобы предоставлять OCR как API
- Скомбинировать данные о рамках с фронтенд‑канвасом, позволяя пользователям выделять текст

Возможности так же разнообразны, как документы, которые вам нужно оцифровать. Есть сложное изображение, отказывающееся распознаваться? Оставьте комментарий, и мы разберёмся вместе. Приятного кодинга! 

![пример распознавания текста с изображения](/images/ocr_example.png "распознавание текста с изображения – вывод Aspose OCR")


## Что изучать дальше?


Ниже представлены руководства, тесно связанные с темами, раскрытыми в этом пособии. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [распознавание текста изображения с Aspose OCR для нескольких языков](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Как установить пороговое значение в OCR‑распознавании изображений](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}