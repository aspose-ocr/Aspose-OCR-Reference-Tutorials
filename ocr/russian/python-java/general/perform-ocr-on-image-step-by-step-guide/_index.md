---
category: general
date: 2026-03-18
description: Выполняйте OCR на изображении, чтобы быстро извлекать текст. Узнайте,
  как загрузить изображение для OCR, создать OCR‑движок и повысить точность распознавания
  с помощью языковых настроек.
draft: false
keywords:
- perform OCR on image
- extract text from image
- improve OCR accuracy
- load image for OCR
- create OCR engine
language: ru
og_description: Выполните OCR изображения с помощью этого подробного руководства.
  Узнайте, как загрузить изображение для OCR, создать OCR‑движок и улучшить точность
  OCR для надёжного извлечения текста.
og_title: Выполнить OCR на изображении — Полный учебник по программированию
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Выполните OCR на изображении – пошаговое руководство
url: /ru/python-java/general/perform-ocr-on-image-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Выполнение OCR на изображении – Полный программный учебник

Когда‑то вам нужно **выполнить OCR на изображении**, но вы не знали, какую библиотеку выбрать или как получить надёжные результаты? Вы не одиноки. В этом руководстве мы пройдём всё, что нужно для **извлечения текста из изображения**, от загрузки картинки до настройки языковых параметров, чтобы вы могли **повысить точность OCR** на каждом этапе.

Мы расскажем, как **загрузить изображение для OCR**, как **создать OCR‑движок**, и почему каждое из этих настроек важно. В конце у вас будет готовый к запуску скрипт, выводящий распознанный текст, и вы поймёте «почему» каждой строки — без расплывчатых «см. документацию» обходных путей. Поехали.

## Что понадобится

- Python 3.8+ (код использует f‑строки и подсказки типов)
- Гипотетический пакет `ocr_lib` — установить через `pip install ocr_lib`
- Файл изображения с чётким печатным текстом (например, `lab_report.png`)
- Любой простой текстовый редактор или IDE (VS Code, PyCharm, что угодно)

Если всё уже есть — отлично, вы готовы. Если нет, скачайте Python с python.org и выполните pip‑команду; это займет минуту.

![perform OCR on image example](/images/ocr-example.png)

*Alt text: perform OCR on image – пример вывода с извлечённым текстом.*

## Шаг 1: Создать OCR‑движок – Как **create OCR engine** в Python

Прежде чем начнётся распознавание, библиотеке нужен объект‑движок, который хранит конфигурацию и состояние выполнения. Думайте о движке как о мозге операции.

```python
# step_1_create_engine.py
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    """
    Initialize and return a fresh OcrEngine instance.
    Creating the engine once and reusing it is more efficient than
    instantiating it inside a loop.
    """
    engine = OcrEngine()
    return engine
```

**Почему это важно:** Раннее создание движка позволяет позже добавить языковые параметры и кэшировать внутренние модели для более быстрых последующих вызовов.

## Шаг 2: Загрузить изображение для OCR – Правильный способ **load image for OCR**

Теперь, когда у нас есть движок, нужно дать ему что‑то для чтения. Метод `setImageFromFile` принимает путь в файловой системе; путь может быть абсолютным или относительным к рабочей директории скрипта.

```python
# step_2_load_image.py
def load_image(engine: OcrEngine, image_path: str) -> None:
    """
    Attach an image file to the engine.
    Raises FileNotFoundError if the file does not exist.
    """
    engine.setImageFromFile(image_path)
```

**Совет:** Используйте абсолютный путь или `os.path.join`, чтобы избежать неожиданного «файл не найден», когда скрипт запускается из другой папки.

```python
import os

image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
load_image(my_engine, image_file)
```

## Шаг 3: Повысить точность OCR – Настройка **language options** для **improve OCR accuracy**

Базовый OCR работает, но специализированные словари (например, лабораторный жаргон) часто сбивают его с толку. Передавая пользовательский словарь и чёрный список, вы уменьшаете ошибки, такие как путаница «0» и «O».

```python
# step_3_language_options.py
def configure_language(engine: OcrEngine) -> None:
    """
    Set up language options to help the engine recognize domain‑specific terms
    and ignore characters that are frequently misread.
    """
    language_opts = LanguageOptions()
    # Add terms that appear often in laboratory reports
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    # Blacklist characters that cause confusion
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)
```

**Почему это помогает:** Словарь сообщает модели OCR, что «HPLC» — допустимый токен, не позволяя разбивать слово на бессмыслицу. Чёрный список указывает модели рассматривать неоднозначные символы как шум, что напрямую **повышает точность OCR**.

## Шаг 4: Выполнить OCR на изображении – Основной вызов **perform OCR on image**

С движком, подготовленным и привязанным изображением, пришло время действительно распознать текст. Этот шаг возвращает объект `OcrResult`, из которого можно получить сырой текст, оценки уверенности или ограничивающие рамки.

```python
# step_4_recognize.py
def recognize_text(engine: OcrEngine) -> OcrResult:
    """
    Run the OCR process. This may take a few seconds depending on image size.
    Returns an OcrResult that contains the extracted string and metadata.
    """
    result = engine.recognize()
    return result
```

Если изображение размыто, вы увидите более низкие значения уверенности в результате. Это сигнал к предварительной обработке изображения (например, увеличению контрастности) перед передачей его в движок.

## Шаг 5: Извлечь текст из изображения – Получение окончательной строки

Наконец, мы запрашиваем у `OcrResult` его текстовое представление. Метод `getText()` возвращает обычную строку, готовую к дальнейшей обработке (сохранению в файл, загрузке в базу данных и т.д.).

```python
# step_5_output.py
def print_result(result: OcrResult) -> None:
    """
    Output the recognized text to the console.
    You could also write it to a file with open('output.txt', 'w') …
    """
    extracted = result.getText()
    print("=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===")
```

**Ожидаемый вывод:** Предположим, `lab_report.png` содержит простую таблицу, вы можете увидеть что‑то вроде:

```
=== OCR Output Start ===
Sample ID: 00123
Method: HPLC
Result: 5.67 mg/L
=== OCR Output End ===
```

Таким образом, часть **extract text from image** завершена.

## Полный рабочий пример – Собираем всё вместе

Ниже один скрипт, который соединяет все кусочки из предыдущих разделов. Скопируйте его в `run_ocr.py` и выполните `python run_ocr.py`.

```python
# run_ocr.py
import os
from ocr_lib import OcrEngine, LanguageOptions, OcrResult

def build_engine() -> OcrEngine:
    engine = OcrEngine()
    return engine

def load_image(engine: OcrEngine, image_path: str) -> None:
    if not os.path.isfile(image_path):
        raise FileNotFoundError(f"Image not found: {image_path}")
    engine.setImageFromFile(image_path)

def configure_language(engine: OcrEngine) -> None:
    language_opts = LanguageOptions()
    language_opts.setDictionary(["HPLC", "UV‑VIS", "chromatogram"])
    language_opts.setBlacklist(["0", "O", "l", "1"])
    engine.setLanguageOptions(language_opts)

def recognize_text(engine: OcrEngine) -> OcrResult:
    return engine.recognize()

def print_result(result: OcrResult) -> None:
    extracted = result.getText()
    print("\n=== OCR Output Start ===")
    print(extracted)
    print("=== OCR Output End ===\n")

def main() -> None:
    # 1️⃣ Create the OCR engine
    ocr_engine = build_engine()

    # 2️⃣ Load the image you want to process
    image_file = os.path.join("YOUR_DIRECTORY", "lab_report.png")
    load_image(ocr_engine, image_file)

    # 3️⃣ Apply language tweaks to **improve OCR accuracy**
    configure_language(ocr_engine)

    # 4️⃣ **Perform OCR on image** – this is the heavy lifting
    ocr_result = recognize_text(ocr_engine)

    # 5️⃣ **Extract text from image** and show it
    print_result(ocr_result)

if __name__ == "__main__":
    main()
```

### Быстрый чек‑лист проверки

| ✅ | Пункт |
|---|------|
| ✔️ | Движок создан (`create OCR engine`) |
| ✔️ | Изображение загружено (`load image for OCR`) |
| ✔️ | Языковые параметры установлены (`improve OCR accuracy`) |
| ✔️ | OCR выполнен (`perform OCR on image`) |
| ✔️ | Текст извлечён (`extract text from image`) |

Запустите скрипт и смотрите консоль. Если вы увидите блок «OCR Output» с содержимым вашего отчёта, вы успешно **выполнили OCR на изображении**.

## Частые ошибки и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **Размытый ввод** | Модель OCR не может различить символы | Предобработайте с OpenCV: `cv2.GaussianBlur` или увеличьте DPI |
| **Неправильный язык** | Язык по умолчанию может быть не английским | Вызовите `engine.setLanguage("eng")` перед `recognize()` |
| **Отсутствие терминов в словаре** | Специфические слова искажаются | Добавьте их через `setDictionary`, как показано в Шаге 3 |
| **Blacklisted characters cause |  |  |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}