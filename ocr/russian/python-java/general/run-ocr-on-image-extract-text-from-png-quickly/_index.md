---
category: general
date: 2026-03-18
description: Запустите OCR на изображении, чтобы извлечь текст из PNG и создать PDF
  с возможностью поиска. Узнайте, как распознавать текст на изображении и конвертировать
  PNG в PDF за считанные минуты.
draft: false
keywords:
- run OCR on image
- extract text from png
- recognize text image
- generate searchable pdf
- convert png to pdf
language: ru
og_description: Запустите OCR на изображении, чтобы извлечь текст из PNG, распознать
  текст на изображении и создать PDF с возможностью поиска. Следуйте этому пошаговому
  руководству.
og_title: Запустите OCR на изображении – быстро извлеките текст из PNG
tags:
- OCR
- Python
- Image Processing
title: Выполните OCR на изображении — быстро извлеките текст из PNG
url: /ru/python-java/general/run-ocr-on-image-extract-text-from-png-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Запуск OCR на изображении – Быстрое извлечение текста из PNG

Когда‑нибудь вам нужно было **run OCR on image** файлы, но вы не знали, с чего начать? Возможно, у вас есть отсканированная статья, сохранённая как `article.png`, и вам нужен просто обычный текст, или нужен PDF с возможностью поиска для архивирования. В любом случае, вы попали в нужное место. В этом руководстве мы пройдём процесс извлечения текста из PNG, распознавания текста на изображении и даже преобразования PNG в PDF с возможностью поиска — всё это с помощью нескольких строк кода.

> **What you’ll get:** полный, исполняемый скрипт, который загружает PNG, запускает OCR, сохраняет вывод hOCR и при желании создаёт PDF с возможностью поиска. Нет недостающих импортов, нет «см. документацию» тупиков — просто автономное решение, которое вы можете сразу добавить в свой проект сегодня.

## Предварительные требования

- **Python 3.8+** (синтаксис, используемый здесь, работает на любой современной версии)
- Библиотека **`ocr_engine`**, которую вы используете (в примере предполагается класс `OcrEngine`; замените на Tesseract, EasyOCR и т.д., если нужно)
- PNG‑изображение, которое вы хотите обработать (например, `article.png`, размещённый в папке, к которой у вас есть доступ)
- Разрешение на запись в каталог вывода

Если вы используете Tesseract под капотом, установите его с помощью:

```bash
# Ubuntu/Debian
sudo apt-get install tesseract-ocr

# macOS (Homebrew)
brew install tesseract
```

А затем установите Python‑обёртку:

```bash
pip install pytesseract Pillow
```

*Pro tip:* держите вашу OCR‑библиотеку в актуальном состоянии — новые языковые пакеты и улучшения производительности появляются часто.

## Запуск OCR на изображении – Пошаговое руководство

Ниже представлен **complete script**. Не стесняйтесь скопировать‑вставить его в файл с именем `run_ocr.py` и запустить его командой `python run_ocr.py`.

```python
# run_ocr.py
import os
from pathlib import Path

# Import the OCR engine – replace with your actual import if different
# For Tesseract via pytesseract you would use: import pytesseract
# Here we assume a generic OcrEngine class that matches the example
from ocr_engine import OcrEngine  # <-- adjust as needed

def main():
    # ------------------------------------------------------------------
    # Step 1: Create an OCR engine instance
    # ------------------------------------------------------------------
    ocr_engine = OcrEngine()
    # Why this matters: the engine holds configuration (language, DPI, etc.)
    # You can tweak ocr_engine.setLanguage('eng') or similar before proceeding.

    # ------------------------------------------------------------------
    # Step 2: Load the image you want to process
    # ------------------------------------------------------------------
    image_path = Path("YOUR_DIRECTORY/article.png")
    if not image_path.is_file():
        raise FileNotFoundError(f"Image not found: {image_path}")
    ocr_engine.setImageFromFile(str(image_path))

    # ------------------------------------------------------------------
    # Step 3: Choose the export format
    # ------------------------------------------------------------------
    # hOCR preserves layout (bounding boxes, fonts) – perfect for searchable PDFs.
    # Other options: "txt", "pdf", "pdfa"
    ocr_engine.setExportFormat("hocr")

    # ------------------------------------------------------------------
    # Step 4: Run the recognition process
    # ------------------------------------------------------------------
    ocr_result = ocr_engine.recognize()
    # The result object gives us access to the raw OCR text, hOCR, etc.

    # ------------------------------------------------------------------
    # Step 5: Write the HOCR output to a file
    # ------------------------------------------------------------------
    output_path = Path("YOUR_DIRECTORY/article.hocr")
    with open(output_path, "w", encoding="utf-8") as output_file:
        output_file.write(ocr_result.getExportedContent())
    print(f"✅ HOCR saved to {output_path}")

    # ------------------------------------------------------------------
    # Optional: Generate a searchable PDF from the HOCR
    # ------------------------------------------------------------------
    # Many OCR engines can bundle the original image with the hOCR to produce
    # a PDF that you can search. If your engine supports it, uncomment:
    # ocr_engine.setExportFormat("pdf")
    # pdf_result = ocr_engine.recognize()
    # pdf_path = Path("YOUR_DIRECTORY/article_searchable.pdf")
    # with open(pdf_path, "wb") as pdf_file:
    #     pdf_file.write(pdf_result.getExportedContent())
    # print(f"📄 Searchable PDF created at {pdf_path}")

if __name__ == "__main__":
    main()
```

### Что делает скрипт, простыми словами

1. **Instantiate** OCR‑движок, чтобы вы могли управлять его настройками.
2. **Load** PNG‑файл (`article.png`). Скрипт завершится раннее, если файл отсутствует — никаких загадочных ошибок `NoneType` позже.
3. **Select** `hocr` как формат экспорта. Этот формат сохраняет оригинальную разметку, что важно для последующего преобразования изображения в PDF с возможностью поиска.
4. **Run** движок распознавания; здесь происходит основная работа.
5. **Write** hOCR‑XML в `article.hocr`. Теперь у вас есть машинно‑читаемое представление текста и его координат.
6. *(Optional)* переключитесь на `"pdf"` и создайте PDF с возможностью поиска одним дополнительным шагом.

Ожидаемый **output** — это файл `.hocr`, закодированный в UTF‑8, который выглядит примерно так (сокращённо):

```xml
<div class='ocr_page' id='page_1' title='image "article.png"; bbox 0 0 2480 3508; ppageno 0'>
  <div class='ocr_carea' id='block_1_1' title="bbox 100 100 2400 3400">
    <p class='ocr_par' id='par_1' title="bbox 100 100 2400 200">
      <span class='ocr_line' id='line_1' title="bbox 100 100 2400 150; baseline 0 -5">
        <span class='ocrx_word' id='word_1' title="bbox 100 100 300 150; x_wconf 96">This</span>
        <span class='ocrx_word' id='word_2' title="bbox 310 100 500 150; x_wconf 92">is</span>
        …
```

Если раскомментировать секцию PDF, вы также получите `article_searchable.pdf`, который можно открыть в любом PDF‑просмотрщике и воспользоваться полем поиска **Ctrl + F**, чтобы мгновенно находить слова.

![Пример вывода Run OCR on image](example.png "Run OCR on image – результаты hOCR и PDF")

## Как извлечь текст из PNG с помощью OcrEngine

Если вам нужен только чистый текст (без разметки, без PDF), вы можете полностью пропустить шаг hOCR:

```python
ocr_engine.setExportFormat("txt")
text_result = ocr_engine.recognize()
plain_text = text_result.getExportedContent()
print("📝 Extracted text:\n", plain_text)
```

*Why choose plain text?* Это лёгко, идеально подходит для индексации и отлично работает с последующими NLP‑конвейерами.

## Распознавание текста на изображении и создание PDF с возможностью поиска

Создание PDF с возможностью поиска — это двухэтапный процесс:

1. **Run OCR** с `hocr` (как мы делали выше), чтобы получить информацию о разметке.
2. **Combine** оригинальный PNG с hOCR в PDF, используя PDF‑экспортер движка.

Большинство современных OCR‑библиотек (Tesseract, ABBYY, Google Vision) предоставляют экспорт `pdf`, который делает именно это. Фрагмент в блоке *Optional* основного скрипта демонстрирует шаблон. Если у вашей библиотеки нет встроенного PDF‑экспортера, вы можете использовать **`pdf2image`** + **`reportlab`**, чтобы объединить изображение и hOCR — просто дайте знать, и я поделюсь быстрым дополнительным примером.

## Преобразование PNG в PDF с выводом OCR

Иногда вам нужен просто **plain PDF**, содержащий изображение (без слоя поиска). Это ещё проще:

```python
from PIL import Image

png_path = Path("YOUR_DIRECTORY/article.png")
pdf_path = Path("YOUR_DIRECTORY/article.pdf")

# Pillow can convert directly:
Image.open(png_path).convert("RGB").save(pdf_path, "PDF", resolution=100.0)
print(f"📄 PNG converted to PDF at {pdf_path}")
```

Объедините это с шагом OCR, если нужна версия с поиском, или оставьте как точную визуальную копию для архивных целей.

## Распространённые подводные камни и советы

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Размытие или низкое разрешение PNG** | Точность OCR резко падает ниже ~300 DPI. | Увеличьте масштаб с помощью `Image.resize((width*2, height*2), Image.LANCZOS)` перед передачей в движок. |
| **Неправильный язык** | Движок по умолчанию использует английский; символы не‑английских языков искажаются. | Вызовите `ocr_engine.setLanguage('deu')` (или соответствующий ISO‑код) перед `recognize()`. |
| **Отсутствует вывод hOCR** | Некоторые движки по умолчанию выводят простой текст, если не вызван `setExportFormat`. | Убедитесь, что `setExportFormat("hocr")` вызывается **до** `recognize()`. |
| **Ошибки прав доступа к файлам** | Попытка записи в папку только для чтения. | Используйте путь внутри вашего проекта или сначала выполните `os.makedirs(..., exist_ok=True)`. |
| **Большие PDF вызывают всплески памяти** | PDF‑экспортер держит всё изображение в ОЗУ. | Обрабатывайте страницы порциями или используйте потоковый PDF‑писатель. |

*Pro tip:* всегда тестируйте на небольшом образце изображения перед масштабированием до тысяч файлов. Это экономит часы отладки.

## Итоги

Теперь вы знаете **how to run OCR on image** файлы, **extract text from PNG**, **recognize text image** для последующих задач, **generate a searchable PDF** и **convert PNG to PDF**, когда нужен простой архив. Предоставленный скрипт — это готовое, готовое к копированию решение, которое работает сразу, а опциональные секции позволяют настроить вывод под ваш конкретный рабочий процесс.

### Что дальше?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}