---
category: general
date: 2026-06-19
description: Создайте PDF с поисковым текстом из изображения с помощью OCR на Python.
  Узнайте, как преобразовать OCR в PDF, извлечь текст из изображения и быстро выполнить
  OCR на изображении.
draft: false
keywords:
- create searchable pdf
- convert ocr to pdf
- extract text from image
- convert image to pdf
- perform ocr on image
language: ru
og_description: Создайте PDF с возможностью поиска из изображения с помощью Python
  OCR. Это руководство показывает, как преобразовать OCR в PDF, извлечь текст из изображения
  и выполнить OCR на изображении.
og_title: Создание PDF с поиском в Python – Полное пошаговое руководство
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  headline: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  type: TechArticle
- description: Create searchable PDF from an image using Python OCR. Learn to convert
    OCR to PDF, extract text from image, and perform OCR on image quickly.
  name: Create Searchable PDF in Python – Complete Step‑by‑Step Guide
  steps:
  - name: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
    text: The OCR confidence scores (`conf` values). Low confidence may mean the image
      is blurry.
  - name: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
    text: Bounding box coordinates—sometimes EasyOCR reports them in a different orientation.
  - name: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
    text: That the PDF viewer isn’t set to “image‑only” mode (rare, but some viewers
      have that option).
  type: HowTo
tags:
- OCR
- Python
- PDF
- ImageProcessing
title: Создание PDF с возможностью поиска в Python — Полное пошаговое руководство
url: /ru/python-java/general/create-searchable-pdf-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF в Python – Полное пошаговое руководство

Когда‑нибудь вам нужно было **create searchable PDF** из отсканированного чека, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с тем же, когда впервые пытаются превратить изображение текста в PDF, по которому действительно можно искать.  

В этом руководстве мы пройдем практическое решение, которое позволяет вам **perform OCR on image**, превратить результат OCR в **searchable PDF**, а также извлечь необработанный текст, если он нужен для дальнейшей обработки. Без лишних слов, только рабочий пример, который вы можете скопировать и вставить в свой проект уже сегодня.

## Что вы узнаете

- Как настроить лёгкий OCR‑движок в Python  
- Точные шаги для **convert OCR to PDF** и сохранения его как поискового документа  
- Способы **extract text from image** для последующего анализа  
- Советы по работе с распространёнными проблемами, такими как ориентация изображения и большие файлы  
- Полный, исполняемый скрипт, который вы можете адаптировать под свой случай использования

### Требования

- Установленный Python 3.8+ на вашем компьютере  
- Базовое знакомство с pip и виртуальными окружениями (необязательно, но рекомендуется)  
- Файл изображения (PNG, JPEG и т.д.), содержащий чёткий, машинно‑читаемый текст  

Если всё это у вас есть, давайте начнём.

## Шаг 1: Установите необходимую библиотеку

Фрагмент кода, который вы видели ранее, использует вымышленный пакет `ocr`, но те же идеи применимы к реальным библиотекам, таким как **EasyOCR**, **pytesseract** или **pdfminer.six**. Для этого руководства мы будем использовать **EasyOCR**, потому что он полностью написан на Python, поддерживает множество языков и предоставляет удобный метод конвертации в PDF через вспомогательный помощник.

```bash
pip install easyocr pillow
```

> **Pro tip:** Устанавливайте внутри виртуального окружения (`python -m venv venv && source venv/bin/activate`), чтобы ваши зависимости оставались упорядоченными.

## Шаг 2: Инициализируйте OCR‑движок – Perform OCR on Image

Теперь, когда библиотека готова, мы создаём OCR‑движок и указываем ему работать с английским текстом. Это первое место, где мы **perform OCR on image**.

```python
import easyocr
from PIL import Image
import io

# Create an EasyOCR reader for English
reader = easyocr.Reader(['en'])  # ← performs OCR on image
```

Зачем нужен отдельный объект‑чтения? EasyOCR предварительно загружает языковые модели, поэтому повторное использование одного и того же `reader` для нескольких изображений гораздо эффективнее, чем повторная инициализация каждый раз.

## Шаг 3: Загрузите изображение – Extract Text from Image

Давайте загрузим изображение в память. Этот шаг позже будет использоваться для **extract text from image**, но сейчас мы просто его загружаем.

```python
# Replace with the path to your receipt or scanned document
image_path = "YOUR_DIRECTORY/receipt.png"

# Open the image with Pillow (helps with format handling)
pil_image = Image.open(image_path).convert("RGB")
```

Если ваше изображение перевёрнуто или искажено, рассмотрите возможность использования методов `rotate` или `transpose` из Pillow перед передачей его в OCR‑движок. Быстрая визуальная проверка может сэкономить часы отладки позже.

## Шаг 4: Запустите OCR‑движок и получите результаты

Это ядро процесса — отправка изображения в OCR‑движок и получение обратно структурированных данных.

```python
# EasyOCR returns a list of (bbox, text, confidence) tuples
ocr_result = reader.readtext(image_path, detail=1, paragraph=True)
```

Флаг `detail=1` предоставляет нам ограничительные рамки, которые понадобятся позже для **convert OCR to PDF**. Если вам нужны только строки, установите `detail=0`.

## Шаг 5: Преобразуйте результат OCR в поисковый PDF – Convert OCR to PDF

EasyOCR не предоставляет прямой записи PDF, но мы можем собрать PDF самостоятельно, используя Pillow и библиотеку `reportlab`. Чтобы руководство оставалось лёгким, мы будем использовать `fpdf2`, который позволяет встраивать оригинальное изображение и накладывать невидимый текст.

```bash
pip install fpdf2
```

```python
from fpdf import FPDF

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        # Set invisible text style
        self.set_text_color(255, 255, 255)   # white on white background
        self.set_font("Helvetica", size=12)

        for bbox, text, conf in ocr_data:
            # bbox = [(x1,y1), (x2,y2), (x3,y3), (x4,y4)]
            x_min = min(point[0] for point in bbox)
            y_min = min(point[1] for point in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

# Create PDF instance with the original image as background
pdf = SearchablePDF(image_path)

# Add invisible OCR text on top of the image
pdf.add_ocr_text(ocr_result)

# Save the searchable PDF
output_path = "YOUR_DIRECTORY/receipt_searchable.pdf"
pdf.output(output_path)
```

Что только что произошло? Мы разместили отсканированное изображение как видимый слой, затем записали распознанные слова сверху, используя белый текст, который сливается с белым фоном. Поисковые инструменты всё равно читают скрытый слой, поэтому PDF становится **searchable** без изменения визуального вида.

## Шаг 6: Сохраните PDF‑байты — Convert Image to PDF

Если вы предпочитаете работать с PDF в памяти (например, отправлять его через API), вы можете захватить байты вместо прямой записи на диск.

```python
pdf_bytes = pdf.output(dest='S').encode('latin1')  # returns a byte string

# Example: write bytes to a file (same as Step 5 but shows the conversion)
with open(output_path, "wb") as f:
    f.write(pdf_bytes)
```

Эта строка демонстрирует классический рабочий процесс **convert image to PDF**: вы начинаете с изображения, запускаете OCR, накладываете текст и в конце выводите поток PDF.

## Шаг 7: Проверьте результат — Быстрые проверки

После выполнения скрипта откройте `receipt_searchable.pdf` в любом PDF‑просмотрщике и попробуйте поиск (Ctrl + F). Введите слово, которое, как вы знаете, присутствует в чеке — если оно переходит к нужному месту, вы успешно **create searchable pdf**!  

Если поиск не срабатывает, проверьте:

1. Оценки уверенности OCR (`conf` значения). Низкая уверенность может означать, что изображение размыто.  
2. Координаты ограничительных рамок — иногда EasyOCR сообщает их в иной ориентации.  
3. Что просмотрщик PDF не установлен в режим «только изображение» (редко, но некоторые просмотрщики имеют такую опцию).

## Полный рабочий скрипт

Объединив всё вместе, представляем полный готовый к запуску файл Python:

```python
# searchable_pdf.py
import easyocr
from PIL import Image
from fpdf import FPDF

# ---------- Configuration ----------
IMAGE_PATH = "YOUR_DIRECTORY/receipt.png"
OUTPUT_PDF = "YOUR_DIRECTORY/receipt_searchable.pdf"
# ----------------------------------

class SearchablePDF(FPDF):
    def __init__(self, image_path):
        super().__init__()
        self.add_page()
        # Fit the image to the page size
        self.image(image_path, x=0, y=0, w=self.w, h=self.h)

    def add_ocr_text(self, ocr_data):
        self.set_text_color(255, 255, 255)   # invisible white text
        self.set_font("Helvetica", size=12)
        for bbox, text, conf in ocr_data:
            x_min = min(p[0] for p in bbox)
            y_min = min(p[1] for p in bbox)
            self.set_xy(x_min, y_min)
            self.cell(0, 0, txt=text, border=0)

def main():
    # 1️⃣ Initialize OCR engine – perform OCR on image
    reader = easyocr.Reader(['en'])

    # 2️⃣ Load the image – extract text from image later
    pil_image = Image.open(IMAGE_PATH).convert("RGB")

    # 3️⃣ Run OCR and capture results
    ocr_result = reader.readtext(IMAGE_PATH, detail=1, paragraph=True)

    # 4️⃣ Convert OCR result to searchable PDF – convert OCR to PDF
    pdf = SearchablePDF(IMAGE_PATH)
    pdf.add_ocr_text(ocr_result)

    # 5️⃣ Save the PDF – convert image to PDF (or keep bytes in memory)
    pdf.output(OUTPUT_PDF)
    print(f"✅ Searchable PDF saved to {OUTPUT_PDF}")

if __name__ == "__main__":
    main()
```

Сохраните этот файл как `searchable_pdf.py`, замените заполнители `YOUR_DIRECTORY` реальными путями и запустите:

```bash
python searchable_pdf.py
```

Вы должны увидеть сообщение подтверждения и совершенно новый поисковый PDF в вашей папке.

## Часто задаваемые вопросы и особые случаи

**Что если изображение цветное?**  
EasyOCR работает как с черно‑белыми, так и с цветными изображениями, но преобразование в градации серого (`pil_image.convert("L")`) иногда повышает точность на шумных сканах.

**Можно ли обрабатывать многостраничные PDF?**  
Да — выполните цикл по каждому изображению страницы, запустите шаги OCR и добавьте каждую страницу к тому же объекту `FPDF`. Просто не забудьте сбросить курсор (`self.add_page()`) для каждого нового изображения.

**Есть ли способ сохранить оригинальный текстовый слой вместо невидимого белого текста?**  
Если вам нужен настоящий PDF «текст‑под‑изображением» (например, для доступности), рассмотрите использование `pdfminer` или `pikepdf` для встраивания скрытого текстового слоя с правильными PDF‑тегами. Это более продвинуто, но принцип остаётся тем же: фоновое изображение + наложенный текст.

**Что если уверенность OCR низкая?**  
Вы можете отфильтровать слова с низкой уверенностью:

```python
filtered = [item for item in ocr_result if item[2] > 0.8]  # keep >80% confidence
pdf.add_ocr_text(filtered)
```

## Итоги — Что мы достигли

Мы начали с простого изображения чека, **performed OCR on image**, извлекли распознанные строки и в конце **create searchable pdf**, который ведёт себя как любой профессионально отсканированный документ. Процесс охватил все вторичные ключевые слова — **convert OCR to PDF**, **extract text from image**, **convert image to PDF**, и **perform OCR on image** — так что теперь у вас есть повторно используемый набор инструментов для любого похожего проекта.

### Следующие шаги

- Поэкспериментируйте с другими языками, передавая их ISO‑коды в `easyocr.Reader(['en', 'es'])`.  
- Замените EasyOCR на Tesseract, если вам требуется полностью офлайн‑решение; остальная часть конвейера остаётся той же.  
- Добавьте визуализацию уверенности OCR (рисуйте ограничительные рамки на изображении) для отладки проблемных сканов.  

Есть свой вариант, которым хотите поделиться? Оставьте комментарий, форкните

## Что стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в ваших проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}