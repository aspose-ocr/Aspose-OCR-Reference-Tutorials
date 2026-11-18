---
category: general
date: 2026-03-26
description: 'Учебник по OCR на Python: узнайте, как извлекать текст из изображения,
  загружать изображение для OCR и распознавать текст с чека с помощью Aspose OCR за
  несколько шагов.'
draft: false
keywords:
- python ocr tutorial
- extract text from image
- load image for ocr
- perform ocr in python
- recognize text from receipt
language: ru
og_description: 'Учебник по OCR на Python: быстро научитесь извлекать текст из изображения,
  загружать изображение для OCR и распознавать текст с чека с помощью Aspise OCR.'
og_title: Учебник по OCR в Python – извлечение текста из изображения
tags:
- OCR
- Aspose
- Python
title: Учебник по OCR на Python – извлечение текста из изображения с помощью Aspose
url: /ru/python-java/general/python-ocr-tutorial-extract-text-from-image-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR tutorial – Извлечение текста из изображения с Aspose

Задумывались когда‑нибудь, как извлечь текст из размытого чека или отсканированной формы, не тратя часы на написание собственных регулярных выражений? Вы не одиноки. В этом **python ocr tutorial** мы пройдём процесс загрузки изображения для OCR, выполнения OCR в Python и, наконец, распознавания текста из файлов чеков с использованием библиотеки Aspose OCR.  

К концу этого руководства у вас будет готовый к запуску скрипт, который читает любой поддерживаемый формат изображения, извлекает текстовое содержимое и выводит его в консоль. Никаких внешних сервисов, никаких API‑ключей — только чистый Python и мощный OCR‑движок.  

## Что понадобится

- Python 3.8 или новее (код использует подсказки типов, поэтому лучше использовать современный интерпретатор)
- Пакет `asposeocrjava`, установленный через `pip install aspose-ocr`
- Пример изображения — например `receipt_noisy.jpg`, содержащий типичный чек магазина
- (Optional) Виртуальное окружение для аккуратного управления зависимостями

Если все пункты выполнены, мы можем сразу перейти к коду.  

## Шаг 1: Установить и импортировать классы Aspose OCR

Сначала убедитесь, что пакет Aspose OCR доступен. Затем импортируйте необходимые классы.

```python
# Install the package (run once)
# pip install aspose-ocr

# Import the required Aspose OCR modules
import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult
```

**Почему это важно:** Импорт только необходимых символов поддерживает чистоту пространства имён и сигнализирует интерпретатору, какие части библиотеки действительно используются. Это также сокращает последующие строки кода, делая руководство проще для восприятия.

> **Совет:** Если вы используете Jupyter notebook, добавьте перед строкой установки `!`, чтобы выполнить её в ячейке.

## Шаг 2: Создать OCR‑движок и включить режим Deep‑Learning

Aspose предлагает несколько режимов движка. Для большинства реальных чеков модель deep‑learning обеспечивает наибольшую точность, особенно на шумных сканах.

```python
# Initialise the OCR engine
ocr_engine = OcrEngine()

# Switch to deep‑learning mode for better accuracy on complex images
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
```

**Почему deep‑learning?** Традиционный OCR, основанный на правилах, может давать сбои при низком контрасте или искажённых символах. Модель deep‑learning, обученная на миллионах глифов, лучше адаптируется к вариациям — именно то, что нужно, когда вы *perform OCR in Python* на чеках, снятых камерой телефона.

## Шаг 3: Загрузить изображение для OCR

Теперь мы действительно **load image for OCR**. Aspose.Imaging поддерживает PNG, JPEG, BMP, TIFF и другие форматы, так что вы можете указать практически любое изображение документа.

```python
# Load the image (replace the path with your own file)
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/receipt_noisy.jpg")

# Attach the image to the OCR engine
ocr_engine.set_image(input_image)
```

**Распространённая ошибка:** Если забыть установить изображение в движок, во время выполнения возникнет `NullReferenceException`. Всегда вызывайте `set_image` после загрузки файла.

## Шаг 4: Выполнить OCR и извлечь текст

С готовым движком и прикреплённым изображением мы наконец можем **perform OCR in Python** и получить текстовый результат.

```python
# Run the recognition process
ocr_result: OcrResult = ocr_engine.recognize()

# Extract plain text from the result object
recognized_text = ocr_result.get_text()
```

Метод `recognize()` возвращает объект `OcrResult`, который содержит не только исходный текст, но и оценки уверенности, ограничивающие рамки и информацию о языке. Для быстрого случая **extract text from image** нам нужен только `get_text()`.

## Шаг 5: Показать распознанный текст

Посмотрим, что движок действительно прочитал из чека.

```python
print("Recognized text:\n", recognized_text)
```

Типичный вывод выглядит так:

```
Recognized text:
   Store XYZ
   04/26/2026  14:32
   Item A   2.99
   Item B   5.49
   TOTAL    8.48
   THANK YOU!
```

Если вывод содержит искажённые символы, рассмотрите предобработку изображения (например, увеличение контраста или применение фильтра выравнивания) перед загрузкой в OCR‑движок. Aspose.Imaging предоставляет полный набор инструментов улучшения изображения, которые можно комбинировать.

## Обработка граничных случаев и советы для повышения точности

### 1. Работа с чрезвычайно шумными чеками
Если чек сильно размазан, вы можете переключиться в режим `OcrEngineMode.HIGH_SPEED` для более быстрой, хотя и менее точной, обработки, а затем выполнить второй проход в `DEEP_LEARNING` на очищенном изображении.

```python
ocr_engine.set_engine_mode(OcrEngineMode.HIGH_SPEED)
# ... run first pass, then...
ocr_engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)
# ... run second pass on the same image
```

### 2. Указание языка
По умолчанию Aspose пытается автоматически определить язык. Для английских чеков вы можете зафиксировать его:

```python
ocr_engine.set_language("eng")
```

### 3. Управление памятью
При обработке большого количества изображений в цикле явно освобождайте ресурсы:

```python
input_image.dispose()
ocr_engine.dispose()
```

### 4. Сохранение результатов OCR в файл
Иногда необходимо сохранить извлечённый текст для последующего анализа.

```python
with open("receipt_output.txt", "w", encoding="utf-8") as f:
    f.write(recognized_text)
```

## Полный рабочий пример

Ниже представлен полный скрипт, связывающий всё вместе. Скопируйте его в файл с именем `receipt_ocr.py`, укажите путь к изображению и запустите `python receipt_ocr.py`.

```python
# receipt_ocr.py
# -------------------------------------------------
# Complete Python OCR tutorial using Aspose OCR
# -------------------------------------------------

# 1️⃣ Install the package (run once):
# pip install aspose-ocr

import asposeocrjava as ocr
from asposeocrjava import OcrEngineMode, OcrEngine, OcrResult

def main():
    # 2️⃣ Initialise engine in deep‑learning mode
    engine = OcrEngine()
    engine.set_engine_mode(OcrEngineMode.DEEP_LEARNING)

    # 3️⃣ Load your receipt image
    image_path = "YOUR_DIRECTORY/receipt_noisy.jpg"   # <-- change this
    img = ocr.Imaging.Image.load(image_path)
    engine.set_image(img)

    # 4️⃣ Recognise text
    result: OcrResult = engine.recognize()
    text = result.get_text()

    # 5️⃣ Output the result
    print("=== Recognized text from receipt ===")
    print(text)

    # Optional: write to a file
    with open("receipt_output.txt", "w", encoding="utf-8") as out_file:
        out_file.write(text)

    # Clean up resources
    img.dispose()
    engine.dispose()

if __name__ == "__main__":
    main()
```

Запуск скрипта должен отобразить содержимое чека в консоли и также создать файл `receipt_output.txt` с теми же данными.

![Python OCR tutorial – пример вывода чека](https://example.com/receipt_output.png "пример из руководства python ocr")

*Текст alt изображения:* **python ocr tutorial – пример вывода чека**

## Итоги и дальнейшие шаги

Мы только что прошли через **python ocr tutorial**, который показывает, как **load image for OCR**, **perform OCR in Python** и, наконец, **recognize text from receipt** файлы с использованием Aspose. Ключевые выводы:

- Выберите правильный режим движка (deep‑learning для точности)
- Всегда прикрепляйте изображение перед вызовом `recognize()`
- Используйте объект `OcrResult`, чтобы получить чистый текст, затем сохраняйте или обрабатывайте его по необходимости

Что дальше? Рассмотрите возможность последовательного применения фильтров Aspose Imaging для улучшения сканов с низким контрастом или интеграцию скрипта в Flask API, чтобы можно было загружать чеки через веб‑форму. Вы также можете исследовать экспорт данных OCR в CSV для автоматизации бухгалтерии.

Есть вопросы по работе с многостраничными PDF или нелатинскими скриптами? Оставьте комментарий — с радостью помогу!  

**Готовы вывести автоматизацию документов на новый уровень?** Возьмите код, поэкспериментируйте с разными изображениями и позвольте OCR‑движку выполнить тяжёлую работу. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}