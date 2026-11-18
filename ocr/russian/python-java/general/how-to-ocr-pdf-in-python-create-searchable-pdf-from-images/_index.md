---
category: general
date: 2026-06-06
description: Как выполнять OCR PDF и создавать поисковые PDF‑файлы из изображений
  с помощью Python. Научитесь добавлять поисковый текст и преобразовывать изображение
  в PDF/A за считанные минуты.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: ru
og_description: Как выполнить OCR PDF пошагово. Узнайте, как добавить поисковый текст
  и преобразовать изображение в PDF/A с помощью простого скрипта на Python.
og_title: Как выполнить OCR PDF – Краткое руководство по созданию поисковых PDF
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Как выполнить OCR PDF в Python — создать поисковый PDF из изображений
url: /ru/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнить OCR PDF – Преобразовать отсканированные изображения в поисковые PDF

Когда‑то задумывались **как выполнить OCR PDF**‑файлов, если у вас есть лишь отсканированное изображение счета или чека? Вы не одиноки. Во многих офисах входящая документация приходит в виде плоских PNG или JPEG, а следующий шаг — сделать содержимое доступным для поиска — кажется черным ящиком.  

Хорошие новости? Всего несколькими строками Python вы можете **создать поисковый PDF**, **добавить поисковый текст** и даже **преобразовать изображение в PDF/A** для долгосрочного архивирования. В этом руководстве мы пройдем каждый шаг, объясним, почему он важен, и предоставим готовый к запуску скрипт, который можно вставить в любой проект.

> **Совет:** Тот же подход работает для многостраничных сканов; просто переберите файлы в цикле, и движок выполнит всю тяжелую работу.

---

## Что понадобится

Прежде чем приступить, убедитесь, что на вашем компьютере установлено следующее:

| Требование | Почему это важно |
|------------|------------------|
| Python 3.9 или новее | Современный синтаксис и лучшая поддержка библиотек |
| OCR‑движок на основе `pdfium` (например, `pdfocr` или коммерческий SDK) | Обрабатывает как распознавание изображений, так и генерацию PDF/A |
| Файл изображения (PNG, JPEG, TIFF), который нужно превратить в поисковый PDF | Источник текста |
| Права записи в папку вывода | Чтобы скрипт мог сохранить новый PDF |

Если OCR‑SDK ещё не установлен, выполните:

```bash
pip install pdfocr   # replace with your vendor's package name
```

И всё — никаких сложных системных зависимостей, только `pip install`.

---

## Как выполнить OCR PDF – Обзор

На высоком уровне процесс состоит из трёх простых действий:

1. **Распознать** текст внутри изображения, сохранив оригинальную графику.  
2. **Экспортировать** результат OCR вместе с оригинальным изображением как **поисковый PDF/A** (архивный вариант PDF).  
3. **Проверить**, что полученный файл содержит выбираемый, поисковый текст, наложенный на оригинальную картинку.

Ниже каждый шаг показан в коде с объяснением *почему* команд так написаны.

---

## Шаг 1: Распознавание текста на изображении

Сначала мы просим OCR‑движок прочитать пиксели и вернуть объект результата, содержащий как исходное изображение, так и извлечённый текст. По сути, движок «читает» ваш счёт за вас.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Почему это важно

- **Сохранение графики** означает, что визуальное расположение (таблицы, логотипы, печати) остаётся точно таким, каким её захватил сканер.  
- Объект `result` обычно содержит скрытый текстовый слой, который мы позже внедрим в PDF.  
- Использование `recognize_image` вместо `recognize_pdf` избавляет от дополнительного шага конвертации, ускоряя обработку одиночных изображений.

#### Распространённые варианты

- Если у вас **многостраничный TIFF**, передайте путь к файлу напрямую; большинство движков обработают каждую страницу как отдельное изображение.  
- Для PDF, уже содержащих изображения, можно вызвать `engine.recognize_pdf("file.pdf")` и полностью пропустить этот шаг.

---

## Шаг 2: Экспорт результата OCR как поискового PDF/A

Теперь берём `result` из шага 1 и просим движок записать новый файл. Ключевой флаг здесь — *PDF/A* — стандарт ISO для PDF, предназначенный для долгосрочного сохранения.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Почему это важно

- **Поисковый PDF**: В выходном файле появляется скрытый, выбираемый текстовый слой. Теперь можно использовать Ctrl + F для поиска по документу.  
- **Соответствие PDF/A**: Некоторые организации (юридические, финансовые) требуют PDF/A для аудиторских следов; этот шаг автоматически удовлетворяет требование.  
- Метод также **добавляет поисковый текст** без сплющивания изображения, поэтому визуальная точность остаётся идеальной.

#### Пограничный случай: нужен обычный PDF?

Если PDF/A не требуется, замените `save_as_pdfa` на `save_as_pdf`. Остальная часть рабочего процесса остаётся без изменений.

---

## Шаг 3: Проверка поискового PDF

Быстрая проверка избавит от загадочных ошибок позже. Откройте сгенерированный файл в любом PDF‑просмотрщике, попробуйте выделить слово и используйте функцию поиска.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Ожидаемый вывод

При запуске скрипта в консоль будет выведено:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Открыв файл, вы увидите оригинальное изображение счета с лёгким, невидимым текстовым слоем. Выделите любое слово — оно будет выбираемым; **это и есть добавленный поисковый текст**.

---

## Добавление поискового текста в существующие PDF (Бонус)

Иногда у вас уже есть PDF, но нужно **добавить поисковый текст**. Тот же движок может наложить результаты OCR на существующий PDF:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Здесь `apply_to` объединяет скрытый слой с оригинальными страницами, позволяя **создать поисковый PDF** без повторного сканирования.

---

## Распространённые подводные камни и советы

| Проблема | Как избежать |
|----------|--------------|
| **Низкое разрешение исходных изображений** (< 150 dpi) | Увеличьте масштаб или запросите скан более высокого разрешения; точность OCR резко падает ниже 150 dpi. |
| **Отсутствие языковых данных** | Установите соответствующие языковые пакеты для вашего OCR‑движка (`pip install pdfocr[eng,spa]`). |
| **Папка вывода недоступна для записи** | Запустите скрипт с достаточными правами или выберите другую директорию. |
| **Проверка PDF/A не проходит** | Убедитесь, что не встраиваете неподдерживаемые шрифты или JavaScript; большинство SDK автоматически справляются с этим при использовании `save_as_pdfa`. |

---

## Полный скрипт — однофайловое решение

Ниже представлен автономный скрипт, объединяющий всё вместе. Скопируйте‑вставьте, замените пути‑заполнители, и вы готовы **преобразовать изображение в PDF/A** за секунды.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**Что делает этот скрипт:**  
1. Загружает OCR‑движок.  
2. Считывает выбранное изображение и извлекает текст.  
3. Записывает **поисковый PDF/A**, готовый к распространению или архивированию.  

Не стесняйтесь вынести логику `main` в функцию, обрабатывающую целую папку — просто перебирайте `os.listdir()` и повторяйте три шага для каждого файла.

---

## Следующие шаги и смежные темы

Теперь, когда вы освоили **как выполнить OCR PDF**, рассмотрите следующие идеи:

- **Пакетная обработка:** Используйте `concurrent.futures` для одновременного OCR десятков счетов.  
- **Внедрение метаданных:** Добавляйте даты создания или номера счетов в метаданные PDF для упрощённого индексирования.  
- **Гибридные PDF:** Комбинируйте поисковый текст с встраиваемыми оригинальными изображениями для «цифрового двойника» бумажного документа.  
- **Альтернативные форматы вывода:** Экспортируйте в **DOCX** или **HTML**, если downstream‑системы требуют редактируемые форматы.

Каждый из этих пунктов опирается на базовые концепции, которые вы только что изучили — распознавание, экспорт, проверка.

---

## Итоги

Короче говоря, теперь вы знаете **как выполнить OCR PDF**‑файлов, превратив простое изображение в **поисковый PDF/A** всего в три строки Python. Скрипт берёт на себя всю тяжёлую работу, сохраняет оригинальную графику и выдаёт документ, соответствующий стандартам, который можно искать, архивировать или делиться им.  

Попробуйте на своих счетах, чеках или сканированных контрактах. Если возникнут сложности, оставьте комментарий ниже или обратитесь к официальной документации SDK — обычно там полно дополнительных примеров. Приятного кодинга и наслаждайтесь новой возможностью мгновенно делать любые изображения поисковыми! 

![How to OCR PDF example showing original image and searchable PDF overlay](placeholder.png "How to OCR PDF example")

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, построенные на техниках, продемонстрированных в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}