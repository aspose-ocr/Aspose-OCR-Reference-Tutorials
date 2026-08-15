---
category: general
date: 2026-03-28
description: Узнайте, как быстро выполнять OCR PDF с помощью Python. Это руководство
  покажет, как извлекать текст из PDF, распознавать текст в PDF и конвертировать отсканированный
  PDF в текст с использованием Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: ru
og_description: Освойте OCR PDF с помощью Python. Извлекайте текст из PDF, распознавайте
  текст в PDF и преобразуйте отсканированный PDF в текст за считанные минуты.
og_title: Как выполнить OCR PDF в Python – Полное руководство
tags:
- PDF
- OCR
- Python
- Aspose
title: Как выполнить OCR PDF в Python – пошаговое руководство
url: /ru/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как выполнять OCR PDF в Python – Пошаговое руководство

Когда‑то задавались вопросом **как выполнить OCR PDF**, если файл представляет собой просто изображение страницы? Вы не одиноки. В этом руководстве мы пройдем все шаги по OCR PDF‑файлов, извлечению текста из PDF и преобразованию отсканированного PDF в поисковый текст — все с помощью чистого кода на Python.

Мы охватим всё: от установки библиотеки Aspose OCR до получения распознанного текста с каждой страницы. К концу вы сможете **OCR PDF с Python**, **извлекать текст из PDF** и **преобразовывать отсканированный PDF в текст** без необходимости искать информацию в разных документах. Никакой лишней теории, только практический, готовый к запуску пример, который можно скопировать‑вставить.

## Что понадобится

Прежде чем начать, убедитесь, что у вас есть:

* Python 3.8+ (рекомендована последняя стабильная версия)  
* Лицензия Aspose OCR for Python или бесплатный trial‑ключ — их можно получить на сайте Aspose.  
* Отсканированный PDF, который нужно обработать (мы будем называть его `input.pdf`).  

Если всё уже готово — отлично, приступаем. Если нет, установка пакета займет считанные минуты, и мы покажем, как это сделать.

## Как выполнить OCR PDF — Настройка окружения

Первое, что нужно сделать, — получить модуль Aspose OCR на ваш компьютер. Пакет называется `aspose-ocr`, и его можно установить через pip:

```bash
pip install aspose-ocr
```

> **Совет:** используйте виртуальное окружение (`python -m venv venv`), чтобы зависимости оставались упорядоченными.

После установки пакета вы можете импортировать его и запустить OCR‑движок. Это фундамент для любого рабочего процесса **ocr pdf with python**, который вы будете строить дальше.

## OCR PDF с Python — Импорт Aspose OCR

Теперь, когда библиотека доступна, подключим её в наш скрипт. Мы также включим режим *direct PDF*, который заставляет Aspose читать байты PDF напрямую из файла, а не преобразовывать каждую страницу в изображение сначала.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Зачем использовать `PdfMode.DIRECT`? Потому что он пропускает дополнительный шаг растеризации, ускоряя процесс и сохраняет оригинальное расположение элементов — это особенно полезно, когда нужно **recognize text from PDF** с высокой точностью.

## Распознавание текста из PDF — Запуск движка

Когда движок готов, указываем ему наш отсканированный файл. Метод `recognize_from_pdf` делает всю тяжелую работу: он парсит каждую страницу, запускает OCR‑алгоритм и возвращает объект `OcrResult`, содержащий коллекцию объектов `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Если интересует, работает ли это с зашифрованными PDF — да, достаточно задать пароль через `ocr_engine.password = "secret"` перед вызовом `recognize_from_pdf`. Многие руководства упускают этот случай, но он часто нужен в реальных конвейерах.

## Извлечение текста из PDF — Доступ к результатам страниц

Список `ocr_result.pages` содержит одну запись на каждую страницу. Каждый объект `Page` имеет атрибут `.text`, в котором хранится обычный текст отсканированной страницы. Пройдемся по списку и выведем результаты, чтобы увидеть, что именно было извлечено.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Запуск скрипта выдаст примерно следующее:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Этот вывод подтверждает, что вы успешно **extract text from PDF** и **recognize text from PDF** с помощью Aspose OCR. Теперь полученные строки можно передать в базу данных, поисковый индекс или любой последующий NLP‑конвейер.

![пример как выполнить OCR PDF](placeholder-image.png "пример как выполнить OCR PDF")

*Текст alt‑изображения:* **пример как выполнить OCR PDF** — показывает вывод консоли с распознанным текстом по страницам.

## Преобразование отсканированного PDF в текст — Сохранение результата

Большинству разработчиков нужен не только вывод в консоль, а постоянный файл. Ниже небольшая вспомогательная функция, которая записывает текст каждой страницы в отдельный файл `.txt`, эффективно **convert scanned PDF to text** в папке `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

После завершения скрипта у вас будет аккуратная директория:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Теперь вы полностью **convert scanned PDF to text** и можете передать эти файлы в любой последующий процесс — поиск, аналитику или простой `grep`.

## Часто задаваемые вопросы и особые случаи

**Что делать, если в моём PDF есть изображения вместе с реальным текстом?**  
Aspose OCR попытается распознать всё, но ускорить процесс можно, отключив OCR для страниц, где уже есть выделяемый текст. Установите `ocr_engine.auto_detect_page_orientation = True` и затем вызывайте `ocr_engine.recognize_from_pdf(..., detect_text=False)` для известных «чистых» страниц.

**Можно ли управлять языковой моделью?**  
Конечно. Установите `ocr_engine.language = aocr.Language.English` (или любой поддерживаемый язык) перед вызовом `recognize_from_pdf`. Это повышает точность для неанглоязычных документов.

**Как обрабатывать очень большие PDF (100+ страниц)?**  
Разбивайте их на части. Метод `recognize_from_pdf` принимает параметр `page_range`, например `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Перебирайте диапазоны, чтобы снизить потребление памяти.

## Полный рабочий пример

Объединив всё вместе, получаем один скрипт, который можно сохранить в файл `ocr_pdf.py` и запустить:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Запустите его так:

```bash
python ocr_pdf.py
```

Вы увидите вывод в консоли, подтверждающий текст каждой страницы и путь к сохранённым файлам `.txt`.

## Заключение

Мы рассмотрели **как выполнить OCR PDF** с помощью Python, продемонстрировали чистый способ **ocr pdf with python**, показали, как **extract text from PDF**, объяснили механику **recognize text from PDF** и, наконец, предоставили готовый фрагмент кода, который **convert scanned PDF to text**. Весь процесс упакован

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}