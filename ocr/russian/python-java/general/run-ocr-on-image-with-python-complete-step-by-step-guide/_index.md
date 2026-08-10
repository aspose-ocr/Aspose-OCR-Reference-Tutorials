---
category: general
date: 2026-06-06
description: Запустите OCR на изображении с помощью Python и посмотрите оценки уверенности.
  Узнайте, как фильтровать слова с низкой уверенностью, устанавливать пороги и обрабатывать
  крайние случаи.
draft: false
keywords:
- run OCR on image
- Python OCR tutorial
- OCR confidence threshold
- low‑confidence word detection
- image text extraction
language: ru
og_description: Выполните OCR изображения в Python, проверьте уровни уверенности и
  отфильтруйте слова с низкой уверенностью. Этот учебник проведёт вас через полный,
  готовый к запуску пример.
og_title: Запустите OCR на изображении с помощью Python – Полное руководство
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  headline: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Run OCR on image using Python and see confidence scores. Learn how
    to filter low‑confidence words, set thresholds, and handle edge cases.
  name: Run OCR on Image with Python – Complete Step‑by‑Step Guide
  steps:
  - name: Install and Import the OCR Engine
    text: First, make sure the OCR library is available. **EasyOCR** works out‑of‑the‑box
      for many languages and gives you a confidence score per word.
  - name: Run OCR on the Image
    text: Now we actually **run OCR on image**. The `recognize_image` method from
      the original example is replaced with EasyOCR’s `readtext` call, which returns
      a list of `(bbox, text, confidence)` tuples.
  - name: Summarize Overall Confidence
    text: 'Unlike the earlier snippet that printed a single `confidence` attribute,
      EasyOCR gives a confidence per word. To get an overall sense, we’ll average
      them:'
  - name: List Low‑Confidence Words
    text: Now comes the part that directly answers the “list words whose confidence
      is below the desired threshold” requirement. We’ll set a **OCR confidence threshold**
      of 0.80 (80 %) by default, but you can adjust it.
  - name: Edge Cases & Variations
    text: 1. **Batch Processing** – If you need to **run OCR on image** files in bulk,
      wrap the above logic in a loop that iterates over a directory. 2. **Multiple
      Languages** – Pass a list like `['en', 'fr']` to `easyocr.Reader` and the engine
      will detect both. 3. **Alternative Engines** – Want to try **pyte
  type: HowTo
- questions:
  - answer: Not directly. Convert each PDF page to an image first (e.g., with `pdf2image`)
      and then feed the PNG/JPEG into the script.
    question: Does this work with PDFs?
  - answer: 'Try image preprocessing: increase contrast, remove background noise,
      or rotate the image to a horizontal baseline. EasyOCR also accepts a `contrast_ths`
      parameter you can tweak.'
    question: My confidence numbers are all low—what can I do?
  - answer: Absolutely. After the low‑confidence loop, write `ocr_results` to a `csv.DictWriter`
      where each row contains `text`, `confidence`, and bounding‑box coordinates.
    question: Can I export the results to CSV?
  - answer: 'EasyOCR automatically uses CUDA if a compatible GPU and PyTorch are installed.
      Verify with `torch.cuda.is_available()` before running the script. --- ## Conclusion
      We’ve just **run OCR on image** using Python, inspected the overall confidence,
      and isolated any low‑confidence words that need a {{< /b'
    question: Is there a GPU‑accelerated version?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: Запуск OCR на изображении с помощью Python — Полное пошаговое руководство
url: /ru/python-java/general/run-ocr-on-image-with-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнить OCR на изображении с помощью Python – Полное пошаговое руководство

Когда‑то вам нужно **выполнить OCR на изображении**, но вы не знали, как получить надёжный текст? Вы не одиноки — многие разработчики сталкиваются с тем же: извлечённые слова выглядят «дрожащими», а показатель уверенности остаётся загадкой.  

В этом руководстве мы сразу перейдём к работающему решению: вы увидите, как выполнить OCR на изображении, прочитать общую уверенность и вытащить любые слова с низкой уверенностью, которые могут потребовать ручной проверки. К концу вы получите переиспользуемый скрипт, поймёте, почему каждая строка важна, и узнаете, как настроить порог уверенности для своих проектов.

## Что покрывает этот учебник

Мы пройдём весь процесс — от загрузки изображения до печати аккуратного отчёта о словах, у которых уверенность ниже 80 %. По пути обсудим:

* Выбор надёжного OCR‑движка (мы будем использовать **EasyOCR**, популярную библиотеку OCR для Python)  
* Интерпретацию атрибута `confidence`, который возвращает каждый результат OCR  
* Фильтрацию слов с помощью пользовательского **порога уверенности OCR**  
* Расширение скрипта для пакетной обработки или альтернативных движков, таких как **pytesseract**  

Предыдущий опыт работы с OCR не требуется, достаточно базовых знаний Python и рабочей среды (рекомендовано Python 3.9+).  

Готовы превратить размытые скриншоты в чистый, индексируемый текст? Поехали.

---

## ## Как выполнить OCR на изображении с помощью Python

Сердце учебника — трёхшаговый фрагмент кода, который отражает уже показанный пример. Ниже мы разберём каждую строку, объясним, почему она нужна, и предоставим готовый скрипт, готовый к копированию.

### Шаг 1: Установить и импортировать OCR‑движок

Сначала убедитесь, что библиотека OCR доступна. **EasyOCR** работает «из коробки» для многих языков и выдаёт оценку уверенности для каждого слова.

```bash
pip install easyocr
```

```python
import easyocr  # The engine that will run OCR on image files
import os
```

*Почему EasyOCR?* Он включает модель глубокого обучения, обученную на разнообразных наборах данных, поэтому обычно выдаёт более высокие значения уверенности, чем старый движок Tesseract, особенно на изображениях смешанного качества.

> **Pro tip:** Если вы работаете в ограниченной среде (например, в небольшом Docker‑контейнере), `pytesseract` может быть легче, но вы потеряете часть современной точности, которую предоставляет EasyOCR.

### Шаг 2: Выполнить OCR на изображении

Теперь мы действительно **выполняем OCR на изображении**. Метод `recognize_image` из оригинального примера заменён вызовом `readtext` из EasyOCR, который возвращает список кортежей `(bbox, text, confidence)`.

```python
# Initialize the OCR reader for English (you can add more languages as needed)
reader = easyocr.Reader(['en'])

# Path to the image you want to process
image_path = os.path.join("YOUR_DIRECTORY", "mixed_quality.png")

# Perform OCR – this is the step where we run OCR on image
ocr_results = reader.readtext(image_path, detail=1, paragraph=False)
```

Каждый элемент в `ocr_results` выглядит так:

```python
[
    ((x1, y1, x2, y2, x3, y3, x4, y4), "Detected text", 0.92),
    ...
]
```

Третий элемент (`0.92` в примере) — это оценка уверенности в диапазоне от 0 до 1.

### Шаг 3: Суммировать общую уверенность

В отличие от предыдущего фрагмента, который выводил единственный атрибут `confidence`, EasyOCR даёт уверенность для каждого слова. Чтобы получить общее представление, мы вычислим их среднее:

```python
# Extract just the confidence numbers
confidences = [item[2] for item in ocr_results]

# Compute the mean confidence (overall confidence)
overall_confidence = sum(confidences) / len(confidences) if confidences else 0

print(f"Overall confidence: {overall_confidence:.2%}")
```

*Почему среднее?* Оно даёт быструю проверку состояния — если общая уверенность ниже, скажем, 70 %, вероятно, потребуется улучшить изображение (лучшее освещение, предобработка и т.д.).

### Шаг 4: Список слов с низкой уверенностью

Теперь переходим к части, которая напрямую отвечает на требование «вывести список слов, чья уверенность ниже заданного порога». По умолчанию мы задаём **порог уверенности OCR** = 0.80 (80 %), но вы можете изменить его.

```python
# Define the confidence threshold – tweak as needed
THRESHOLD = 0.80

print("\nLow‑confidence words:")
low_confidence_found = False
for bbox, text, conf in ocr_results:
    if conf < THRESHOLD:
        low_confidence_found = True
        print(f"  • '{text}' ({conf:.2%})")
if not low_confidence_found:
    print("  All words meet the confidence threshold.")
```

Цикл выводит каждое слово, которое не прошло порог, вместе с процентом уверенности. Это точный аналог оригинального цикла `for recognized_word in recognition_result.words`, но теперь работает с форматом вывода EasyOCR.

---

## ## Понимание оценок уверенности OCR

Уверенность — это не магическое число; это оценка модели того, насколько она уверена в конкретной транскрипции. Учтите следующее:

| Ситуация | Типичная уверенность | Что делать |
|-----------|-------------------|------------|
| Чёткое, высокоразрешающее сканирование | 0.95 – 1.00 | Дополнительные действия не требуются |
| Небольшое размытие или неравномерное освещение | 0.80 – 0.94 | Рассмотрите лёгкую предобработку (повышение контраста) |
| Сильный шум, повернутый текст | < 0.70 | Примените предобработку (выравнивание, удаление шума) или переключитесь на другой OCR‑движок |

> **Watch out:** Некоторые языки (например, курсивное рукописное письмо) естественно дают более низкие оценки. Настройте порог соответственно.

### Пограничные случаи и варианты

1. **Пакетная обработка** – Если нужно **выполнить OCR на изображениях** массово, оберните вышеописанную логику в цикл, проходящий по каталогу.  
2. **Несколько языков** – Передайте список вроде `['en', 'fr']` в `easyocr.Reader`, и движок будет распознавать оба.  
3. **Альтернативные движки** – Хотите попробовать **pytesseract**? Замените блок чтения на:

   ```python
   import pytesseract
   from PIL import Image

   img = Image.open(image_path)
   raw_text = pytesseract.image_to_string(img, output_type=pytesseract.Output.DICT)
   # raw_text['text'] contains the full string,
   # raw_text['conf'] holds per‑character confidence.
   ```

   Затем потребуется агрегировать уверенности по символам в уверенности по словам — немного больше работы, но выполнимо.

4. **Трюки предобработки** – Применение фильтров OpenCV (`cv2.threshold`, `cv2.GaussianBlur`) может повысить уверенность на шумных сканах.  

---

## ## Полный готовый к запуску скрипт

Ниже представлен полностью готовый файл Python, который можно добавить в проект. Сохраните его как `ocr_report.py` и запустите `python ocr_report.py`. Убедитесь, что путь к изображению указывает на реальный файл.

```python
#!/usr/bin/env python3
"""
run_ocr_on_image.py

A self‑contained script that:
  1. Runs OCR on an image using EasyOCR.
  2. Prints the overall confidence.
  3. Lists any words whose confidence falls below a configurable threshold.

Author: Your Name
Date: 2026‑06‑06
"""

import os
import easyocr

# --------------------------- Configuration --------------------------- #
IMAGE_DIR = "YOUR_DIRECTORY"          # <-- Change to your folder
IMAGE_NAME = "mixed_quality.png"      # <-- Change to your file name
THRESHOLD = 0.80                       # Confidence threshold (0‑1)

# --------------------------- Helper Functions ----------------------- #
def load_image_path():
    """Construct the absolute path to the target image."""
    return os.path.join(IMAGE_DIR, IMAGE_NAME)

def run_ocr(image_path):
    """Run OCR on the image and return detailed results."""
    reader = easyocr.Reader(['en'])
    return reader.readtext(image_path, detail=1, paragraph=False)

def compute_overall_confidence(results):
    """Return the mean confidence across all detected words."""
    if not results:
        return 0.0
    confidences = [item[2] for item in results]
    return sum(confidences) / len(confidences)

def report_low_confidence_words(results, threshold):
    """Print words whose confidence is below the given threshold."""
    low_conf = [(text, conf) for _, text, conf in results if conf < threshold]
    if not low_conf:
        print("All words meet the confidence threshold.")
    else:
        for text, conf in low_conf:
            print(f"Low‑confidence word: '{text}' ({conf:.2%})")

# --------------------------- Main Execution ------------------------ #
def main():
    image_path = load_image_path()
    if not os.path.isfile(image_path):
        print(f"❌ Image not found: {image_path}")
        return

    # Step 1: Run OCR on image
    ocr_results = run_ocr(image_path)

    # Step 2: Show overall confidence
    overall = compute_overall_confidence(ocr_results)
    print(f"Overall confidence: {overall:.2%}")

    # Step 3: List low‑confidence words
    print("\n--- Low‑confidence words (threshold: {0:.0%}) ---".format(THRESHOLD))
    report_low_confidence_words(ocr_results, THRESHOLD)

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод** (ваши цифры будут отличаться):

```
Overall confidence: 78.45%

--- Low‑confidence words (threshold: 80%) ---
Low‑confidence word: 'recgnition' (62.13%)
Low‑confidence word: 'imgae' (57.90%)
```

Если каждое слово превышает порог в 80 %, вы увидите дружелюбное сообщение «All words meet the confidence threshold.».

---

## ## Часто задаваемые вопросы (FAQ)

**В: Работает ли это с PDF?**  
О: Не напрямую. Сначала преобразуйте каждую страницу PDF в изображение (например, с помощью `pdf2image`), а затем передайте PNG/JPEG в скрипт.

**В: Все мои оценки уверенности низкие — что делать?**  
О: Попробуйте предобработку изображения: увеличьте контраст, удалите фоновой шум или поверните изображение в горизонтальное положение. EasyOCR также принимает параметр `contrast_ths`, который можно настроить.

**В: Можно ли экспортировать результаты в CSV?**  
О: Конечно. После цикла с низкой уверенностью запишите `ocr_results` в `csv.DictWriter`, где каждая строка будет содержать `text`, `confidence` и координаты ограничивающего прямоугольника.

**В: Есть ли версия с ускорением на GPU?**  
О: EasyOCR автоматически использует CUDA, если совместимый GPU и PyTorch установлены. Проверьте `torch.cuda.is_available()` перед запуском скрипта.

---

## Заключение

Мы только что **выполнили OCR на изображении** с помощью Python, проверили общую уверенность и выделили любые слова с низкой уверенностью, которые требуют ручного вмешательства.

## Что изучать дальше?

Следующие учебники охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)
- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}