---
category: general
date: 2026-06-25
description: Извлечение текста из PDF с помощью OCR на Python. Узнайте, как преобразовать
  PDF в текст с понятным примером OCR на Python и получить надёжные результаты быстро.
draft: false
keywords:
- extract pdf text OCR
- convert pdf to text
- python ocr example
- Aspose OCR Python
- multi‑page PDF OCR
language: ru
og_description: Извлечение текста из PDF с помощью OCR на Python. Это руководство
  демонстрирует пример OCR на Python, который преобразует PDF в текст, легко обрабатывая
  многостраничные документы.
og_title: Извлечение текста из PDF с помощью OCR в Python – Полный программный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract PDF text OCR using Python. Learn how to convert PDF to text
    with a clear python OCR example and get reliable results fast.
  headline: Extract PDF Text OCR in Python – Complete Step‑by‑Step Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF processing
title: Извлечение текста из PDF с помощью OCR в Python — Полное пошаговое руководство
url: /ru/python-java/general/extract-pdf-text-ocr-in-python-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PDF с помощью OCR в Python – Полное пошаговое руководство

Когда‑то вам нужно было **извлечь текст из PDF с помощью OCR**, но вы не знали, какая библиотека справится с многостраничными PDF без проблем? Вы не одиноки. Во многих реальных проектах — будь то юридические контракты, отсканированные счета или архивные отчёты — получение чистого, поискового текста из PDF является обязательным навыком.

В этом руководстве мы пройдём через **python ocr example**, который **convert pdf to text** с использованием Aspose.OCR. К концу вы получите готовый к запуску скрипт, который извлекает текст со всех страниц, показывает предварительный просмотр и сохраняет весь документ в один файл `.txt`. Без лишних слов, только практическое решение, которое можно сразу внедрить в ваш код.

## Что вы узнаете

- Как установить и импортировать модуль Aspose OCR для Python.  
- Как создать экземпляр OCR‑движка и выполнить **extract pdf text OCR** для многостраничного PDF.  
- Как пройтись по результатам каждой страницы, отобразить предварительный просмотр и записать полный вывод на диск.  
- Советы по работе с распространёнными проблемами, такими как пустые страницы или символы Unicode.  

> **Prerequisites:** установлен Python 3.8+, базовые навыки работы с pip и PDF‑файл, который вы хотите обработать. Предыдущий опыт работы с OCR не требуется.

---

![Extract PDF Text OCR workflow diagram](extract-pdf-text-ocr.png "Diagram of extract pdf text OCR process")

*Alt text: Диаграмма, иллюстрирующая процесс извлечения текста из PDF с помощью OCR в Python.*

## Шаг 1: Установите Aspose OCR для Python

Прежде чем запускать любой код, необходимо установить пакет Aspose.OCR. Он распространяется через PyPI, поэтому достаточно одной команды pip.

```bash
pip install aspose-ocr
```

> **Pro tip:** Если вы работаете внутри виртуального окружения (настоятельно рекомендуется), сначала активируйте его, чтобы изолировать зависимости.

## Шаг 2: Импортируйте модуль и создайте OCR‑движок

Теперь, когда библиотека доступна, импортируйте её и создайте `OcrEngine`. Движок — это «мозг», который выполняет всю тяжёлую работу: распознаёт символы, обрабатывает макет страниц и возвращает чистые строки Unicode.

```python
# Step 2: Import the Aspose OCR module and create an engine
import aspose.ocr as ocr

engine = ocr.OcrEngine()
```

> **Why this matters:** Создание экземпляра движка один раз и его повторное использование для всех страниц гораздо эффективнее, чем создание нового движка для каждой страницы. Это также гарантирует одинаковые настройки на протяжении всего документа.

## Шаг 3: Распознайте все страницы PDF (многостраничный OCR)

Метод `recognize_multi_page` Aspose.OCR принимает путь к файлу и возвращает список объектов `OcrResult` — по одному на каждую страницу. Это ядро нашей операции **convert pdf to text**.

```python
# Step 3: Run OCR on every page of the PDF
pdf_path = "YOUR_DIRECTORY/contract.pdf"   # replace with your actual file
pdf_pages = engine.recognize_multi_page(pdf_path)  # returns List[OcrResult]
```

> **Edge case:** Если PDF защищён паролем, перед вызовом `recognize_multi_page` необходимо задать пароль через `engine.set_password("your_password")`.

## Шаг 4: Пройдитесь по результатам и покажите предварительный просмотр

Быстрый просмотр помогает убедиться, что OCR действительно извлекает текст. Мы выведем первые 200 символов каждой страницы, но при необходимости можете изменить срез.

```python
# Step 4: Display a short preview of each page’s extracted text
for page_number, page_result in enumerate(pdf_pages, start=1):
    print(f"--- Page {page_number} ---")
    # Show the first 200 characters of the page's OCR text
    print(page_result.text[:200])
    print()  # blank line for readability
```

**Sample output**

```
--- Page 1 ---
This Agreement is made on the 1st day of January 2025 between ...

--- Page 2 ---
WHEREAS, the Parties desire to enter into a collaborative ...

--- Page 3 ---
IN WITNESS WHEREOF, the Parties have executed this Agreement ...
```

Выше показан лишь фрагмент, а полный текст находится в `page_result.text`.

## Шаг 5: Объедините все страницы в один текстовый файл (по желанию)

Большинство последующих процессов — индексация поиска, анализ данных или простое архивирование — предпочитают один файл `.txt`. Давайте сконкатенируем страницы и запишем их.

```python
# Step 5: Save the complete OCR output to a .txt file
output_path = "YOUR_DIRECTORY/contract_extracted.txt"

with open(output_path, "w", encoding="utf-8") as out_file:
    for page_result in pdf_pages:
        out_file.write(page_result.text)
        out_file.write("\n\n")  # separate pages with a blank line
print(f"All pages saved to {output_path}")
```

> **Why this works:** Использование UTF‑8 гарантирует, что вы не потеряете специальные символы, такие как буквы с диакритическими знаками или символы, часто встречающиеся в юридических документах.

## Шаг 6: Обработка распространённых проблем

| Проблема | Симптом | Решение |
|----------|---------|----------|
| Пустые страницы в выводе | `page_result.text` пустой | Убедитесь, что исходный PDF действительно содержит отсканированные изображения; некоторые PDF уже содержат текст и требуют другого подхода (например, библиотеки для извлечения текста из PDF). |
| Искажённые символы | Вместо букв появляются странные символы | Проверьте, что язык OCR‑движка установлен правильно: `engine.language = ocr.Language.English` (или другой язык). |
| Большие PDF‑файлы обрабатываются слишком долго | Скрипт «зависает» на странице | Включите многопоточность: `engine.recognize_multi_page(pdf_path, ocr.RecognizeOptions(parallel=True))`. |
| Ошибки памяти при работе с огромными файлами | Возникает `MemoryError` | Обрабатывайте PDF частями (например, по 50 страниц) или увеличьте лимит памяти Python. |

## Полный скрипт — готов к запуску

Объединив всё вместе, получаем полностью автономный скрипт, который можно скопировать в файл `extract_pdf_text_ocr.py`.

```python
# extract_pdf_text_ocr.py
# Complete python ocr example that extracts PDF text using Aspose OCR.

import aspose.ocr as ocr

def main():
    # 1️⃣ Install the library via `pip install aspose-ocr` before running.
    # 2️⃣ Set the path to your PDF.
    pdf_path = "YOUR_DIRECTORY/contract.pdf"
    output_path = "YOUR_DIRECTORY/contract_extracted.txt"

    # 3️⃣ Create the OCR engine.
    engine = ocr.OcrEngine()
    # Optional: set language for better accuracy.
    # engine.language = ocr.Language.English

    # 4️⃣ Perform multi‑page OCR.
    pdf_pages = engine.recognize_multi_page(pdf_path)

    # 5️⃣ Show a preview of each page.
    for page_number, page_result in enumerate(pdf_pages, start=1):
        print(f"--- Page {page_number} ---")
        print(page_result.text[:200])
        print()

    # 6️⃣ Write the full text to a file.
    with open(output_path, "w", encoding="utf-8") as out_file:
        for page_result in pdf_pages:
            out_file.write(page_result.text)
            out_file.write("\n\n")
    print(f"✅ All pages saved to {output_path}")

if __name__ == "__main__":
    main()
```

Запустите его из терминала:

```bash
python extract_pdf_text_ocr.py
```

Вы увидите предварительные просмотры страниц в консоли, а затем подтверждение, что полный текст сохранён.

## Итоги и дальнейшие шаги

Мы продемонстрировали, как **extract pdf text OCR** с помощью лаконичного **python ocr example**, который **convert pdf to text** эффективно. Основные шаги — установка, импорт, создание движка, запуск `recognize_multi_page`, просмотр и сохранение — покрывают типичный рабочий процесс для отсканированных PDF.

**Что дальше?**  

- **Точная настройка:** Поэкспериментируйте с `engine.recognize_multi_page(..., RecognizeOptions(...))`, меняя DPI или подключая языковые пакеты.  
- **Постобработка:** Удаляйте лишние пробелы, запускайте проверку орфографии или передавайте текст в конвейер обработки естественного языка.  
- **Пакетная обработка:** Пройдитесь по папке с PDF, чтобы построить поисковый архив.  

Если возникнут проблемы, проверьте, что PDF действительно содержит растровые изображения (OCR работает с изображениями, а не с встроенным текстом). Для уже текстовых PDF рассмотрите библиотеки `pdfminer.six` или `PyMuPDF`.

---

**Happy coding!** Если это руководство помогло вам **extract pdf text OCR** для вашего проекта, поделитесь результатами в комментариях или откройте issue на GitHub‑странице Aspose OCR с предложениями по улучшению. Экспериментируйте, и скоро у вас будет надёжный конвейер, превращающий любой отсканированный PDF в поисковый, редактируемый текст.

## Что изучать дальше?

Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью рабочие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text Images – OCR Basics with Aspose.OCR for Java](/ocr/english/java/ocr-basics/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}