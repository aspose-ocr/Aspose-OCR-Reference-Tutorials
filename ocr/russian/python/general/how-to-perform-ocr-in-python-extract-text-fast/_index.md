---
category: general
date: 2026-03-26
description: Узнайте, как выполнять OCR в Python и легко извлекать текст из изображения,
  читать текст со сканированного документа или извлекать текст из счета с помощью
  простого OcrEngine.
draft: false
keywords:
- how to perform OCR
- extract text from image
- read text from scan
- extract text from invoice
- how to use OCR
language: ru
og_description: Как выполнить OCR в Python? Это руководство покажет, как извлекать
  текст из изображения, читать текст со сканирования и получать текст из счета за
  считанные минуты.
og_title: Как выполнить OCR в Python – быстро извлекать текст
tags:
- OCR
- Python
- Image Processing
title: Как выполнить OCR в Python — быстро извлекать текст
url: /ru/python/general/how-to-perform-ocr-in-python-extract-text-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR в Python – Быстрое извлечение текста

Вы когда‑нибудь задумывались **как выполнять OCR** на отсканированном чеке или размытом PDF? Вы не одиноки. Во многих проектах необходимость **извлекать текст из изображения** появляется довольно рано, и обычный подход «вручную печатать всё» просто не масштабируется.  

В этом руководстве вы увидите полностью готовый к запуску пример, который показывает **как использовать OCR** для чтения текста со скана, извлечения данных из счета и даже автоматической коррекции наклона — всё это с помощью всего нескольких строк кода на Python.

## Что вы узнаете

* Точные зависимости и необходимые импорты.
* Как создать и настроить экземпляр `OcrEngine`.
* Способы **извлекать текст из изображения**, **читать текст со скана** и **извлекать текст из счета** с использованием одного и того же движка.
* Распространённые подводные камни (неправильный язык, отсутствующие файлы, большие изображения) и как их избежать.
* Ожидаемый вывод, чтобы вы могли убедиться, что OCR выполнен успешно.

Ссылки на внешнюю документацию не требуются — всё самодостаточно, так что вы можете скопировать‑вставить код и сразу увидеть результаты.

## Предварительные требования

Перед тем как погрузиться, убедитесь, что у вас есть:

* Установлен Python 3.8+ (пакет `ocr` работает с любой современной версией).
* Доступна библиотека `ocr` (`pip install ocr‑engine` — замените на фактическое название пакета, если оно отличается).
* Файл изображения, который вы хотите обработать — для демонстрации мы будем использовать `invoice.png`, расположенный в папке `YOUR_DIRECTORY`.

Вот и всё. Если у вас уже есть всё перечисленное, можно начинать.

## Шаг 1: Установить и импортировать модуль OCR

Во-первых, нам нужна библиотека OCR. Если вы ещё не установили её, выполните следующую команду в терминале:

```bash
pip install ocr-engine
```

Теперь импортируем модуль в наш скрипт.

```python
# Step 1: Import the OCR module
import ocr
```

> **Совет:** Держите виртуальное окружение в порядке; это предотвращает конфликты версий, когда вы позже добавляете другие пакеты для обработки изображений.

## Шаг 2: Создать и настроить OCR‑движок

Создание движка так же просто, как вызвать его конструктор, но истинная мощь заключается в правильной настройке. Мы установим язык на английский и включим автоматическую коррекцию наклона, что необходимо при работе со сканированными счетами, которые не идеально выровнены.

```python
# Step 2: Create an OCR engine instance
engine = ocr.OcrEngine()

# Step 3: Configure the engine – set language and enable automatic skew correction
engine.language = ocr.Language.English   # any supported language, e.g., Spanish, French
engine.auto_skew = True                 # fixes tilted scans automatically
```

Почему включать `auto_skew`? Многие сканеры создают изображения, отклонённые на несколько градусов. Без коррекции движок может пропустить символы, превратив полностью читаемый счет в набор бессмыслицы.

## Шаг 3: Выполнить OCR на целевом изображении

Теперь мы передаём файл изображения в движок. Метод `recognize_image` возвращает объект, содержащий исходный текст и оценки уверенности (если библиотека их предоставляет).

```python
# Step 4: Perform OCR on the target image
ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

Если вы работаете со сценарием **читать текст со скана**, просто замените путь на сканированный PDF, преобразованный в PNG или JPEG. Тот же вызов работает с любым форматом изображения, поддерживаемым базовой библиотекой.

## Шаг 4: Проверить и использовать извлечённый текст

Выведем необработанный вывод OCR. В реальном конвейере обработки счетов вы, вероятно, будете разбирать эту строку, извлекать позиции, итоги и даты, но пока быстрый взгляд подтвердит, что OCR выполнен успешно.

```python
# Step 5: Display the raw extracted text
print("Raw OCR text:\n", ocr_result.text)
```

**Ожидаемый вывод (усечённый для краткости):**

```
Raw OCR text:
 Invoice #12345
 Date: 2026‑03‑01
 Bill To: Acme Corp.
 Item          Qty   Price   Total
 ------------------------------------------------
 Widget A      10    5.00    50.00
 Widget B      5     12.00   60.00
 ------------------------------------------------
 Subtotal:                     110.00
 Tax (5%):                     5.50
 Grand Total:                  115.50
```

Если вывод выглядит искажённым, дважды проверьте, что изображение чёткое и что `engine.language` соответствует языку документа.

## Шаг 5: Обработка распространённых граничных случаев

### Большие изображения

Обработка скана размером 5000 × 5000 пикселей может требовать много памяти. Быстрый способ смягчить это — уменьшить масштаб изображения перед передачей в движок:

```python
from PIL import Image

def load_and_resize(path, max_dim=2000):
    img = Image.open(path)
    img.thumbnail((max_dim, max_dim), Image.ANTIALIAS)
    return img

scaled_image = load_and_resize("YOUR_DIRECTORY/invoice.png")
ocr_result = engine.recognize_image(scaled_image)
```

### Несколько языков

Если вам нужно **извлекать текст из изображения**, содержащего как английский, так и испанский, вы можете задать список языков:

```python
engine.language = [ocr.Language.English, ocr.Language.Spanish]
```

Движок попытается распознать символы из обоих наборов.

### Обработка ошибок

Никогда не предполагайте, что файл существует. Оберните вызов в блок try‑except, чтобы вывести дружелюбное сообщение:

```python
try:
    ocr_result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
    print("OCR succeeded!")
except FileNotFoundError:
    print("Error: The image file was not found. Check the path and try again.")
except ocr.OcrError as e:
    print(f"OCR failed with error: {e}")
```

## Визуальная справка

Ниже скриншот образца счета, который мы использовали в демонстрации. Обратите внимание на небольшое наклонение — именно то, что исправляет `auto_skew`.

![how to perform OCR on an invoice](/images/ocr-example.png)

*Alt text:* как выполнять OCR на изображении счета, показывающем автоматическую коррекцию наклона.

## Полный, исполняемый пример

Объединив всё вместе, представляем единый скрипт, который можно запустить из командной строки. Он охватывает установку, настройку, обработку ошибок и простой шаг пост‑обработки, записывающий извлечённый текст в файл `output.txt`.

```python
# full_ocr_demo.py
# -------------------------------------------------
# Demonstrates how to perform OCR, extract text from image,
# read text from scan, and extract text from invoice.
# -------------------------------------------------

import ocr
from pathlib import Path

def main(image_path: str, output_path: str = "output.txt"):
    # Create and configure the engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.English
    engine.auto_skew = True

    # Verify the image exists
    if not Path(image_path).is_file():
        print(f"❌  Image not found: {image_path}")
        return

    # Run OCR
    try:
        result = engine.recognize_image(image_path)
    except ocr.OcrError as err:
        print(f"❌  OCR failed: {err}")
        return

    # Output the raw text
    print("✅  OCR completed. Raw text:")
    print(result.text)

    # Save to a text file for later processing
    Path(output_path).write_text(result.text, encoding="utf-8")
    print(f"💾  Text saved to {output_path}")

if __name__ == "__main__":
    # Replace with your actual file location
    main("YOUR_DIRECTORY/invoice.png")
```

Запуск `python full_ocr_demo.py` выведет извлечённый текст в консоль и сохранит его в `output.txt`. Оттуда вы можете применять регулярные выражения, CSV‑записыватели или любую другую логику, необходимую для автоматизации **извлечения текста из счета**.

## Заключение

Теперь у вас есть надёжное, сквозное решение для **как выполнять OCR** в Python. Создавая `OcrEngine`, настраивая язык и коррекцию наклона, а также обрабатывая несколько практических граничных случаев, вы можете надёжно **извлекать текст из изображения**, **читать текст со скана** и **извлекать текст из счета** без необходимости искать информацию в разрозненной документации.

Что дальше? Попробуйте обработать пакет файлов в цикле, поэкспериментировать с разными языками или подключить вывод к библиотеке генерации PDF, чтобы создавать поисковые PDF. Возможности безграничны, а код, который вы только что увидели, — надёжная отправная точка.

Есть вопросы по конкретному формату файла или нужна помощь в настройке порогов уверенности? Оставьте комментарий ниже — будем рады помочь вам доработать ваш OCR‑конвейер!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}