---
category: general
date: 2026-01-12
description: Как быстро выполнить OCR и преобразовать изображение в текст. Узнайте,
  как распознавать специальные символы, извлекать текст из изображения и загружать
  изображение для OCR с полным примером на Python.
draft: false
keywords:
- how to perform OCR
- convert image to text
- recognize special characters
- extract text from image
- load image for OCR
language: ru
og_description: Как выполнить OCR в Python, преобразовать изображение в текст и распознать
  специальные символы. Следуйте этому практическому руководству по извлечению текста
  из изображений.
og_title: Как выполнить OCR в Python – Полный учебник
tags:
- OCR
- Python
- Image Processing
title: Как выполнить OCR в Python – пошаговое руководство
url: /ru/python/general/how-to-perform-ocr-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в Python – пошаговое руководство

Когда‑нибудь вам нужно было **выполнять OCR** на скриншоте, содержащем как латинские, так и кириллические символы? Вы не одиноки. Во многих проектах — будь то оцифровка чеков, индексация многоязычных документов или создание поискового архива — **как выполнять OCR** быстро становится актуальным вопросом.  

В этом руководстве мы пройдем через полностью готовый к запуску пример, который покажет, как **конвертировать изображение в текст**, **распознавать специальные символы** и **извлекать текст из изображения** с помощью простой библиотеки Python. К концу вы получите готовый к запуску скрипт, который загружает изображение для OCR, обрабатывает многоязычное содержание и выводит результат.

## Что понадобится

Перед тем как начать, убедитесь, что у вас есть следующие предварительные условия:

- Python 3.8+ установлен на вашем компьютере.  
- Пакет `ocr` (или любая совместимая OCR‑библиотека), установленный через `pip install ocr`.  
- Файл изображения (`multilingual.png`), содержащий как латинские, так и кириллические глифы.  
- Базовый текстовый редактор или IDE — VS Code, PyCharm или даже простой Блокнот подойдёт.  

Если у вас нет пакета `ocr`, вы можете заменить его на `pytesseract` с несколькими небольшими изменениями; основные концепции остаются теми же.

## Шаг 1: Установить и импортировать OCR‑библиотеку

Сначала подготовим OCR‑движок. Мы импортируем библиотеку, создадим экземпляр движка и настроим его для поддержки многоязычия.

```python
# Install the library (run this once in your terminal)
# pip install ocr

import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()

# Optional: Enable language packs for Latin and Cyrillic
engine.set_languages(['eng', 'rus'])  # 'eng' = English, 'rus' = Russian
```

**Почему это важно:**  
Создание движка — это фундамент; без него вы не сможете **загрузить изображение для OCR** позже. Включение языковых пакетов гарантирует, что движок сможет корректно идентифицировать такие символы, как “Ŀ”, “Ҕ” и “Ǣ”. Если пропустить этот шаг, вы получите искажённый вывод для нелатинских скриптов.

## Шаг 2: Загрузить изображение с многоязычным текстом

Теперь укажем движку файл, который нужно обработать. Путь может быть абсолютным или относительным; просто убедитесь, что он указывает на читаемое изображение.

```python
# Step 2: Load the image containing multilingual text
image_path = "YOUR_DIRECTORY/multilingual.png"  # replace with your actual path
engine.load_image(image_path)
```

> ![пример выполнения OCR](/images/ocr-example.png "выполнение OCR на многоязычном изображении")

**Почему это важно:**  
Вызов `load_image` считывает пиксельные данные в память, подготавливая их к работе OCR‑алгоритма. Если изображение большое, движок может автоматически уменьшить его масштаб; позже вы сможете точно настроить это с помощью `engine.set_max_resolution(3000)` для сканов высокого разрешения.

## Шаг 3: Запустить процесс распознавания

С движком, подготовленным и изображением, загруженным, мы наконец можем извлечь текстовое содержание.

```python
# Step 3: Perform OCR recognition on the loaded image
result = engine.recognize()
```

**Почему это важно:**  
`recognize()` выполняет тяжёлую работу нейронной сети за кулисами. Он возвращает объект, содержащий исходный текст, оценки уверенности и даже ограничивающие рамки, если они нужны для визуальной отладки.

## Шаг 4: Вывести распознанный текст

Посмотрим, что нашёл движок. Мы выведем текст в консоль, но вы также можете записать его в файл или базу данных.

```python
# Step 4: Output the recognized text, which should include characters like “Ŀ”, “Ҕ”, “Ǣ”
print("=== OCR Result ===")
print(result.text)
```

### Ожидаемый вывод

```
=== OCR Result ===
Hello, world! Ŀ is a Latin‑extended character.
Привет, мир! Ҕ is a Cyrillic character.
Special combo: Ǣ is a ligature.
```

Если вы видите что‑то похожее, поздравляем — вы успешно **конвертировали изображение в текст** и **распознали специальные символы**.

## Обработка распространённых проблем

Даже с простым скриптом могут возникнуть некоторые трудности. Ниже — практические советы из собственного опыта.

### 1. Отсутствуют языковые пакеты

Если вместо кириллических букв вы получаете знаки вопроса (`?`), проверьте, что языковые пакеты установлены. Для многих OCR‑движков необходимо скачать соответствующие файлы `.traineddata` и разместить их в папке `tessdata` движка.

```python
# Example for pytesseract
import pytesseract
pytesseract.pytesseract.tesseract_cmd = r"C:\Program Files\Tesseract-OCR\tesseract.exe"
# Ensure 'eng' and 'rus' data files exist in tessdata
```

### 2. Низкое качество изображения

Размытые или низкоконтрастные изображения дают низкие оценки уверенности. Предобработайте изображение с помощью OpenCV:

```python
import cv2

# Load, convert to grayscale, and apply thresholding
raw = cv2.imread(image_path)
gray = cv2.cvtColor(raw, cv2.COLOR_BGR2GRAY)
_, thresh = cv2.threshold(gray, 150, 255, cv2.THRESH_BINARY)

# Save a temporary cleaned image and feed it to the OCR engine
cv2.imwrite("cleaned.png", thresh)
engine.load_image("cleaned.png")
```

### 3. Большие файлы и использование памяти

Обработка фотографии размером 10 МБ может резко увеличить потребление памяти. Используйте `engine.set_max_image_size(2000)`, чтобы ограничить разрешение, либо разбейте изображение на плитки и выполните OCR для каждой плитки отдельно.

### 4. Получение ограничивающих рамок

Если нужно подсветить, где находится каждое слово (полезно для наложения в UI), обратитесь к `result.boxes`:

```python
for box in result.boxes:
    print(f"Word: {box.text} – Coordinates: {box.x0},{box.y0},{box.x1},{box.y1}")
```

## Полный скрипт — однократный запуск

Объединив всё вместе, получаем один файл, который можно запустить как `python ocr_demo.py`. В нём есть обработка ошибок, необязательная предобработка и комментарии для ясности.

```python
#!/usr/bin/env python3
"""
Complete OCR demo: load image, recognize multilingual text,
and print results. Works with the generic 'ocr' library.
"""

import os
import sys
import ocr

def main(image_path: str):
    # Verify the image exists
    if not os.path.isfile(image_path):
        sys.exit(f"Error: File not found – {image_path}")

    # Initialize the OCR engine
    engine = ocr.OcrEngine()
    engine.set_languages(['eng', 'rus'])          # load language packs
    engine.set_max_image_size(2500)               # limit memory usage

    # Load the image
    try:
        engine.load_image(image_path)
    except Exception as e:
        sys.exit(f"Failed to load image: {e}")

    # Perform recognition
    try:
        result = engine.recognize()
    except Exception as e:
        sys.exit(f"OCR failed: {e}")

    # Output the text
    print("\n=== OCR Result ===")
    print(result.text)

    # Optional: display confidence scores
    if hasattr(result, "confidence"):
        avg_conf = sum(result.confidence) / len(result.confidence)
        print(f"\nAverage confidence: {avg_conf:.1%}")

if __name__ == "__main__":
    # Replace with your actual image path or pass as CLI argument
    img = sys.argv[1] if len(sys.argv) > 1 else "YOUR_DIRECTORY/multilingual.png"
    main(img)
```

Запустите его с помощью:

```bash
python ocr_demo.py path/to/multilingual.png
```

Вы должны увидеть тот же вывод, что и ранее, подтверждая, что вы **извлекли текст из изображения** успешно.

## Заключение

Мы рассмотрели **как выполнять OCR** в Python от начала до конца: установка библиотеки, загрузка изображения, распознавание многоязычного содержания и обработка самых распространённых граничных случаев. Следуя этому руководству, вы теперь можете **конвертировать изображение в текст**, **распознавать специальные символы** и **извлекать текст из изображения** в своих проектах — без ручного перепечатывания.

Что дальше? Попробуйте поэкспериментировать с:

- Добавление дополнительных языковых пакетов (например, `spa` для испанского).  
- Экспорт результатов в JSON для дальнейшей обработки.  
- Интеграция шага OCR в Flask API, чтобы другие сервисы могли вызывать его.  

Если столкнётесь с какими‑либо странностями, сообщество большинства OCR‑библиотек активно — ищите “ocr library language pack installation” или оставляйте комментарий ниже. Счастливого кодинга и приятного превращения картинок в поисковый текст!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}