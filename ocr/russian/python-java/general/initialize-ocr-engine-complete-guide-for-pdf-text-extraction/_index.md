---
category: general
date: 2026-06-25
description: Инициализировать OCR‑движок в Python для извлечения текста из многостраничных
  PDF, используя пользовательские словари, настройки языка и указание области.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: ru
og_description: Инициализировать OCR‑движок в Python для надёжного чтения вьетнамских
  PDF, настроить язык, предобработку и пользовательский словарь для точных результатов.
og_title: Инициализация OCR‑движка – Пошаговое руководство по извлечению из PDF
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Инициализация OCR‑движка – Полное руководство по извлечению текста из PDF
url: /ru/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Инициализация OCR‑движка – Полное руководство по извлечению текста из PDF

Когда‑то вам нужно было **инициализировать OCR‑движок** для партии вьетнамских счетов‑фактур, но вы не знали, с чего начать? Вы не одиноки. Во многих реальных проектах первая преграда – заставить OCR‑библиотеку работать с вашими PDF, особенно когда требуется настроить язык, предобработку или пользовательский словарь.  

В этом руководстве мы пройдём через полностью готовый пример, показывающий, как **инициализировать OCR‑движок**, настроить язык, включить умную предобработку изображений, добавить пользовательский словарь и, наконец, извлечь структурированные данные со всех страниц многостраничного PDF. К концу вы получите автономный скрипт, который можно просто вставить в свой проект — без недостающих частей и без «см. документацию» ухищрений.

## Что вы узнаете

- Как **инициализировать OCR‑движок** с поддержкой вьетнамского языка.  
- Почему **настройка языка OCR** важна для точности.  
- Использование опций **OCR‑предобработки изображений**, таких как авто‑выравнивание и авто‑бинаризация.  
- Добавление **пользовательского словаря OCR** для повышения распознавания терминов отрасли.  
- **Распознавание многостраничных PDF** и извлечение конкретного региона (например, общей суммы).  
- Преобразование сырых результатов в чистую структуру, похожую на JSON, для дальнейшей обработки.

### Предварительные требования

- Установлен Python 3.8+.  
- OCR‑библиотека, предоставляющая класс `OcrEngine` (в примере используется гипотетический пакет `ocr`; замените его на ваш реальный SDK).  
- Пример многостраничного PDF (`sample.pdf`) в известной директории.  
- Базовое знакомство со словарями Python и циклами.

Если всё это у вас есть, приступаем.

---

## Шаг 1: Как инициализировать OCR‑движок в Python

Первое, что нужно сделать — **инициализировать OCR‑движок**. Представьте, что вы включаете машину и указываете, на каком языке будете работать.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Почему это важно:**  
> Большинство OCR‑движков поставляются с общими языковыми пакетами. Явно задав `ocr_engine.language`, вы избавляете движок от догадок о неправильных символах, что значительно снижает количество ошибок распознавания диакритических знаков, характерных для вьетнамского.

### Совет
Если понадобится поддерживать несколько языков в одном запуске, можно менять `ocr_engine.language` «на лету» перед обработкой каждой страницы. Не забудьте переинициализировать тяжёлые модели, если SDK требует этого.

---

## Шаг 2: Включение опций OCR‑предобработки изображений

Сырые сканы редко бывают идеальными. Наклонённые страницы, неравномерное освещение или низкий контраст могут сбить с толку даже лучшие распознаватели. Поэтому сразу после инициализации мы **настраиваем OCR‑предобработку изображений**.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Эти два флага обычно достаточны, чтобы очистить большинство сканированных счетов. Если ваши PDF уже высокого качества, их можно отключить, чтобы сэкономить несколько миллисекунд на страницу.

---

## Шаг 3: Добавление пользовательского словаря OCR

Отраслевые термины — коды заказов, идентификаторы продуктов, юридические сокращения — редко встречаются в общих языковых моделях. Добавив **пользовательский словарь OCR**, вы даёте движку «шпаргалку».

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Что происходит под капотом?**  
> Движок повышает коэффициенты уверенности для любого слова, совпадающего с записью в этом списке, делая его гораздо менее вероятным к ошибочному распознаванию.

---

## Шаг 4: Распознавание многостраничного PDF — извлечение всего текста сразу

Теперь, когда движок полностью настроен, мы можем **распознавать многостраничные PDF**. Метод `recognize_multi_page` возвращает список, где каждый элемент представляет одну страницу, уже обработанную OCR.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Если вы работаете с огромными PDF (сотни страниц), рассмотрите обработку их порциями, чтобы снизить потребление памяти. Обычно SDK предлагает потоковый API для таких сценариев.

---

## Шаг 5: Извлечение конкретного региона с каждой страницы

В большинстве счетов‑фактур поле «Общая сумма» находится в одном и том же месте на каждой странице. Вместо парсинга всего текста страницы мы можем указать движку сосредоточиться на прямоугольнике.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Зачем ограничивать область?**  
> Ограничивая OCR небольшим участком, вы ускоряете обработку и уменьшаете количество ложных срабатываний, особенно когда остальная часть страницы «шумит».

---

## Шаг 6: Формирование словаря, похожего на JSON, для каждой страницы

Сырый текст полезен, но downstream‑системы обычно ожидают структурированные данные. Ниже мы собираем чистый словарь, содержащий номер страницы, полный текст страницы, извлечённую сумму и список всех распознанных слов с коэффициентами уверенности.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Запуск скрипта выдаст серию словарей — по одному на страницу — примерно в таком виде:

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Вы легко можете перенаправить вывод в файл (`> results.jsonl`) для последующей пакетной обработки.

---

## Полный рабочий пример

Объединив всё вместе, получаем полный скрипт, который можно скопировать, вставить и запустить:

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Ожидаемый вывод

Запуск скрипта против трёхстраничного PDF‑счёта может дать:

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

Не стесняйтесь передавать результат в `jq` или любой другой JSON‑парсер для проверки структуры.

---

## Часто задаваемые вопросы и особые случаи

| Вопрос | Ответ |
|----------|--------|
| **Что делать, если мой PDF защищён паролем?** | Большинство SDK позволяют передать аргумент `password` в `recognize_multi_page`. Просто добавьте `password="mySecret"` в вызов. |
| **Мои сканы в градациях серого, а не чёрно‑белые.** | Опция `auto_binarize` справится с этим, но вы также можете вручную конвертировать изображение с помощью `Pillow` перед передачей в `recognize_region`. |
| **Общая сумма иногда появляется в другом месте.** | Либо вычисляйте прямоугольник динамически (например, через шаблонное сопоставление), либо выполните OCR всей страницы и затем ищите текст с помощью regex, например `r'\d{1,3}(,\d{3})* VND'`. |
| **Производительность падает на PDF из 500 страниц.** | Обрабатывайте пакетами: обработайте 50 страниц, запишите результаты, затем очистите список `pages`, чтобы освободить память. Также отключите `auto_deskew`, если сканы уже выровнены. |
| **Как добавить поддержку других языков позже?** | Просто измените `ocr_engine.language = ocr.Language.English` (или любой поддерживаемый enum) перед вызовом `recognize_multi_page`. Остальная часть конвейера остаётся без изменений. |

---

## Советы для продакшн‑развёртываний

1. **Обработка ошибок** — оберните вызовы OCR в блоки `try/except`; логируйте индекс страницы при сбое, чтобы можно было повторить позже.  
2. **Логирование** — используйте модуль `logging` вместо `print` для гибкой настройки уровня детализации.  
3. **Параллелизм** — если ваша OCR‑библиотека потокобезопасна, запустите `ThreadPoolExecutor` для одновременной обработки страниц.  
4. **Файл конфигурации** — храните язык, словарь и координаты прямоугольника в JSON/YAML‑файле; это делает скрипт переиспользуемым в разных проектах.  
5. **Тестирование** — создайте небольшой набор тестов с известными PDF и проверьте, что извлечённое `total_amount` совпадает с ожидаемыми значениями.  

---

## Заключение

Вы только что изучили **

## Что изучать дальше?

Следующие учебные материалы охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, помогая вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [recognize text image with Aspose OCR for multiple languages](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}