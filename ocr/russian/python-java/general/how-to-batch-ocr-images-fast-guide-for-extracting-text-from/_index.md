---
category: general
date: 2026-01-12
description: Как быстро выполнять пакетное OCR изображений и извлекать текст из JPEG‑файлов
  в Python. Узнайте пошаговую пакетную обработку с полным исполняемым примером.
draft: false
keywords:
- how to batch OCR images
- extract text from JPEG files
language: ru
og_description: Как пакетно выполнять OCR изображений и извлекать текст из файлов
  JPEG. Это руководство проведёт вас через готовое к запуску решение на Python.
og_title: Как пакетно выполнять OCR изображений — быстрый учебник по Python
tags:
- OCR
- Python
- image processing
title: Как пакетно выполнять OCR изображений – быстрый гид по извлечению текста из
  JPEG‑файлов
url: /ru/python-java/general/how-to-batch-ocr-images-fast-guide-for-extracting-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как пакетно выполнять OCR изображений – Быстрое руководство по извлечению текста из JPEG файлов

Когда‑нибудь задавались вопросом **how to batch OCR images** без написания отдельного скрипта для каждого файла? Вы не одиноки. Во многих проектах — сканирование счетов, оцифровка архивов или модерация контента — нам нужно извлекать текст из десятков или сотен JPEG‑файлов за один раз. Хорошая новость: это можно сделать всего несколькими строками Python, получив переиспользуемый движок, который можно вставить в любой конвейер.

В этом руководстве мы покажем вам точно **how to batch OCR images**, а затем пройдёмся по извлечению текста из JPEG‑файлов, обработке граничных случаев и проверке результата. К концу вы получите автономный скрипт, который можно запустить для любой папки с изображениями, и поймёте, почему пакетная обработка важна для производительности и поддерживаемости.

## Что вы узнаете

- Настроить простой OCR‑движок и сконфигурировать его для английского языка.  
- Собрать все JPEG‑файлы из каталога с помощью `pathlib`.  
- Вызвать OCR‑движок один раз для обработки всей партии.  
- Показать предварительный просмотр распознанного текста для каждого изображения.  
- Советы по работе с большими партиями, разными языками и типичными подводными камнями.

**Prerequisites**: Python 3.8+, библиотека `ocr` (или любой совместимый обёртка), и папка с JPEG‑изображениями, которые вы хотите проанализировать. Внешние сервисы не требуются — всё работает локально.

---

## Step 1: Initialise the OCR Engine – The Core of How to Batch OCR Images

Прежде чем мы сможем **batch OCR images**, нам нужен движок, умеющий читать текст. В большинстве библиотек вы создаёте объект движка, при необходимости задаёте язык и затем переиспользуете его для каждого файла.

```python
import ocr
import pathlib

# Create the OCR engine and set it to English (the most common case)
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

*Why this matters*: Инициализация движка один раз избавляет от накладных расходов на повторную загрузку языковых моделей. Это также даёт единственное место для настройки параметров (например, DPI, whitelist символов), которые будут применяться ко всей партии.

> **Pro tip**: Если вы планируете обрабатывать многоязычные документы, замените `ocr.Language.ENGLISH` на `ocr.Language.MULTI` или загрузите несколько языковых пакетов перед началом партии.

## Step 2: Gather All JPEG Files – The “Extract Text from JPEG Files” Part

Теперь, когда движок готов, нам нужно указать, какие изображения обрабатывать. Использование `pathlib` делает код независимым от платформы и лаконичным.

```python
# Replace YOUR_DIRECTORY with the path that holds your JPEG files
image_dir = pathlib.Path("YOUR_DIRECTORY/")
image_paths = list(image_dir.glob("*.jpg"))  # only JPEG files, case‑sensitive
```

*Why this matters*: Сначала собирая список файлов, мы можем передать всю коллекцию OCR‑движку одним вызовом — именно то, о чём говорит “how to batch OCR images”. Если у вас есть вложенные папки, вы можете изменить `glob("**/*.jpg")` на рекурсивный поиск.

> **Edge case**: Если ваши изображения имеют смешанные расширения (`.jpeg`, `.JPG`), расширьте шаблон glob: `image_dir.rglob("*.[jJ][pP][eE]?g")`.

## Step 3: Process the Whole Batch in One Call – The Real Power of Batch OCR

Большинство современных OCR‑библиотек предоставляют метод `process_batch` (или аналогичный), принимающий итерируемый объект путей к файлам. Это сердце **how to batch OCR images** эффективно.

```python
# Process every JPEG file in a single batch operation
ocr_results = ocr_engine.process_batch(image_paths)
```

*Why this matters*: Один пакетный вызов уменьшает количество переходов Python‑to‑C, держит языковую модель в памяти и часто позволяет внутреннюю параллелизацию. Результатом является список объектов — каждый содержит распознанный текст и оценки уверенности.

> **Performance note**: Для очень больших партий (тысячи изображений) рассмотрите разбивку списка на более мелкие части (например, по 200 файлов), чтобы избежать избыточного потребления памяти.

## Step 4: Show a Preview of the Extracted Text – Quick Validation

После завершения партии полезно взглянуть на первые несколько символов каждого результата. Это помогает убедиться, что OCR действительно извлекает текст из ваших JPEG‑файлов.

```python
for image_path, ocr_result in zip(image_paths, ocr_results):
    # Show the image name and the first 100 characters of its recognised text
    preview = ocr_result.text[:100].replace("\n", " ").strip()
    print(f"{image_path.name}: {preview}...")
```

*Why this matters*: Краткий предварительный просмотр позволяет быстро обнаружить очевидные сбои (например, пустой вывод, искажённые символы) без открытия каждого файла. Если вы заметите систематические проблемы, можно скорректировать настройки движка и повторно запустить партию.

> **Common pitfall**: Забвение удалить символы новой строки может сделать превью «грязным». Строка `replace("\n", " ")` очищает его.

## Full Working Example – All Steps Combined

Ниже представлен полный скрипт, который вы можете скопировать‑вставить, скорректировать путь к каталогу и запустить. Он демонстрирует весь рабочий процесс **how to batch OCR images** от начала до конца.

```python
import ocr
import pathlib

def batch_ocr_jpeg(folder: str):
    """
    Process all JPEG files in `folder` and print a 100‑character preview
    of the recognised text for each image.
    """
    # Step 1 – Initialise OCR engine
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ENGLISH

    # Step 2 – Gather JPEG paths
    img_dir = pathlib.Path(folder)
    jpeg_paths = list(img_dir.glob("*.jpg"))  # add more patterns if needed

    if not jpeg_paths:
        print("No JPEG files found in the specified directory.")
        return

    # Step 3 – Batch process
    results = engine.process_batch(jpeg_paths)

    # Step 4 – Display previews
    for path, res in zip(jpeg_paths, results):
        preview = res.text[:100].replace("\n", " ").strip()
        print(f"{path.name}: {preview}...")

if __name__ == "__main__":
    # Replace with the path containing your JPEG images
    batch_ocr_jpeg("YOUR_DIRECTORY/")
```

**Expected output** (sample):

```
invoice_001.jpg: Invoice #001  Date: 2024-03-15  Total: $1,245.00  Bill To: Acme Corp...
receipt_202.jpg: Receipt 202  Store: QuickMart  Total: $45.67  Date: 03/12/2024...
...
```

Если превью показывает осмысленный текст, вы успешно **extracted text from JPEG files** с использованием пакетного подхода.

## Handling Large Batches and Advanced Scenarios

### Chunking Large Workloads
При работе с тысячами изображений память может стать узким местом. Разбейте список на более мелкие части:

```python
from itertools import islice

def chunked(iterable, size):
    it = iter(iterable)
    while True:
        chunk = list(islice(it, size))
        if not chunk:
            break
        yield chunk

for chunk in chunked(jpeg_paths, 200):  # 200 files per batch
    results = engine.process_batch(chunk)
    # process results as shown earlier
```

### Switching Languages
Если ваши документы содержат французский или испанский, измените язык перед запуском партии:

```python
engine.language = ocr.Language.FRENCH  # or ocr.Language.SPANISH
```

### Saving Results to Disk
Вместо вывода в консоль вы можете записать каждый OCR‑результат в файл `.txt`:

```python
output_dir = pathlib.Path("ocr_output")
output_dir.mkdir(exist_ok=True)

for path, res in zip(jpeg_paths, results):
    txt_path = output_dir / f"{path.stem}.txt"
    txt_path.write_text(res.text, encoding="utf-8")
```

## Conclusion

Теперь вы знаете **how to batch OCR images** и надёжно **extract text from JPEG files** с помощью компактного Python‑скрипта. Инициализировав движок один раз, собрав все пути к JPEG, обработав их одной пакетной операцией и просмотрев результат, вы получаете и скорость, и простоту. Далее вы можете расширять процесс — добавить поддержку нескольких языков, сохранять результаты в базе данных или интегрировать скрипт в более крупный конвейер обработки документов.

Готовы к следующему шагу? Попробуйте заменить библиотеку `ocr` на Tesseract, поэкспериментировать с различными предобработками изображений (пороговая обработка, изменение размера) или передать извлечённый текст в модель natural‑language‑processing для автоматической категоризации. Возможности безграничны, а у вас уже есть надёжный фундамент для дальнейшего развития.

Happy coding, and may your OCR batches always be error‑free!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}