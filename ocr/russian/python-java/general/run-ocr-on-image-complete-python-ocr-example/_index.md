---
category: general
date: 2026-03-18
description: Быстро выполняйте OCR изображения с помощью Python. Узнайте, как распознавать
  текст из PNG, загружать изображение для OCR и извлекать слова из изображения в пошаговом
  руководстве.
draft: false
keywords:
- run OCR on image
- recognize text from png
- python OCR example
- extract words from image
- load image for OCR
language: ru
og_description: Запустите OCR на изображении с помощью Python. Этот учебник показывает,
  как распознавать текст из PNG, загружать изображение для OCR и извлекать слова из
  изображения с полным примером кода.
og_title: Запуск OCR на изображении – Руководство по Python
tags:
- OCR
- Python
- Image Processing
title: Запустить OCR на изображении – Полный пример OCR на Python
url: /ru/python-java/general/run-ocr-on-image-complete-python-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на изображении – Полный пример на Python

Когда‑то вам нужно **запустить OCR на изображении**, но вы не знали, с чего начать? Вы не одиноки; многие разработчики сталкиваются с этим, когда впервые пытаются извлечь текст из отсканированных документов. В этом руководстве мы пройдемся по **примеру OCR на Python**, который позволяет **распознавать текст из PNG**‑файлов, **загружать изображение для OCR** и **извлекать слова из изображения** с оценкой уверенности — всё в нескольких строках кода.

Мы расскажем обо всём, что необходимо: о требуемой библиотеке, как настроить движок, почему каждый шаг важен и как выглядит вывод. К концу вы сможете вставить этот фрагмент в свой проект и мгновенно получать текст из любого изображения. Без лишних слов, только практичное, готовое к запуску решение.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

- Python 3.8 или новее  
- Пакет `ocrengine` (или любая библиотека, предоставляющая класс `OcrEngine`). Установить его можно командой `pip install ocrengine` – при необходимости замените название на другое OCR‑решение, например `pytesseract`.  
- Файл изображения (PNG, JPG и т.д.), который вы хотите обработать – в этом руководстве мы будем использовать `invoice.png`.  

Это всё. Никаких тяжёлых зависимостей, внешних сервисов, только чистый Python.

![run OCR on image example showing a scanned invoice](/images/run-ocr-on-image.png)

*Alt text: пример запуска OCR на изображении – сканированный счёт обрабатывается*

## Шаг 1 – Установка и импорт OCR‑библиотеки

Сначала загрузим OCR‑движок в наше окружение и импортируем его. Если вы используете гипотетический пакет `ocrengine`, импорт выглядит так:

```python
# Install the package (run once in your terminal)
# pip install ocrengine

# Import the OCR engine class
from ocrengine import OcrEngine
```

**Почему это важно:** Импорт правильного класса даёт доступ к методам, которые мы будем вызывать позже, например `setImageFromFile` и `recognize`. Если пропустить этот шаг, Python выдаст `ModuleNotFoundError`, и вы не сможете даже загрузить изображение.

## Шаг 2 – Создание экземпляра OCR‑движка

Теперь, когда библиотека готова, нам нужен объект‑движок, который будет хранить конфигурацию и состояние процесса распознавания.

```python
# Step 2: Create an OCR engine instance
ocr_engine = OcrEngine()
```

*Совет:* Некоторые OCR‑движки позволяют настроить языковые модели или DPI‑параметры на этом этапе. Для базового **python OCR example** значения по умолчанию подходят, но если вы работаете с низкокачественными сканами, стоит их изменить.

## Шаг 3 – Загрузка изображения для обработки

Следующий логичный шаг – **load image for OCR**. Укажите движку путь к PNG‑файлу (или к любому поддерживаемому формату), который хотите проанализировать.

```python
# Step 3: Load the image you want to process
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice.png")
```

**Что происходит «под капотом»?** Движок читает пиксельные данные, преобразует их в формат, понятный алгоритму распознавания, и сохраняет их внутри. Если путь к файлу неверный, вы получите `FileNotFoundError`, поэтому проверьте, что изображение действительно существует.

## Шаг 4 – Запуск алгоритма распознавания

После загрузки изображения мы наконец **run OCR on image**, чтобы извлечь текстовое содержимое.

```python
# Step 4: Run the recognition algorithm to obtain results
ocr_result = ocr_engine.recognize()
```

На этом этапе движок сканирует битмап, применяет сопоставление шаблонов и возвращает объект, содержащий каждое найденное слово, строку и метрику уверенности.

## Шаг 5 – Перебор распознанных слов и вывод уверенности

Самая полезная часть любого OCR‑процесса – увидеть **confidence** для каждого извлечённого токена. Это показывает, насколько уверенно движок определил каждое слово, позволяя отфильтровать результаты с низкой уверенностью при необходимости.

```python
# Step 5: Iterate over each recognized word and display its text with confidence
for recognized_word in ocr_result.getWords():
    word_text = recognized_word.getText()
    confidence = recognized_word.getConfidence()   # 0‑100%
    print(f"Word: '{word_text}' – confidence: {confidence}%")
```

**Ожидаемый вывод** (пример):

```
Word: 'Invoice' – confidence: 98%
Word: 'Number' – confidence: 95%
Word: ':' – confidence: 92%
Word: '2023-07-15' – confidence: 97%
Word: 'Total' – confidence: 96%
Word: ':' – confidence: 93%
Word: '$' – confidence: 88%
Word: '1,250.00' – confidence: 94%
```

Теперь вы точно видите, **какие слова были извлечены из изображения** и насколько надёжно каждое обнаружение. Это ядро любой **extract words from image**‑конвейера.

## Обработка распространённых граничных случаев

### Что делать, если изображение в градациях серого?

Некоторые OCR‑движки работают лучше с цветными изображениями. Если вы замечаете низкую уверенность в целом, попробуйте преобразовать PNG в более контрастную черно‑белую версию перед передачей в движок. Для этого поможет Pillow:

```python
from PIL import Image, ImageOps

img = Image.open("YOUR_DIRECTORY/invoice.png")
bw = ImageOps.grayscale(img).point(lambda x: 0 if x < 128 else 255, '1')
bw.save("YOUR_DIRECTORY/invoice_bw.png")
ocr_engine.setImageFromFile("YOUR_DIRECTORY/invoice_bw.png")
```

### Работа с несколькими языками

Если ваш документ содержит и английский, и испанский, вам понадобится **recognize text from PNG** с использованием многоязычной модели. Большинство движков позволяют задать список языков при инициализации:

```python
ocr_engine = OcrEngine(languages=["eng", "spa"])
```

### Фильтрация слов с низкой уверенностью

Иногда нужны только слова с уверенностью выше, скажем, 90 %. Быстрый фильтр выглядит так:

```python
high_confidence_words = [
    w.getText()
    for w in ocr_result.getWords()
    if w.getConfidence() >= 90
]
print(high_confidence_words)
```

## Полный готовый к запуску скрипт

Объединив всё вместе, получаем единый скрипт, который можно скопировать‑вставить и запустить сразу (только замените путь к вашему PNG).

```python
# run_ocr_on_image.py
# -------------------------------------------------
# Complete Python OCR example: load image for OCR,
# run OCR on image, and extract words from image.
# -------------------------------------------------

# Install the library first:
# pip install ocrengine pillow   # pillow only needed for optional preprocessing

from ocrengine import OcrEngine

def main():
    # 1️⃣ Create the OCR engine
    ocr_engine = OcrEngine()

    # 2️⃣ Load the target PNG (replace with your own file)
    image_path = "YOUR_DIRECTORY/invoice.png"
    ocr_engine.setImageFromFile(image_path)

    # 3️⃣ Run recognition
    ocr_result = ocr_engine.recognize()

    # 4️⃣ Print each word with its confidence
    print("\n--- OCR Results ---")
    for word in ocr_result.getWords():
        text = word.getText()
        conf = word.getConfidence()
        print(f"Word: '{text}' – confidence: {conf}%")

if __name__ == "__main__":
    main()
```

Запустите его командой:

```bash
python run_ocr_on_image.py
```

Вы увидите список слов и процентные значения уверенности, выведенные в консоль, точно как показано выше.

## Часто задаваемые вопросы

**Работает ли это с JPG или TIFF?**  
Конечно. Метод `setImageFromFile` принимает любой формат, который может декодировать базовая библиотека, так что вы можете **run OCR on image** файлы типа JPG, TIFF, BMP и т.д.

**Можно ли обрабатывать несколько изображений в цикле?**  
Да. Оберните шаги загрузки и распознавания в `for`‑цикл по списку путей к файлам. Не забудьте переинициализировать движок, если библиотека требует новый экземпляр для каждого изображения.

**А если нужен весь текст в одной строке, а не по словам?**  
Большинство объектов результата OCR предоставляют метод `getText()`, который возвращает весь документ целиком. Пример:

```python
full_text = ocr_result.getText()
print(full_text)
```

## Следующие шаги и смежные темы

Теперь, когда вы знаете, как **run OCR on image**, можете изучить:

- **Post‑processing**: использовать регулярные выражения для очистки дат, сумм или идентификаторов, извлечённых из счетов.  
- **Batch processing**: комбинировать скрипт с `os.listdir()` для обработки целых папок отсканированных документов.  
- **Alternative libraries**: `pytesseract` – популярный open‑source вариант; workflow почти такой же — просто замените вызовы движка.  
- **Exporting results**: записывать извлечённые слова и оценки уверенности в CSV для дальнейшего анализа.

Каждое из этих расширений опирается на фундамент, заложенный здесь, позволяя превращать сырые OCR‑данные в полезную информацию.

---

### TL;DR

Мы представили лаконичный **python OCR example**, демонстрирующий, как **load image for OCR**, **run OCR on image** и **extract words from image**, выводя при этом оценки уверенности. Полный скрипт готов к запуску, и теперь вы знаете, как адаптировать его под любой проект, требующий **recognize text from PNG** (или других форматов). Попробуйте, настройте пороги уверенности и наблюдайте, как ваши приложения становятся «текстово‑осведомлёнными» за считанные минуты. Приятного кодинга!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}