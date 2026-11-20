---
category: general
date: 2026-07-05
description: Как использовать OCR в Python для быстрой конвертации TIFF в текст. Узнайте
  шаги библиотеки OCR Python для извлечения текста из TIFF‑изображений и создания
  OCR‑движка на Python.
draft: false
keywords:
- how to use ocr
- ocr library python
- convert tiff to text
- extract text from tiff
- python ocr engine
language: ru
og_description: Как использовать OCR в Python? Это руководство покажет вам шаг за
  шагом, как преобразовать TIFF в текст, используя OCR‑движок на Python и библиотеку
  ocr.
og_title: Как использовать OCR в Python – Полное извлечение текста из TIFF
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  headline: How to Use OCR in Python – Extract Text from TIFF
  type: TechArticle
- description: How to use OCR in Python to convert TIFF to text quickly. Learn the
    ocr library python steps for extracting text from TIFF images and building a python
    OCR engine.
  name: How to Use OCR in Python – Extract Text from TIFF
  steps:
  - name: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
    text: '**Chunk the pages** – Instead of `recognize_multi_page`, call `engine.recognize(page)`
      inside a generator that yields one page at a time.'
  - name: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
    text: '**Adjust DPI** – Lowering the image resolution (e.g., from 300 DPI to 200 DPI)
      reduces CPU load while barely affecting accuracy for most printed text.'
  - name: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
    text: '**Parallelize** – If your OCR engine is thread‑safe, spawn a `concurrent.futures.ThreadPoolExecutor`
      to run recognition on multiple pages concurrently.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Image Processing
title: Как использовать OCR в Python — извлечение текста из TIFF
url: /ru/python-java/general/how-to-use-ocr-in-python-extract-text-from-tiff/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как использовать OCR в Python – извлечение текста из TIFF

Вы когда‑нибудь задумывались **как использовать OCR в Python**, чтобы превратить отсканированную книгу в редактируемый текст? Вы не одиноки — разработчики, исследователи и любители часто сталкиваются с этой проблемой при работе с многостраничными TIFF‑изображениями. Хорошая новость? С помощью **ocr library python** вы можете быстро создать небольшой OCR‑движок, указать ему TIFF‑файл и получить чистый, индексируемый текст за секунды.

В этом руководстве мы пройдем всё, что вам нужно: установим нужный пакет, загрузим многостраничный TIFF, запустим OCR‑движок и, наконец, выведем содержимое каждой страницы. К концу вы сможете **convert TIFF to text** и **extract text from TIFF** файлы, не выходя из среды Python.

## Требования

- Python 3.9 или новее (пример тестировался на 3.11)
- Последняя версия библиотеки `ocr` (или любой совместимый `python ocr engine`, который вы предпочитаете)
- Многостраничный TIFF‑файл, который вы хотите обработать (мы будем называть его `scanned_book.tif`)
- Базовое знакомство со скриптами Python и виртуальными окружениями

Не требуется тяжёлых внешних инструментов — только pip и несколько строк кода.

## Установка OCR Library Python

Прежде всего: вам нужен надёжный OCR‑бэкенд. Для этого руководства мы будем использовать вымышленный пакет `ocr`, который поставляется с простым высокоуровневым API, но тот же подход работает и с обёртками на основе Tesseract, такими как `pytesseract`, или коммерческими SDK.

```bash
# Create a clean virtual environment (optional but recommended)
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Pro tip:** Если вы используете Windows и пакет зависит от нативных бинарных файлов, убедитесь, что установлен соответствующий пакет Visual C++ redistributable. Установщик обычно предупредит вас, если чего‑то не хватает.

## Как использовать OCR‑движок в Python

Теперь, когда библиотека готова, давайте запустим OCR‑движок и укажем ему наш TIFF‑файл. Следующий фрагмент кода создаёт экземпляр движка, задаёт язык English и подготавливает его к обработке многостраничных файлов.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
engine = ocr.OcrEngine()
engine.language = ocr.Language.ENGLISH   # You can switch to ocr.Language.FRENCH, etc.
```

**Почему задавать язык?**  
Большинство OCR‑движков используют языковые модели для повышения точности. Если пропустить этот шаг, движок перейдёт к использованию общей модели, которая может неправильно распознавать пунктуацию или специальные символы.

## Загрузка многостраничного TIFF‑изображения

Следующий шаг — загрузка отсканированного документа. Вспомогательная функция `ocr.Image.load` понимает стеки TIFF «из коробки», возвращая объект, представляющий каждую страницу внутренне.

```python
# Step 2: Load the multi‑page TIFF image containing the scanned book
tiff_path = "YOUR_DIRECTORY/scanned_book.tif"
tiff_image = ocr.Image.load(tiff_path)
```

> **Edge case:** Если ваш TIFF использует сжатие (CCITT Group 4, LZW и т.д.) и библиотека выдаёт ошибку, попробуйте сначала конвертировать его в несжатую версию с помощью ImageMagick:
> ```bash
> convert scanned_book.tif -compress none scanned_book_uncompressed.tif
> ```

## Выполнение OCR на всех страницах — Convert TIFF to Text

Имея объект изображения, движок теперь может обработать все страницы сразу. Этот метод возвращает список, где каждый элемент содержит результат OCR для отдельной страницы.

```python
# Step 3: Perform OCR on all pages of the image
page_results = engine.recognize_multi_page(tiff_image)
```

**Что происходит «под капотом»?**  
Функция `recognize_multi_page` проходит по каждой растеризованной странице, запускает нейронный распознаватель и упаковывает вывод простого текста вместе с оценками уверенности. По сути, это пакетная операция, экономящая вам написание ручного цикла.

## Итерация по результатам — Extract Text from TIFF

Наконец, мы выводим распознанный текст. Вы можете записать результат в отдельные файлы `.txt`, загрузить его в базу данных или передать в поисковый индекс — что бы ни соответствовало вашему рабочему процессу.

```python
# Step 4: Iterate through the results and display the recognized text for each page
for page_index, result in enumerate(page_results):
    print(f"Page {page_index + 1}:\n{result.text}\n")
```

### Ожидаемый вывод

```
Page 1:
Chapter 1
In the beginning...

Page 2:
The quick brown fox jumps over the lazy dog.

Page 3:
...

```

Каждая строка `result.text` содержит необработанный вывод OCR для этой страницы. Если вам необходимо сохранять переносы строк, большинство движков предоставляют `result.lines` в виде списка строк.

## Обработка больших TIFF‑файлов — советы и приёмы

Обработка TIFF‑файла в 500 страниц может требовать много памяти. Вот несколько стратегий, чтобы всё прошло гладко:

1. **Chunk the pages** – Вместо `recognize_multi_page` вызывайте `engine.recognize(page)` внутри генератора, который выдаёт одну страницу за раз.
2. **Adjust DPI** – Понижение разрешения изображения (например, с 300 DPI до 200 DPI) уменьшает нагрузку на CPU, почти не влияя на точность большинства печатных текстов.
3. **Parallelize** – Если ваш OCR‑движок потокобезопасен, создайте `concurrent.futures.ThreadPoolExecutor` для одновременного распознавания нескольких страниц.

```python
import concurrent.futures

def ocr_page(page):
    return engine.recognize(page).text

with concurrent.futures.ThreadPoolExecutor(max_workers=4) as executor:
    texts = list(executor.map(ocr_page, tiff_image.pages))
```

## Сохранение извлечённого текста в файлы

Большинству реальных конвейеров требуется постоянное хранилище. Ниже показан лаконичный способ выгрузить текст каждой страницы в отдельный файл, сохраняя порядок страниц.

```python
import pathlib

output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for i, result in enumerate(page_results, start=1):
    file_path = output_dir / f"page_{i:03}.txt"
    file_path.write_text(result.text, encoding="utf-8")
    print(f"Saved page {i} to {file_path}")
```

Теперь у вас есть чистый каталог файлов `.txt`, готовый для индексации или дальнейшей обработки NLP.

## Предпросмотр изображения — How to Use OCR Results Visually

Если вы хотите увидеть наложение OCR на оригинальное изображение (удобно для отладки), многие библиотеки позволяют рисовать ограничивающие рамки. Вот быстрый пример с использованием Pillow:

```python
from PIL import ImageDraw

for page, result in zip(tiff_image.pages, page_results):
    draw = ImageDraw.Draw(page)
    for word in result.words:          # Assume `result.words` gives bounding boxes
        draw.rectangle(word.box, outline="red")
    page.show()   # Opens the annotated page
```

![Как использовать OCR в Python – наложение OCR на страницу TIFF](ocr_overlay_example.png)

*Alt text:* Как использовать OCR в Python – визуальное наложение распознанного текста на страницу TIFF.

## Распространённые подводные камни и как их избежать

| Проблема | Почему происходит | Решение |
|----------|-------------------|---------|
| Искажённые символы | Неправильная языковая модель | Установите `engine.language` на правильный enum |
| Отсутствующие страницы | Сжатие TIFF не поддерживается | Сначала конвертируйте в несжатый TIFF |
| Низкая производительность | Высокое DPI + однопоточная обработка | Снизьте DPI или включите многопоточность |
| Пустой вывод | Изображение слишком тёмное/низкий контраст | Предобработайте с растягиванием контраста (`opencv` или `Pillow`) |

Решение этих проблем на ранних этапах сэкономит вам часы отладки позже.

## Следующие шаги — выход за пределы базового извлечения

Теперь, когда вы освоили основы **how to use OCR in Python**, рассмотрите возможность изучения:

- **PDF generation** – Объедините извлечённый текст с `reportlab` для создания поисковых PDF‑файлов.
- **Language detection** – Автоматически переключайте `engine.language` с помощью `langdetect`.
- **Structured data extraction** – Используйте регулярные выражения или spaCy для извлечения дат, имён или таблиц из сырого текста.
- **Alternative OCR backends** – Замените `ocr` на `pytesseract` или `easyocr`, если нужна поддержка нескольких языков.

Каждая из этих тем естественно связывается со вторичными ключевыми словами **ocr library python**, **convert tiff to text**, **extract text from tiff**, и **python ocr engine**, предоставляя вам прочную основу для более продвинутых проектов.

---

### Заключение

Мы рассмотрели **how to use OCR in Python** от установки до обработки многостраничных файлов, показав вам точно, как **convert TIFF to text** и **extract text from TIFF** с помощью простого **python OCR engine**. Полный, готовый к запуску пример выше должен работать «из коробки» для большинства стандартных TIFF‑файлов, а приведённые советы помогут вам масштабировать процесс для больших документов или интегрировать OCR в более крупные конвейеры.

Попробуйте это с вашими собственными отсканированными книгами, квитанциями или архивными изображениями — затем экспериментируйте с идеями более высокого уровня, перечисленными в разделе «Следующие шаги». Приятного кодинга, и пусть ваши результаты OCR всегда будут точными!

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Извлечение текста из изображения с Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Как извлечь текст из TIFF с помощью Aspose.OCR для Java](/ocr/english/java/ocr-operations/recognize-tiff/)
- [Как выполнить извлечение текста из изображения из потока с использованием Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}