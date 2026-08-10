---
category: general
date: 2026-06-06
description: Извлекайте текст из изображений PDF с помощью Python OCR. Узнайте, как
  быстро преобразовать отсканированные документы в текст с помощью асинхронного пакетного
  распознавания.
draft: false
keywords:
- extract text from images pdf
- convert scanned documents to text
- python ocr batch processing
- asynchronous OCR python
- image to text conversion
language: ru
og_description: Извлекать текст из изображений PDF с помощью Python. Это пошаговое
  руководство показывает, как преобразовать отсканированные документы в текст с использованием
  асинхронного OCR.
og_title: Извлечение текста из PDF‑изображений – учебник по OCR на Python
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Extract text from images pdf using Python OCR. Learn how to convert
    scanned documents to text quickly with async batch recognition.
  headline: Extract Text from Images PDF – Python Guide to Convert Scanned Documents
    to Text
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
- Text Extraction
title: Извлечение текста из PDF‑изображений – руководство на Python по конвертации
  отсканированных документов в текст
url: /ru/python-java/general/extract-text-from-images-pdf-python-guide-to-convert-scanned/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из PDF‑изображений – Руководство Python по конвертации отсканированных документов в текст

Когда‑нибудь вам нужно было **извлечь текст из PDF‑изображений** без траты часов на переписывание? В этом руководстве мы покажем, как **конвертировать отсканированные документы в текст** с помощью простого асинхронного OCR‑рабочего процесса на Python.  

Если вы когда‑либо смотрели на стопку отсканированных PDF и думали: «Должен быть более быстрый способ», вы попали по адресу. Мы пройдемся по каждой строке кода, объясним, почему каждый элемент важен, и даже рассмотрим несколько крайних случаев, с которыми вы можете столкнуться.

## Что вы узнаете

- Как запустить OCR‑движок и задать язык распознавания.  
- Как передать смешанный список PNG‑файлов и PDF‑документов в пакетный распознаватель.  
- Как выполнять OCR‑задачу асинхронно, чтобы приложение оставалось отзывчивым.  
- Как собрать результаты, сопоставить их с исходными файлами и вывести чистый текст.  

**Prerequisites**: Python 3.8+, базовое понимание `asyncio` или `concurrent.futures`, и OCR‑библиотека, предоставляющая класс `OcrEngine`, аналогичный примеру (например, Aspose.OCR, обёртка Tesseract или собственная обёртка). Никакой сложной настройки не требуется — просто установите библиотеку и вы готовы к работе.

![извлечение текста из PDF‑изображений](https://example.com/placeholder.png "Скриншот вывода OCR – извлечение текста из PDF‑изображений")

## Извлечение текста из PDF‑изображений – Настройка OCR‑движка

Первое, что вам нужно, — это экземпляр OCR‑движка, сконфигурированный под язык ваших документов. В нашем случае мы используем французский, но вы можете заменить его любым поддерживаемым языком.

```python
# Import the OCR library – replace with your actual import
from ocr import OcrEngine, Language

# Step 1: Create and configure the OCR engine
engine = OcrEngine()
engine.set_recognition_language(Language.FRENCH)   # Change to Language.ENGLISH, etc.
```

**Почему это важно**: Установка языка заранее значительно повышает точность. Движок использует языко‑специфичные словари и модели символов; передача неверного языка — частая причина искажённого вывода.

## Подготовка списка файлов – Изображения и PDF вместе

Наш пакетный распознаватель умеет работать как с растровыми изображениями (`.png`, `.jpg`), так и с PDF‑контейнерами. Просто передайте обычный Python‑список путей к файлам.

```python
# Step 2: Define the files to be processed (use your own directory)
files = [
    "YOUR_DIRECTORY/doc1.png",
    "YOUR_DIRECTORY/doc2.png",
    "YOUR_DIRECTORY/doc3.pdf"
]
```

**Tip**: Держите список плоским; движок внутренне распакует каждую страницу PDF в изображения перед распознаванием. Если у вас тысячи файлов, разбейте список на более мелкие партии, чтобы избежать всплесков памяти.

## Запуск асинхронного пакетного распознавания

Вместо блокировки основного потока мы запускаем OCR‑задачу в фоне. Метод возвращает `Future`, который в итоге будет содержать список объектов `OcrResult`.

```python
# Step 3: Start asynchronous batch recognition
future = engine.recognize_batch_async(files)   # returns a Future[List[OcrResult]]
```

**Как это работает**: Под капотом движок создаёт пул потоков (или асинхронную задачу, в зависимости от реализации). Это позволяет вам продолжать выполнять другую работу — обновлять UI, загружать новые файлы или вести журнал прогресса — пока тяжёлая обработка происходит в другом месте.

## Делайте что‑то полезное, пока работает OCR

Распространённая ошибка — сидеть без дела и опрашивать `Future` в плотном цикле. Вместо этого можно выполнять любую несвязанную работу. Для демонстрации мы просто выведем строку статуса.

```python
# Step 4: Perform other work while OCR runs
print("Batch started – doing other work...")
# Imagine you could be uploading files, sending heartbeats, etc.
```

## Сбор результатов после завершения `Future`

Когда вы готовы собрать вывод OCR, используйте `as_completed` из `concurrent.futures`. Этот шаблон работает как с одним `Future`, так и с множеством.

```python
from concurrent.futures import as_completed

# Step 5: Wait for the batch to finish and retrieve the results
for completed in as_completed([future]):
    ocr_results = completed.result()   # List[OcrResult] in the same order as `files`
    for path, result in zip(files, ocr_results):
        print(f"{path} →\n{result.text}\n")
```

**Что вы увидите**: Каждый путь к файлу, за которым следует извлечённое представление в виде обычного текста. Для PDF `result.text` содержит конкатенированный текст всех страниц.

### Ожидаемый вывод (пример)

```
YOUR_DIRECTORY/doc1.png →
Bonjour, ceci est un test d’OCR.

YOUR_DIRECTORY/doc2.png →
Le texte de la deuxième image apparaît ici.

YOUR_DIRECTORY/doc3.pdf →
Page 1 du PDF : Lorem ipsum dolor sit amet…
Page 2 du PDF : Consectetur adipiscing elit…
```

Если вы заметили пропущенные символы, дважды проверьте, что выбранный язык совпадает с языком документа, и рассмотрите предварительную обработку изображений (выравнивание, увеличение контраста) перед передачей их в движок.

## Обработка крайних случаев и распространённых подводных камней

| Ситуация | Что делать |
|-----------|------------|
| **Смешанные языки** | Сначала выполните определение языка, затем создайте отдельные движки для каждого языка. |
| **Большие PDF (> 100 MB)** | Разбейте PDF на отдельные страницы на диске (например, с помощью `PyPDF2`) и передавайте их как отдельные записи. |
| **Нелатинские скрипты** | Убедитесь, что OCR‑библиотека содержит необходимый языковой пакет; некоторые библиотеки требуют загрузки дополнительных файлов данных. |
| **Узкое место в производительности** | Увеличьте размер пула потоков (`engine.set_thread_pool_size(8)`) или переключитесь на GPU‑ускоренный бекенд, если он доступен. |
| **Отсутствие текста в изображениях низкого разрешения** | Предобработайте с помощью OpenCV: `cv2.resize`, `cv2.threshold` и `cv2.medianBlur` для улучшения читаемости. |

## Полный рабочий пример (готовый к копированию)

```python
# ------------------------------------------------------------
# Full script: extract text from images pdf – async OCR batch
# ------------------------------------------------------------
import os
from concurrent.futures import as_completed
# Replace the import below with the actual OCR library you use
from ocr import OcrEngine, Language, OcrResult

def main():
    # 1️⃣ Initialize OCR engine
    engine = OcrEngine()
    engine.set_recognition_language(Language.FRENCH)   # Change as needed

    # 2️⃣ Build list of files (images + PDFs)
    base_dir = "YOUR_DIRECTORY"
    files = [
        os.path.join(base_dir, "doc1.png"),
        os.path.join(base_dir, "doc2.png"),
        os.path.join(base_dir, "doc3.pdf")
    ]

    # 3️⃣ Launch async batch recognition
    future = engine.recognize_batch_async(files)

    # 4️⃣ Do other work – here we just print a placeholder
    print("Batch started – doing other work...")

    # 5️⃣ Retrieve results when ready
    for completed in as_completed([future]):
        ocr_results = completed.result()   # List[OcrResult]
        for path, result in zip(files, ocr_results):
            print(f"{path} →\n{result.text}\n")

if __name__ == "__main__":
    main()
```

Сохраните этот файл как `extract_text_async.py`, замените `YOUR_DIRECTORY` на путь к вашим файлам, установите OCR‑пакет (`pip install your-ocr-lib`) и запустите `python extract_text_async.py`. Вы должны увидеть консольный вывод, показанный ранее.

## Следующие шаги – Выход за рамки базового извлечения

- **Post‑processing**: Удаляйте лишние пробелы, нормализуйте Unicode (`unicodedata.normalize`) или запускайте проверку орфографии, чтобы очистить шум OCR.  
- **Структурированный вывод**: Экспортируйте результаты в CSV, JSON или напрямую в базу данных для последующего поиска.  
- **Параллельные партии**: Если у вас сотни файлов, запустите несколько `Future` и используйте очередь, чтобы держать CPU занятым, не перегружая память.  
- **Интеграция с веб‑фреймворками**: Подключите этот скрипт к эндпоинту Flask или FastAPI, чтобы предоставлять OCR‑услугу по запросу.

---

### TL;DR

Теперь вы знаете, как **извлекать текст из PDF‑изображений** с помощью минимального Python‑скрипта, который запускает OCR асинхронно, позволяя **конвертировать отсканированные документы в текст**, пока ваша программа остаётся отзывчивой. Поэкспериментируйте с настройками языка, размерами партий и приёмами предобработки, чтобы достичь максимальной точности.

Есть свой подход, которым хотите поделиться — может, OCR рукописных заметок или облачный сервис? Оставьте комментарий, и счастливого кодинга!

## Что стоит изучить дальше?

Следующие учебники охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом руководстве. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в ваших проектах.

- [Извлечение текста из изображения с Aspose OCR – Пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображений с помощью OCR‑операции по папкам](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Извлечение текста из изображений с Aspose.OCR – Разрешённые символы](/ocr/english/java/advanced-ocr-techniques/specify-allowed-characters/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}