---
category: general
date: 2026-05-31
description: Узнайте, как использовать область интереса OCR для загрузки изображения
  и извлечения текста из прямоугольника — идеально подходит для распознавания суммы
  в счете.
draft: false
keywords:
- ocr region of interest
- extract text from rectangle
- load image for ocr
- how to extract amount
- recognize text from invoice
language: ru
og_description: Освойте область интереса OCR для загрузки изображения, извлечения
  текста из прямоугольника и распознавания текста из счета в одном учебнике.
og_title: 'OCR: область интереса — пошаговое руководство по Python'
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  headline: OCR Region of Interest – Extract Text from Rectangle in Python
  type: TechArticle
- description: Learn how to use OCR region of interest to load image for OCR and extract
    text from rectangle, perfect for recognizing amount on an invoice.
  name: OCR Region of Interest – Extract Text from Rectangle in Python
  steps:
  - name: Loads an invoice image from disk.
    text: Loads an invoice image from disk.
  - name: Marks a rectangular ROI where the total amount lives.
    text: Marks a rectangular ROI where the total amount lives.
  - name: Runs OCR only inside that ROI.
    text: Runs OCR only inside that ROI.
  - name: Prints the cleaned‑up amount string.
    text: Prints the cleaned‑up amount string.
  type: HowTo
tags:
- OCR
- Python
- Image Processing
title: OCR область интереса – извлечение текста из прямоугольника в Python
url: /ru/python-java/general/ocr-region-of-interest-extract-text-from-rectangle-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Область интереса OCR – Извлечение текста из прямоугольника в Python

Задумывались ли вы когда‑нибудь, как **ocr region of interest** конкретную часть отсканированного счета без подачи всей страницы в движок? Вы не первый, кто смотрит на размытый чек и думает: «Как извлечь сумму, которая где‑то в правом нижнем углу?» Хорошая новость в том, что вы можете указать библиотеке OCR, где именно искать, что значительно ускорит процесс и повысит точность.

В этом руководстве мы пройдем полный, готовый к запуску пример, который покажет, как **load image for OCR**, определить **region of interest**, а затем **extract text from rectangle**, чтобы наконец **recognize text from invoice** и ответить на классический вопрос «how to extract amount». Никаких расплывчатых ссылок — только конкретный код, понятные объяснения и несколько профессиональных советов, о которых вы бы хотели знать раньше.

---

## Что вы построите

1. Загружает изображение счета с диска.  
2. Отмечает прямоугольную ROI, где находится общая сумма.  
3. Запускает OCR только внутри этой ROI.  
4. Выводит очищенную строку суммы.  

Все это работает с любой библиотекой OCR, поддерживающей ROI — здесь мы используем вымышленный, но репрезентативный пакет `SimpleOCR`, имитирующий популярные инструменты, такие как Tesseract или EasyOCR. Не стесняйтесь заменить его; концепции остаются теми же.

---

## Требования

- Установлен Python 3.8+ (`python --version` должен показывать ≥3.8).  
- Устанавливаемый через pip пакет OCR (например, `pip install simpleocr`).  
- Изображение счета (PNG или JPEG), размещённое в папке, к которой вы можете обратиться.  
- Базовое знакомство с функциями и классами Python (ничего сложного).

Если у вас уже всё есть, отлично — давайте погрузимся. Если нет, сначала получите изображение; остальные шаги независимы от фактического содержимого файла.

---

## Шаг 1: Load Image for OCR

Первое, что требуется любой цепочке OCR, — это битмап для чтения. Большинство библиотек предоставляют простой метод `load_image`, принимающий путь к файлу. Вот как это делается с нашим движком `SimpleOCR`:

```python
# Step 1: Create an OCR engine instance and load the invoice image
from simpleocr import OcrEngine

# Initialize the engine (you can pass language settings here if needed)
ocr_engine = OcrEngine()

# Load the image – replace the path with yours
ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")
```

> **Pro tip:** Используйте абсолютные пути или `os.path.join`, чтобы избежать неожиданностей «файл не найден» при запуске скрипта из другой рабочей директории.

---

## Шаг 2: Define OCR Region of Interest

Вместо того чтобы позволять движку сканировать всю страницу, мы указываем ему *точно*, где находится сумма. Это шаг **ocr region of interest**, и он является ключом к надёжному извлечению, особенно когда документ содержит шумные заголовки или нижние колонтитулы.

```python
# Step 2: Define the region of interest (ROI) where the amount appears
# Rectangle(x, y, width, height) – adjust these values for your layout
from simpleocr import Rectangle

amount_region = Rectangle(120, 340, 200, 40)   # x=120, y=340, w=200, h=40
ocr_engine.add_roi(amount_region)
```

Почему именно эти числа? `x` и `y` — смещения в пикселях от верхнего‑левого угла, а `width` и `height` описывают размер коробки. Если вы не уверены, откройте изображение в любом редакторе, включите линейку и запишите координаты. Многие IDE даже позволяют выводить позицию курсора при наведении.

---

## Шаг 3: Extract Text from Rectangle

Теперь, когда ROI задан, мы просим движок **recognize text from invoice**, но ограничивая его только прямоугольником, который мы только что добавили. Вызов возвращает объект результата, который обычно содержит сырую строку, оценки уверенности и иногда ограничивающие рамки.

```python
# Step 3: Perform OCR on the specified ROI
ocr_result = ocr_engine.recognize()
```

За кулисами `recognize()` проходит по каждой ROI, обрезает этот фрагмент, запускает модель OCR и собирает результаты вместе. Поэтому определение точного **extract text from rectangle** региона может сэкономить секунды при обработке пакетных заданий.

---

## Шаг 4: How to Extract Amount – Clean the Output

OCR не идеален; часто появляются лишние пробелы, переводы строк или даже неверно распознанные символы (например, «S» вместо «5»). Быстрый `strip()` и небольшое регулярное выражение обычно решают задачу для денежных значений.

```python
# Step 4: Clean and display the recognized amount
import re

raw_amount = ocr_result.text.strip()
# Simple regex to keep digits, commas, periods, and optional currency symbols
clean_amount = re.search(r'[\d,.]+', raw_amount)
if clean_amount:
    print("Amount:", clean_amount.group())
else:
    print("Could not locate a numeric amount in the ROI.")
```

> **Why this matters:** Если вы планируете передавать сумму в базу данных или платёжный шлюз, нужен предсказуемый формат. Удаление пробельных символов и фильтрация нечисловых символов предотвращает ошибки на последующих этапах.

---

## Шаг 5: Recognize Text from Invoice – Full Script

Объединив всё вместе, представляем полный, готовый к запуску скрипт. Сохраните его как `extract_amount.py` и выполните `python extract_amount.py`.

```python
# extract_amount.py
import re
from simpleocr import OcrEngine, Rectangle

def main():
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load the invoice image (adjust the path)
    ocr_engine.load_image("YOUR_DIRECTORY/invoice.png")

    # Define ROI where the amount is located
    amount_region = Rectangle(120, 340, 200, 40)
    ocr_engine.add_roi(amount_region)

    # Run OCR on the ROI
    ocr_result = ocr_engine.recognize()

    # Clean and print the amount
    raw_amount = ocr_result.text.strip()
    match = re.search(r'[\d,.]+', raw_amount)
    if match:
        print("Amount:", match.group())
    else:
        print("Could not locate a numeric amount in the ROI.")

if __name__ == "__main__":
    main()
```

### Ожидаемый вывод

```
Amount: 1,245.67
```

Если ROI смещён, вы можете увидеть что‑то вроде `Amount: 1245.6S` — обратите внимание на лишнее «S». Скорректируйте координаты прямоугольника и запустите снова, пока вывод не станет чистым.

---

## Частые проблемы и граничные случаи

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| **ROI слишком маленькая** | Текст суммы обрезается, что приводит к частичному распознаванию. | Увеличьте `width`/`height` примерно на 10‑20 % и протестируйте снова. |
| **Неправильный DPI** | Сканы низкого разрешения (≤150 dpi) снижают точность OCR. | Пересэмплируйте изображение до 300 dpi перед загрузкой или попросите сканер использовать более высокое DPI. |
| **Несколько валют** | Регулярное выражение выбирает первую числовую группу, которая может быть номером счета. | Уточните регулярное выражение, чтобы искать символы валют (`$`, `€`, `£`) перед цифрами. |
| **Повернутые счета** | OCR‑движки предполагают вертикальный текст; повернутые страницы ломают распознавание. | Примените коррекцию вращения (`ocr_engine.rotate(90)`) перед добавлением ROI. |
| **Шум на фоне** | Тени или печати сбивают модель с толку. | Предобработайте изображение простым порогом (`cv2.threshold`) или используйте фильтр шумоподавления. |

Решение этих граничных случаев на ранних этапах экономит часы отладки позже.

---

## Профессиональные советы для реальных проектов

- **Пакетная обработка:** Перебирайте папку со счетами, вычисляйте ROI динамически (например, на основе обнаружения шаблона) и сохраняйте результаты в CSV.  
- **Сопоставление шаблонов:** Если вы работаете с несколькими макетами счетов, поддерживайте JSON‑карту `template_id → ROI coordinates`. Переключайте ROI на основе быстрого классификатора макета.  
- **Параллельное выполнение:** Используйте `concurrent.futures.ThreadPoolExecutor` для одновременного запуска нескольких экземпляров OCR — отлично подходит для высокообъёмных бэк‑офисных конвейеров.  
- **Фильтрация по уверенности:** Большинство результатов OCR включают оценку уверенности. Отбрасывайте результаты ниже порога (например, 85 %) и помечайте их для ручной проверки.

---

## Заключение

Мы рассмотрели всё, что нужно для **ocr region of interest**, **load image for OCR**, **extract text from rectangle** и, наконец, **recognize text from invoice**, чтобы ответить на классический вопрос **how to extract amount**. Скрипт компактен, но достаточно гибок, чтобы адаптироваться к различным форматам документов, языкам и OCR‑бэкендам.

Теперь, когда вы освоили основы, подумайте о расширении рабочего процесса: добавить сканирование штрих‑кодов, интегрировать парсер PDF или отправлять извлечённую сумму в бухгалтерский API. Возможности безграничны, и с чётко определённой ROI вы всегда получите более быстрые и чистые результаты.

Если возникнут сложности, оставляйте комментарий ниже — удачной OCR‑работы!

![пример области интереса OCR](https://example.com/ocr_roi_example.png "пример области интереса OCR")


## Что вам стоит изучить дальше?

- [Как извлечь текст из изображения, подготавливая прямоугольники в OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)
- [Извлечение текста из изображения Java с Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)
- [Извлечение текста из изображения – оптимизация OCR с Aspose.OCR для .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}