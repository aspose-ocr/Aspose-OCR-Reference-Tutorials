---
category: general
date: 2026-06-22
description: Предобработайте изображение для OCR, чтобы извлечь текст из изображения
  и улучшить точность OCR с использованием Aspose OCR в Python. Включён полный, готовый
  к запуску пример.
draft: false
keywords:
- preprocess image for OCR
- extract text from image
- improve OCR accuracy
language: ru
og_description: Подготовьте изображение для OCR, извлеките текст из изображения и
  улучшите точность OCR с помощью Aspose OCR. Узнайте полный процесс работы в Python.
og_title: Предобработка изображения для OCR – Полный учебник по Python
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  headline: Preprocess Image for OCR – Step‑by‑Step Python Guide
  type: TechArticle
- description: Preprocess image for OCR to extract text from image and improve OCR
    accuracy using Aspose OCR in Python. Complete, runnable example included.
  name: Preprocess Image for OCR – Step‑by‑Step Python Guide
  steps:
  - name: Prerequisites
    text: '| Requirement | Why it matters | |-------------|----------------| | Python
      3.8+ | Aspose OCR’s wheels target modern interpreters. | | `aspose-ocr` package
      (`pip install aspose-ocr`) | Provides the `OcrEngine`, `ImagePreprocessor`,
      and filter classes. | | A sample image (e.g., `noisy-document.jpg`) |'
  - name: – Initialise the OCR Engine and Load Your Source Image
    text: '```python import aspose.ocr as ocr'
  - name: – Build a Preprocessing Chain to Clean the Image
    text: '```python # Initialise the preprocessor – a container for a series of filters
      preprocessor = ocr.ImagePreprocessor()'
  - name: – Attach the Preprocessor to the Engine
    text: '```python # Hook the preprocessing pipeline into the OCR engine ocr_engine.set_preprocessor(preprocessor)
      ```'
  - name: – Run OCR and Extract Text from Image
    text: '```python # Perform the recognition on the pre‑processed image recognition_result
      = ocr_engine.recognize()'
  - name: – Verify the Output and Fine‑Tune for Better Accuracy
    text: '```python # Quick sanity check: print length and a sample snippet print(f"Detected
      {len(extracted_text)} characters.") print("First 200 chars:", extracted_text[:200])
      ```'
  type: HowTo
- questions:
  - answer: Yes. Convert each page to an image (e.g., using `pdf2image`) and feed
      it through the same pipeline in a loop. The same `preprocess image for OCR`
      steps apply per page.
    question: Does this work with multi‑page PDFs?
  - answer: 'Set the language before recognition: `engine.set_language(ocr.Language.FRENCH)`.
      The preprocessing filters stay the same; only the language model changes.'
    question: What if my document is in a language other than English?
  - answer: 'Absolutely. The `ImagePreprocessor` is extensible—just call `add_filter`
      again. For heavy‑dotted backgrounds, `ocr.Filters.MedianFilter(kernel=3)` can
      be useful. --- ## Wrap‑Up We’ve just **preprocess image for OCR**, run Aspose’s
      engine, and **extract text from image** while showcasing several tric'
    question: Can I chain more filters?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Предобработка изображения для OCR – пошаговое руководство на Python
url: /ru/python-java/general/preprocess-image-for-ocr-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Предобработка изображения для OCR – Полный учебник на Python

Если вам нужно **preprocess image for OCR**, вы, вероятно, сталкивались с шумными сканами, наклонными страницами или фотографиями с низким контрастом, которые просто не хотят работать. Пробовали извлечь текст из изображения и получили кучу непонятных символов? Именно здесь надёжная цепочка предобработки может стать разницей между несколькими читаемыми словами и полной катастрофой транскрипции.

В этом руководстве мы пройдём полный пример от начала до конца, который **extracts text from image**, одновременно показывая, как **improve OCR accuracy** с помощью Aspose OCR for Python. Никаких расплывчатых ссылок — только код, который вы можете скопировать‑вставить, объяснение каждой строки и советы для реальных граничных случаев.

## Что вы получите

- Готовый к запуску скрипт на Python, который загружает шумный документ, очищает его и выводит распознанный текст.  
- Понимание того, почему каждый фильтр предобработки важен и как настраивать его параметры.  
- Стратегии обработки распространённых проблем, таких как сильный шум‑пятнистость, экстремальное вращение или сканы с низким контрастом.  

### Требования

| Требование | Почему это важно |
|-------------|-------------------|
| Python 3.8+ | Колёса Aspose OCR ориентированы на современные интерпретаторы. |
| `aspose-ocr` package (`pip install aspose-ocr`) | Предоставляет `OcrEngine`, `ImagePreprocessor` и классы фильтров. |
| A sample image (e.g., `noisy-document.jpg`) | Мы используем специально «грязное» изображение, чтобы продемонстрировать выгоды предобработки. |
| Basic familiarity with Python functions | Помогает адаптировать скрипт под ваш собственный конвейер. |

> **Pro tip:** Если вы работаете в Windows, запускайте скрипт внутри виртуального окружения, чтобы избежать конфликтов версий.

---

## Предобработка изображения для OCR с Aspose OCR (Python)

Ниже представлена суть учебника — пошаговый разбор кода, который вам понадобится. Каждый раздел объясняет **что** мы делаем *и* **почему**, чтобы вы могли позже настроить конвейер без догадок.

![preprocess image for OCR example](ocr-preprocess.png){alt="preprocess image for OCR"}

### Шаг 1 – Инициализация OCR Engine и загрузка исходного изображения

```python
import aspose.ocr as ocr

# Create the OCR engine – the central object that drives recognition
ocr_engine = ocr.OcrEngine()

# Load the raw image file. Using ImageStream lets Aspose handle various formats.
ocr_engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))
```

- **Почему** `OcrEngine`? Он инкапсулирует распознаватель, настройки языка и (позже) предобработчик.  
- **Почему** `ImageStream.from_file`? Он абстрагирует работу с типами файлов, позволяя менять JPEG на PNG без изменений кода.

### Шаг 2 – Создание цепочки предобработки для очистки изображения

```python
# Initialise the preprocessor – a container for a series of filters
preprocessor = ocr.ImagePreprocessor()

# 1️⃣ Deskew – corrects any rotation so text lines become horizontal.
preprocessor.add_filter(ocr.Filters.Deskew())

# 2️⃣ Despeckle – removes isolated noise pixels; strength=2 is a good middle ground.
preprocessor.add_filter(ocr.Filters.Despeckle(strength=2))

# 3️⃣ ContrastBoost – lifts faint characters; level=1.5 amplifies contrast without blowing out highlights.
preprocessor.add_filter(ocr.Filters.ContrastBoost(level=1.5))
```

**Как эти фильтры повышают точность OCR:**

- **Deskew** устраняет распространённую проблему «наклонённой страницы», которая сбивает сегментацию символов.  
- **Despeckle** устраняет пятна, возникающие из‑за сканеров низкого качества; более высокая сила удаляет больше шума, но может стирать мелкие детали.  
- **ContrastBoost** делает тёмный текст более заметным на светлом фоне, что является классическим преимуществом для большинства OCR‑движков.

> **Edge case:** Если ваш документ уже идеально прямой, вы можете пропустить `Deskew()`, чтобы сэкономить несколько миллисекунд.

### Шаг 3 – Привязка предобработчика к движку

```python
# Hook the preprocessing pipeline into the OCR engine
ocr_engine.set_preprocessor(preprocessor)
```

Теперь каждый раз, когда вызывается `ocr_engine.recognize()`, сначала будут применены три фильтра в точно заданном порядке. Порядок важен: нужно **deskew before despeckling**, иначе фильтр шума может принять повернутые края за шум.

### Шаг 4 – Запуск OCR и извлечение текста из изображения

```python
# Perform the recognition on the pre‑processed image
recognition_result = ocr_engine.recognize()

# Pull out the plain text string
extracted_text = recognition_result.get_text()
print(extracted_text)
```

- Вызов `recognize()` возвращает объект `RecognitionResult`, который содержит не только необработанный текст, но и оценки уверенности, ограничивающие рамки и детали языка.  
- Здесь нам нужен только простой строковый результат, но вы можете исследовать `recognition_result.get_confidence()` для быстрой проверки **improve OCR accuracy**.

### Шаг 5 – Проверка вывода и тонкая настройка для лучшей точности

```python
# Quick sanity check: print length and a sample snippet
print(f"Detected {len(extracted_text)} characters.")
print("First 200 chars:", extracted_text[:200])
```

Если вывод всё ещё содержит искажённые символы, рассмотрите следующие настройки:

| Проблема | Предлагаемое решение |
|----------|----------------------|
| Текст всё ещё размытый | Увеличьте `ContrastBoost(level)` до 2.0 или добавьте `ocr.Filters.GaussianBlur(radius=1)` перед despeckling. |
| Слишком много лишних символов | Повышайте `Despeckle(strength)` до 3, либо вставьте `ocr.Filters.RemoveLines()` для удаления горизонтальных линий. |
| Наклон сохраняется | Вызовите `ocr.Filters.Deskew(max_angle=5)`, чтобы ограничить коррекцию небольшими вращениями. |

---

## Полный, исполняемый скрипт

Скопируйте блок ниже в файл с именем `ocr_preprocess.py`. Замените `YOUR_DIRECTORY/noisy-document.jpg` реальным путём к вашему изображению, затем выполните `python ocr_preprocess.py`.

```python
import aspose.ocr as ocr

def main():
    # Initialise engine and load image
    engine = ocr.OcrEngine()
    engine.set_image(ocr.ImageStream.from_file("YOUR_DIRECTORY/noisy-document.jpg"))

    # Build preprocessing pipeline
    preproc = ocr.ImagePreprocessor()
    preproc.add_filter(ocr.Filters.Deskew())
    preproc.add_filter(ocr.Filters.Despeckle(strength=2))
    preproc.add_filter(ocr.Filters.ContrastBoost(level=1.5))

    # Attach pipeline
    engine.set_preprocessor(preproc)

    # Recognise and extract text
    result = engine.recognize()
    text = result.get_text()

    # Display results
    print("\n--- OCR Output ---")
    print(text)
    print("\n--- Summary ---")
    print(f"Characters detected: {len(text)}")
    print("Snippet:", text[:200].replace("\n", " "))

if __name__ == "__main__":
    main()
```

Запуск этого скрипта на шумном, слегка повернутом JPEG должен дать чистый, читаемый текст — демонстрируя, как правильно построенная цепочка предобработки **improves OCR accuracy** значительно.

---

## Часто задаваемые вопросы и ответы

**Q: Работает ли это с многостраничными PDF?**  
A: Да. Преобразуйте каждую страницу в изображение (например, с помощью `pdf2image`) и пропустите её через тот же конвейер в цикле. Те же шаги `preprocess image for OCR` применяются к каждой странице.

**Q: Что если мой документ на языке, отличном от английского?**  
A: Установите язык перед распознаванием: `engine.set_language(ocr.Language.FRENCH)`. Фильтры предобработки остаются теми же; меняется только языковая модель.

**Q: Можно ли добавить больше фильтров?**  
A: Конечно. `ImagePreprocessor` расширяемый — просто вызовите `add_filter` ещё раз. Для сильно точечных фонов может быть полезен `ocr.Filters.MedianFilter(kernel=3)`.

---

## Итоги

Мы только что **preprocess image for OCR**, запустили движок Aspose и **extract text from image**, продемонстрировав несколько приёмов для **improve OCR accuracy**. Полный пример готов к использованию в любом проекте, а модульный дизайн фильтров позволяет заменять, добавлять или удалять шаги по мере необходимости.

Далее вы можете изучить:

- **Пакетную обработку** десятков сканов с помощью `concurrent.futures`.  
- **Пост‑обработку** с библиотеками проверки орфографии (например, `pyspellchecker`) для исправления опечаток, внесённых OCR.  
- **Интеграцию** скрипта в веб‑службу с использованием Flask или FastAPI, превратив его в OCR‑микросервис по запросу.

Попробуйте, настройте силы фильтров и наблюдайте, как растут показатели распознавания. Если возникнут проблемы, оставьте комментарий — удачной разработки!

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to Use AspOCR: Preprocess Image OCR Filters for .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}