---
category: general
date: 2026-06-25
description: Как использовать OCR в Python — узнайте, как загрузить изображение для
  OCR, распознать текст в области и быстро извлечь текст из области.
draft: false
keywords:
- how to use ocr
- load image for ocr
- recognize text in region
- how to extract region text
language: ru
og_description: Как использовать OCR в Python – пошаговое руководство по загрузке
  изображения, распознаванию текста в определённом регионе и извлечению номера счета.
og_title: 'Как использовать OCR в Python: загрузить изображение и извлечь текст из
  области'
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: How to use OCR in Python – learn how to load image for OCR, recognize
    text in region, and extract region text quickly.
  headline: 'How to Use OCR Python: Load Image and Extract Region Text'
  type: TechArticle
- questions:
  - answer: Most modern OCR engines handle a wide range of fonts, but you can boost
      accuracy by training a custom language model or pre‑processing the image (e.g.,
      applying a threshold filter).
    question: What if the invoice number is printed in a fancy font?
  - answer: Absolutely. Define a list of `Rectangle` objects—one per field—and loop
      over them, storing each result in a dictionary.
    question: Can I extract multiple fields at once?
  - answer: 'Convert each page to an image first (using `pdf2image` or similar), then
      apply the same region‑based extraction per page. --- ## Wrapping Up In this
      tutorial we covered **how to use OCR** in Python to load an image, recognize
      text in a specific region, and extract that region’s text—perfect for pull'
    question: Does this work on multi‑page PDFs?
  type: FAQPage
tags:
- OCR
- Python
- Image Processing
title: 'Как использовать OCR в Python: загрузить изображение и извлечь текст из области'
url: /ru/python-java/general/how-to-use-ocr-python-load-image-and-extract-region-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR Python: загрузить изображение и извлечь текст из области

**How to use OCR in Python** проще, чем вы думаете. Когда‑нибудь вы смотрели на отсканированный счет и задавались вопросом, как извлечь только номер счета, не разбирая всю страницу? Вы не одиноки — многие разработчики сталкиваются с этой проблемой, когда впервые пробуют оптическое распознавание символов. В этом руководстве мы пройдем загрузку изображения для OCR, определение прямоугольника, распознавание текста в этой области и, наконец, извлечение текста области. К концу вы получите готовый к запуску скрипт, который изолирует любой нужный вам фрагмент текста.

> *Pro tip:* Если вы работаете с PDF, сначала конвертируйте каждую страницу в изображение — большинство OCR‑библиотек лучше работают с PNG/JPEG.

## Что понадобится

- Python 3.8+ (рекомендуется последняя стабильная версия)  
- OCR‑библиотека, предоставляющая класс `OcrEngine` (например, **ocr** из `pip install ocr-lib`)  
- Пример изображения — здесь мы будем использовать `invoice.png`, размещённый в папке, которой вы управляете  
- Базовое знакомство с прямоугольниками (x, y, width, height)  

Никаких тяжёлых зависимостей, GPU не требуется — только обычная работа на CPU, что делает решение портируемым.

---

## Как использовать OCR: инициализация движка (Шаг 1)

Прежде чем можно будет читать любой текст, вам нужен экземпляр OCR‑движка. Считайте его мозгом, который будет анализировать пиксельные шаблоны.

```python
import ocr               # The OCR library
from ocr import Rectangle  # Helper for defining regions

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

*Почему это важно:* Инициализация движка загружает языковые модели и задаёт конфигурации по умолчанию. Пропуск этого шага вызовет исключение в момент вызова `recognize_region`.

## Загрузка изображения для OCR (Шаг 2)

Теперь, когда движок готов, мы передаём ему изображение. Метод `Image.load` библиотеки обрабатывает распространённые форматы и нормализует bitmap.

```python
# Step 2: Load the image containing the invoice
image_path = "YOUR_DIRECTORY/invoice.png"
image = ocr.Image.load(image_path)
```

Если файл не найден, Python выбросит `FileNotFoundError`. Убедитесь, что путь абсолютный или относительный к рабочему каталогу вашего скрипта.  

*Edge case:* Некоторые OCR‑движки ожидают изображение в градациях серого. Если вы замечаете низкую точность, сначала конвертируйте изображение:

```python
image = image.convert("L")  # L = 8‑bit pixels, black and white
```

---

## Распознавание текста в области (Шаг 3)

Определение области — это момент, когда вы указываете движку, *где* искать. `Rectangle` принимает значения с плавающей точкой для субпиксельной точности, что удобно при работе с высокоразрешающими сканами.

```python
# Step 3: Define the rectangle that encloses the invoice number
invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
```

- **x, y** – координаты левого верхнего угла прямоугольника (в пикселях)  
- **width, height** – размеры коробки  

Возможно, вы задаётесь вопросом, как найти эти числа. Быстрый способ — открыть изображение в любом редакторе (например, GIMP или Paint.NET) и с помощью инструмента выделения прочитать координаты.  

*Почему не просто распознавать всю страницу?* Ограничение области уменьшает шум, ускоряет обработку и значительно повышает точность для небольших полей, таких как номера счетов.

## Как извлечь текст из области (Шаг 4)

С установленной областью попросите движок распознать только этот фрагмент. Объект результата содержит исходный текст и оценки уверенности.

```python
# Step 4: Recognize text only within the specified region
region_result = engine.recognize_region(image, invoice_rect)
```

Если OCR‑движок поддерживает несколько языков, вы можете передать необязательный код языка:

```python
region_result = engine.recognize_region(image, invoice_rect, lang="eng")
```

*Распространённая ошибка:* Некоторые движки возвращают список слов вместо одной строки. В таких случаях их нужно конкатенировать:

```python
text = " ".join(region_result.words)
```

## Вывод извлечённого номера счета (Шаг 5)

Наконец, выведите — или сохраните — извлечённый текст. Вы также можете пост‑обработать строку, удалив лишние пробелы или нечисловые символы.

```python
# Step 5: Output the extracted invoice number
raw_text = region_result.text.strip()
# Optional: keep only digits (most invoice numbers are numeric)
invoice_number = "".join(filter(str.isdigit, raw_text))

print("Invoice number:", invoice_number)
```

Запуск скрипта с правильно выровненным прямоугольником должен дать что‑то вроде:

```
Invoice number: 20231578
```

Если вы получаете мусорные символы, дважды проверьте координаты прямоугольника или рассмотрите возможность увеличения разрешения изображения.

---

## Полный рабочий пример

Собрав всё вместе, представляем автономный скрипт, который вы можете скопировать и запустить:

```python
import ocr
from ocr import Rectangle

def extract_invoice_number(image_path: str,
                          rect: Rectangle,
                          lang: str = "eng") -> str:
    """
    Loads an image, runs OCR on the specified rectangle, and returns
    a cleaned invoice number string.
    """
    engine = ocr.OcrEngine()
    image = ocr.Image.load(image_path)

    # Optional: force grayscale for better accuracy
    image = image.convert("L")

    result = engine.recognize_region(image, rect, lang=lang)
    raw = result.text.strip()
    cleaned = "".join(filter(str.isdigit, raw))
    return cleaned

if __name__ == "__main__":
    # Adjust these values to match your invoice layout
    invoice_rect = Rectangle(120.5, 45.2, 300.0, 60.0)
    invoice_path = "YOUR_DIRECTORY/invoice.png"

    number = extract_invoice_number(invoice_path, invoice_rect)
    print("Invoice number:", number)
```

Сохраните файл как `extract_invoice.py`, замените `YOUR_DIRECTORY` на реальный путь к папке и запустите:

```bash
python extract_invoice.py
```

Вы должны увидеть номер счета, выведенный в консоль.

---

## Часто задаваемые вопросы

**Q: Что если номер счета напечатан декоративным шрифтом?**  
A: Большинство современных OCR‑движков работают с широким спектром шрифтов, но вы можете повысить точность, обучив пользовательскую языковую модель или предварительно обработав изображение (например, применив пороговый фильтр).

**Q: Можно ли извлечь несколько полей одновременно?**  
A: Конечно. Определите список объектов `Rectangle` — по одному на поле — и пройдитесь по нему в цикле, сохраняя каждый результат в словаре.

**Q: Работает ли это с многостраничными PDF?**  
A: Сначала конвертируйте каждую страницу в изображение (используя `pdf2image` или аналогичный инструмент), затем применяйте извлечение по областям к каждой странице.

## Подведение итогов

В этом руководстве мы рассмотрели **как использовать OCR** в Python для загрузки изображения, распознавания текста в определённой области и извлечения текста этой области — идеально для получения номеров счетов, идентификаторов заказов или любого небольшого фрагмента данных из отсканированных документов. Изолируя интересующую область, вы получаете скорость, точность и меньше хлопот с пост‑обработкой.

Готовы к следующему шагу? Попробуйте расширить скрипт, чтобы **загружать изображение для OCR** из папки с пакетными счетами, или поэкспериментировать с **распознаванием текста в области** для разных полей, таких как даты и суммы. Тот же шаблон применим — просто измените координаты прямоугольника.

Если вы столкнулись с проблемами или у вас есть идеи по улучшению, оставьте комментарий ниже. Счастливого кодинга, и пусть ваши OCR‑конвейеры всегда работают точно!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как извлечь текст из изображения, подготовив прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Как использовать AspOCR: предобработка фильтров OCR для изображений в .NET](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}