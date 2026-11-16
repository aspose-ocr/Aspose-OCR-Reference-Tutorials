---
category: general
date: 2026-03-18
description: Как использовать OCR для извлечения текста из изображений — краткое руководство
  по распознаванию текста из PNG‑файлов и загрузке изображений для OCR.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- how to extract text
- load image for OCR
language: ru
og_description: Как использовать OCR для извлечения текста из изображений — научитесь
  распознавать текст из PNG, загружать изображение для OCR и извлекать текст с помощью
  простого скрипта на Python.
og_title: 'Как использовать OCR: извлечение текста из изображений в Python'
tags:
- OCR
- Python
- Image Processing
title: 'Как использовать OCR: извлечение текста из изображений в Python'
url: /ru/python-java/general/how-to-use-ocr-extract-text-from-images-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR: извлечение текста из изображений в Python

Когда‑то задумывались **как использовать OCR**, имея неаккуратный скриншот или отсканированный чек? Вы не одиноки — разработчикам постоянно нужно вытаскивать читаемый текст из картинок, особенно PNG, полученных из мобильных приложений или веб‑загрузок. В этом руководстве мы пройдем полный, готовый к запуску пример, показывающий, как **извлекать текст из изображений**, **распознавать текст из PNG**‑файлов и даже **загружать изображение для OCR** всего в несколько строк кода на Python.

Мы охватим всё: от установки нужной библиотеки до работы с многоязычными документами, так что к концу вы точно будете знать *как извлекать текст* из любого изображения, которое бросите в движок. Никаких расплывчатых ссылок, только чёткое пошаговое решение, которое можно скопировать‑вставить и запустить.

## Что вы узнаете

В следующих разделах мы:

1. Настроим лёгкий OCR‑движок (без тяжёлых зависимостей).  
2. Загрузим файл изображения — конкретно PNG — в движок.  
3. Включим автоматическое определение языка, чтобы движок мог работать с многоязычным контентом.  
4. Запустим процесс распознавания и получим результат в виде простого текста.  
5. Подправим рабочий процесс для крайних случаев, таких как отсутствие файлов или неподдерживаемые форматы.

Если вы уверенно владеете базовым Python, вам всё подойдёт. Предыдущий опыт работы с OCR не требуется, хотя быстрый взгляд на документацию библиотеки никогда не помешает.

---

![Как использовать OCR на PNG‑изображении](placeholder.png "Как использовать OCR на PNG‑изображении – пошаговое руководство")

## Как использовать OCR – загрузка изображения и распознавание текста {#how-to-use-ocr}

### Шаг 1: Установите OCR‑библиотеку

Первым делом вам нужен Python‑пакет, предоставляющий класс `OcrEngine`. Для целей этого руководства мы будем использовать вымышленный, но наглядный пакет **SimpleOCR**, который можно установить через pip:

```bash
pip install simple-ocr
```

> **Pro tip:** Если вы работаете в виртуальном окружении (настоятельно рекомендуется), активируйте его перед выполнением команды установки. Это поможет поддерживать зависимости проекта в порядке.

### Шаг 2: Импортируйте движок и создайте экземпляр

Создать движок так же просто, как вызвать его конструктор. Думайте о движке как о «мозге», который позже будет обрабатывать переданное ему изображение.

```python
# Step 2: Import and instantiate the OCR engine
from simple_ocr import OcrEngine

# Create a fresh engine instance – this allocates internal buffers
engine = OcrEngine()
```

Зачем создавать новый экземпляр каждый раз? Для изоляции. Свежий движок гарантирует, что никакое оставшееся состояние от предыдущего запуска не загрязнит текущее распознавание, что критично при пакетной обработке множества файлов.

### Шаг 3: Загрузите изображение, которое хотите обработать

Теперь мы действительно **загружаем изображение для OCR**. Метод `setImageFromFile` принимает путь к любому растровому изображению; мы укажем PNG под названием `mixed_doc.png`.

```python
# Step 3: Load the PNG image you want to read
image_path = "YOUR_DIRECTORY/mixed_doc.png"
engine.setImageFromFile(image_path)
```

Если файл не найден, `SimpleOCR` бросает понятный `FileNotFoundError`. Вы можете перехватить его, чтобы вывести дружелюбное сообщение об ошибке:

```python
try:
    engine.setImageFromFile(image_path)
except FileNotFoundError:
    print(f"❗️ Unable to locate '{image_path}'. Check the path and try again.")
    raise
```

### Шаг 4: Включите автоматическое определение языка

Большинство современных OCR‑движков поставляются с языковыми пакетами. Передавая `"multilingual"`, мы говорим движку «поймать» текст и автоматически подобрать нужную языковую модель. Это особенно удобно, когда ваш PNG содержит смесь английского и испанского, к примеру.

```python
# Step 4: Turn on auto‑language detection (covers all installed packs)
engine.setLanguage("multilingual")
```

Если язык известен заранее, вместо `"multilingual"` можно указать конкретный локаль, например `"eng"` или `"spa"`, чтобы ускорить обработку.

### Шаг 5: Запустите процесс распознавания

Здесь происходит основная работа. `recognize()` сканирует изображение, применяет сегментацию, запускает нейронную сеть и формирует внутренний буфер текста.

```python
# Step 5: Execute OCR – this may take a moment for large images
engine.recognize()
```

Внутри движок выполняет:

- **Предобработку** (выравнивание, бинаризация)  
- **Анализ макета** (определение колонок, таблиц)  
- **Классификацию символов** (с использованием модели глубокого обучения)  

Всё это абстрагировано, поэтому вам нужна лишь одна строка.

### Шаг 6: Получите и выведите распознанный текст

Наконец, мы получаем объект результата и извлекаем обычную строку. Это тот момент, когда вы действительно **извлекаете текст из изображения**.

```python
# Step 6: Get the OCR result and display the plain text
result = engine.getResult()
text = result.getText()
print("📝 Recognized Text:\n")
print(text)
```

**Ожидаемый вывод** (усечённый для краткости):

```
📝 Recognized Text:

Invoice #12345
Date: 2026‑03‑15
Total: $89.99
Thank you for your purchase!
```

Если изображение не содержит распознаваемых символов, `text` будет пустой строкой. Можно защититься от этого:

```python
if not text.strip():
    print("⚠️ No text detected – try a higher‑resolution image or adjust preprocessing.")
```

---

## Извлечение текста из изображения – обработка типичных краевых случаев

### Несколько языков в одном файле

Когда документ смешивает языки, настройка `"multilingual"` обычно справляется. Однако, если вы замечаете ошибки распознавания, можно вручную задать список резервных языков:

```python
engine.setLanguage(["eng", "spa", "fra"])  # English, Spanish, French
```

### Форматы, отличные от PNG

Хотя наш фокус — **распознавать текст из PNG**, `SimpleOCR` также принимает JPEG, BMP и TIFF. Просто измените расширение файла в `setImageFromFile`. Для стеков TIFF может потребоваться выбрать конкретную страницу:

```python
engine.setImageFromFile("scanned.tif", page=0)  # first page only
```

### Большие файлы и использование памяти

Если вы обрабатываете гигапиксельные сканы, подумайте о масштабировании перед OCR:

```python
from PIL import Image

with Image.open(image_path) as img:
    img.thumbnail((2000, 2000))  # keep aspect ratio, max 2000px
    img.save("temp_resized.png")
engine.setImageFromFile("temp_resized.png")
```

Изменение размера уменьшает нагрузку на память, сохраняя достаточную детализацию для точного распознавания.

### Отладка неудачных загрузок

Иногда изображение выглядит нормально, но повреждено внутри. Включите подробный лог, чтобы увидеть, что видит движок:

```python
engine.enableDebug(True)   # prints internal steps to stdout
engine.recognize()
```

---

## Полный готовый к запуску скрипт

Ниже представлен полный программный код, объединяющий все части. Скопируйте его в файл с именем `ocr_demo.py`, замените плейсхолдер `YOUR_DIRECTORY` на нужный путь и запустите `python ocr_demo.py`.

```python
# ocr_demo.py
# Full example showing how to use OCR to extract text from a PNG image.
# Requires: pip install simple-ocr pillow

from simple_ocr import OcrEngine
import os
from PIL import Image

def main():
    # 1️⃣ Create the OCR engine
    engine = OcrEngine()

    # 2️⃣ Define the image path – change this to your actual file location
    image_path = os.path.join("YOUR_DIRECTORY", "mixed_doc.png")

    # 3️⃣ Load the image (with a safety net for missing files)
    try:
        engine.setImageFromFile(image_path)
    except FileNotFoundError:
        print(f"❗️ Cannot find image at '{image_path}'. Exiting.")
        return

    # Optional: resize large images to keep memory usage low
    # (uncomment if you deal with huge scans)
    # with Image.open(image_path) as img:
    #     img.thumbnail((2000, 2000))
    #     resized_path = "temp_resized.png"
    #     img.save(resized_path)
    #     engine.setImageFromFile(resized_path)

    # 4️⃣ Enable automatic language detection (covers all installed packs)
    engine.setLanguage("multilingual")

    # 5️⃣ Run the OCR engine
    engine.recognize()

    # 6️⃣ Retrieve and print the recognized text
    result = engine.getResult()
    text = result.getText()

    if text.strip():
        print("\n📝 Recognized Text:\n")
        print(text)
    else:
        print("⚠️ No recognizable text found. Try a clearer image or adjust preprocessing.")

if __name__ == "__main__":
    main()
```

Запуск этого скрипта должен вывести текстовую версию того, что находится в `mixed_doc.png`. Не стесняйтесь заменить файл на любую другую картинку — **как извлекать текст** будет работать так же.

---

## Заключение

Мы только что прошли через **как использовать OCR** в Python для **извлечения текста из изображений**, сосредоточившись на **распознавании текста из PNG**‑ресурсов и практических шагах по **загрузке изображения для OCR**. Приведённый выше фрагмент — автономное решение: установить пакет, передать файл, включить многоязычное определение, запустить движок и получить результат.

Отсюда вы можете:

- Интегрировать скрипт в веб‑сервис, принимающий пользовательские загрузки.  
- Пакетно обрабатывать папку PDF‑файлов, конвертированных в PNG.  
- Добавить пост‑обработку (например, очистку с помощью regex, проверку орфографии) для повышения точности.

Помните, качество OCR зависит от чёткости изображения, правильных языковых пакетов и иногда небольшого предварительного преобразования — так что экспериментируйте.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}