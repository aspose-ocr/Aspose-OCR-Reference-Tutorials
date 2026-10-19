---
category: general
date: 2026-04-26
description: как использовать OCR для отсканированных PDF, извлекать текст из PDF,
  запускать OCR на PDF и преобразовывать отсканированный PDF в поисковые файлы за
  несколько шагов.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: ru
og_description: 'как использовать OCR в Python: узнайте, как извлекать текст из PDF,
  выполнять OCR на PDF и преобразовывать отсканированные PDF в документы, доступные
  для поиска.'
og_title: Как использовать OCR – Краткое руководство по извлечению текста из PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: как использовать OCR – извлекать текст из PDF с помощью Python
url: /ru/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# как использовать OCR – извлечение текста из PDF с помощью Python

Задумывались ли вы когда‑нибудь **как использовать OCR**, чтобы извлечь текст из отсканированного контракта, чека или электронной книги? Вы не одиноки. Во многих реальных проектах получаемый PDF представляет собой просто изображение, и без OCR вы не сможете искать, индексировать или анализировать его содержимое.  

В этом руководстве мы пройдем полный, готовый к запуску пример, который показывает **как использовать OCR**, как **извлекать текст из PDF**, и почему вам может понадобиться **конвертировать отсканированный PDF** в поисковые документы. Мы также рассмотрим тонкое искусство **загрузки PDF как изображения**, чтобы движок OCR мог чётко видеть каждую страницу.

> **Быстрый обзор:** К концу вы получите скрипт, который загружает многостраничный PDF, запускает OCR на каждой странице и выводит распознанный текст – без внешних сервисов.

## Что понадобится

- Python 3.9+ (подойдёт любая современная версия)
- пакет `aocr` (или любая совместимая OCR‑библиотека, предоставляющая `OcrEngine` и `Image.load`)
- отсканированный PDF‑файл, который нужно обработать (например, `contract.pdf`)
- умеренное количество ОЗУ (≈ 200 МБ на 100‑страничный PDF обычно достаточно)

Если вы ещё не установили библиотеку OCR, выполните:

```bash
pip install aocr
```

> **Pro tip:** Используйте виртуальное окружение, чтобы держать зависимости в порядке.

## Шаг 1: Загрузка PDF как изображения – первый кусок головоломки

Прежде чем OCR сможет работать, PDF должен быть представлен в виде изображения. Здесь в игру вступает вторичное ключевое слово **load pdf as image**.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Почему это важно:* `aocr.Image.load` внутренне растеризует каждую страницу PDF в bitmap, который понимает движок OCR. Если пропустить этот шаг и передать сырой PDF, движок выдаст ошибку, потому что ожидает пиксельные данные, а не векторные.

> **Note:** Путь может быть абсолютным или относительным. Убедитесь, что файл доступен для чтения; иначе вы получите `FileNotFoundError`.

## Шаг 2: Запуск OCR на PDF – превращение пикселей в символы

Теперь, когда PDF существует как изображение, мы наконец можем **run OCR on PDF**. Ниже приведён фрагмент, который обрабатывает все страницы за один проход:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*Что происходит «под капотом»?* `process_all_pages` перебирает растеризованные страницы, применяет модель OCR и возвращает список объектов‑результатов – по одному на страницу. Каждый результат содержит распознанный текст, оценки уверенности и ограничивающие рамки (если они понадобятся позже).

## Шаг 3: Извлечение текста из PDF – вытягивание строк

Имея результаты OCR, извлекать чистый текст становится тривиально. Мы пройдемся по страницам и выведем результат, демонстрируя вторичное ключевое слово **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Ожидаемый вывод** (усечённый для краткости):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Если нужен текст в одной строке, просто объедините его:

```python
full_text = "\n".join(r.text for r in page_results)
```

Теперь вы успешно **extracted text from PDF** с помощью OCR.

## Шаг 4: Конвертация отсканированного PDF – делаем его поисковым

Многие downstream‑инструменты (например, Elasticsearch или SharePoint) ожидают поисковый PDF, а не просто дамп текста. Вы можете внедрить вывод OCR обратно в оригинальный PDF, эффективно **convert scanned PDF** в поисковую версию.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Зачем это нужно?* Поисковый PDF сохраняет оригинальное расположение и изображения, одновременно позволяя выделять текст и индексировать его – выгода и для людей, и для машин.

## Общие подводные камни и граничные случаи

### Многостраничные PDF, превышающие память

Если ваш PDF содержит сотни страниц, загрузка всего сразу может исчерпать ОЗУ. Библиотека `aocr` поддерживает ленивую загрузку:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Затем обрабатывайте страницы по одной:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Сканирование низкого качества

Точность OCR резко падает на размытых или низкоконтрастных сканах. Прежде чем передать изображение движку, рассмотрите предобработку:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Поддержка языков

По умолчанию движок предполагает английский. Чтобы **run OCR on PDF** на другом языке, укажите код языка:

```python
ocr_engine.language = "spa"  # Spanish
```

Убедитесь, что соответствующая языковая модель установлена.

## Полный рабочий пример

Собрав всё вместе, получаем автономный скрипт, который можно сохранить в файл `ocr_pdf.py` и сразу запустить:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Запустите его так:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Вы увидите текст, выведенный в консоль, а если указали `-o`, рядом с оригиналом появится поисковый PDF.

## Pro Tips & Best Practices

- **Batch processing:** При обработке десятков PDF оберните вышеописанную логику в цикл и логируйте успех/неудачу каждого файла.
- **Confidence filtering:** Каждый `page_result` содержит метрику уверенности. Отбрасывайте или помечайте страницы с низкой уверенностью для ручной проверки.
- **Parallelism:** Если ваш CPU имеет несколько ядер, рассмотрите использование `concurrent.futures` для параллельной обработки страниц – только следите за использованием памяти.
- **Version lock:** API `aocr` может изменяться. Зафиксируйте версию в `requirements.txt` (например, `aocr==2.3.1`), чтобы избежать ломающих изменений.

## Заключение

Мы прошли путь от **how to use OCR** до **extract text from PDF**, **run OCR on PDF**, **load PDF as image** и даже **convert scanned PDF** в поисковый формат. Код полностью готов, объяснения охватывают как *что*, так и *почему*, и теперь у вас есть переиспользуемый шаблон для любого проекта, работающего с PDF‑файлами, основанными на изображениях.

Что дальше? Попробуйте передать извлечённый текст в конвейер обработки естественного языка, индексировать поисковые PDF в Elasticsearch или поэкспериментировать с другими OCR‑бэкендами, такими как Tesseract или Azure Computer Vision. Возможности безграничны, а инструменты уже у вас под рукой.

Счастливого кодинга, и пусть ваши PDF всегда будут поисковыми! 

![пример использования OCR](/images/ocr_workflow.png "как использовать OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}