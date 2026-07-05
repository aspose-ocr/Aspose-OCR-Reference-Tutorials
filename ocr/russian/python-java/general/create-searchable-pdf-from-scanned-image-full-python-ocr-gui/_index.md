---
category: general
date: 2026-07-05
description: Создайте поисковый PDF с помощью Python. Узнайте, как выполнить OCR отсканированного
  PNG, преобразовать PDF со сканированным изображением и получить поисковый PDF за
  считанные минуты.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: ru
og_description: Быстро создавайте PDF с возможностью поиска. Это руководство показывает,
  как выполнить OCR для PNG, преобразовать отсканированный PDF‑изображение и создать
  поисковый PDF с помощью Python.
og_title: Создайте PDF с возможностью поиска из отсканированного изображения – учебник
  по OCR на Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Создание поискового PDF из отсканированного изображения – Полное руководство
  по OCR на Python
url: /ru/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Создание поискового PDF из отсканированного изображения – Полное руководство по OCR на Python

Задумывались ли вы когда‑нибудь, как **создать поисковый PDF** из отсканированной картинки без необходимости платить за дорогое программное обеспечение? Вы не одиноки. Во многих офисах PDF‑файлы приходят в виде плоских изображений — их трудно искать, невозможно копировать‑вставлять, и они становятся кошмаром для аудитов соответствия. Хорошая новость? С помощью нескольких строк кода на Python вы можете превратить этот статичный PNG в полностью поисковый PDF, и процесс проще, чем вы думаете.

В этом руководстве мы пройдем полный **пример распознавания OCR**, охватывая всё от установки нужной библиотеки до записи окончательного PDF‑файла. К концу вы точно будете знать, как **конвертировать отсканированные PDF‑изображения**, как **программно выполнять ocr pdf**, и у вас будет переиспользуемый скрипт, который можно добавить в любой проект.

## Что вы узнаете

- Установить и настроить библиотеку OCR для Python (мы будем использовать `pytesseract` и `pdf2image`).
- Инициализировать движок OCR и задать язык.
- Загрузить отсканированный PNG (или любое изображение) и выполнить OCR.
- Преобразовать результат OCR в **searchable PDF** (массив байтов) и сохранить его.
- Советы по работе с многостраничными документами, разными языками и распространёнными подводными камнями.

Предыдущий опыт работы с OCR не требуется — достаточно рабочей среды Python 3 и небольшого любопытства.

---

## Создание поискового PDF — Обзор

Ниже представлена высокоуровневая блок‑схема шагов, которые мы реализуем.  

![Диаграмма рабочего процесса создания поискового PDF](https://example.com/flowchart.png "Диаграмма рабочего процесса создания поискового PDF")

*Alt text: Диаграмма рабочего процесса создания поискового PDF, показывающая инициализацию движка, загрузку изображения, распознавание OCR, конвертацию в PDF и запись файла.*

---

## Шаг 1: Инициализация движка OCR (how to ocr pdf)

Зачем вообще нужно что‑то инициализировать? Движок OCR — это мозг, который интерпретирует пиксельные шаблоны как символы. Создавая экземпляр движка и явно задавая язык, мы сообщаем библиотеке, какой алфавит ожидать, что значительно повышает точность.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Pro tip:** Если вам нужно выполнять OCR документов на нескольких языках, установите соответствующие языковые пакеты для Tesseract и передайте список вроде `"eng+spa"` в `ocr_language`.

---

## Шаг 2: Загрузка отсканированного изображения (convert scanned image pdf)

Следующий элемент головоломки — загрузить данные изображения в Python. Независимо от того, имеете ли вы один PNG или многостраничный TIFF, класс `PIL.Image` может открыть его. Если вы начинаете с PDF, который уже содержит отсканированные изображения, `pdf2image` преобразует каждую страницу в изображение для нас.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Why this matters:** Загрузка изображения как объекта Pillow дает нам доступ к его необработанным пиксельным данным, которые нужны движку OCR. Пропуск этого шага и передача сырых байтов напрямую вызовет ошибки.

---

## Шаг 3: Выполнение распознавания OCR на изображении (ocr recognition example)

Теперь самая интересная часть — позволить движку прочитать текст. `pytesseract.image_to_pdf_or_hocr` возвращает поток байтов PDF, который уже содержит невидимый текстовый слой, что именно нам нужно для **searchable PDF**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Edge case:** Если ваше изображение имеет низкий контраст, рассмотрите возможность применения простого порога перед OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Этот небольшой шаг предобработки может значительно повысить точность.

---

## Шаг 4: Запись байтов PDF в файл (convert png searchable pdf)

Библиотека OCR передаёт нам массив байтов — представьте его как необработанное содержимое PDF‑файла. Всё, что нам теперь нужно, это записать эти байты на диск.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**What you’ll see:** Откройте полученный файл в любом PDF‑просмотрщике и попробуйте найти слово, которое вы знаете, присутствует в оригинальном изображении. Подсветка должна сразу перейти к нужному месту, подтверждая, что невидимый текстовый слой работает.

---

## Шаг 5: Расширение на многостраничные документы (convert scanned image pdf)

Реальные контракты часто охватывают несколько страниц. Чтобы **convert scanned image pdf** файлы, содержащие несколько страниц, пройдитесь по каждой странице, выполните OCR и объедините полученные PDF‑файлы.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Why merge?** Каждый вызов `image_to_pdf_or_hocr` создаёт отдельный PDF. Объединение их гарантирует, что окончательный документ сохранит исходный порядок страниц.

---

## Распространённые подводные камни и как их исправить

| Symptom | Likely Cause | Fix |
|---------|--------------|-----|
| Текст не ищется после открытия PDF | Tesseract не находит символы (пустой вывод) | Проверьте качество изображения, увеличьте DPI или примените предобработку (контраст, бинаризация). |
| Искажённые символы (например, �) | Неправильный языковой пакет или отсутствуют шрифты | Установите правильные языковые данные (`tesseract‑lang‑eng`) и убедитесь, что `ocr_language` соответствует. |
| Размер PDF‑файла огромный (>10 МБ для одностраничного изображения) | Используется lossless PNG как источник; OCR добавляет изображение полного разрешения | Уменьшите масштаб изображения перед OCR (`image.thumbnail((1240, 1754))` для A4). |
| Скрипт падает в Windows с ошибкой “tesseract.exe not found” | Бинарный файл Tesseract не в PATH | Добавьте `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (откорректируйте путь). |

---

## Полный готовый к запуску скрипт

Объединив всё вместе, вот один файл, который вы можете скопировать‑вставить и запустить:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Сохраните его как `create_searchable_pdf.py`, замените заполнители реальными путями и запустите:

```bash
python create_searchable_pdf.py
```

Вы должны увидеть a

## Что вам стоит изучить дальше?

Следующие руководства охватывают тесно связанные темы, которые опираются на техники, продемонстрированные в этом руководстве. Каждый ресурс включает полные рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы к реализации в своих проектах.

- [Как выполнить OCR PDF в .NET с помощью Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Конвертировать изображения в PDF C# — Сохранить многостраничный результат OCR](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [OCR распознавание PDF‑документов в Aspose.OCR для Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}