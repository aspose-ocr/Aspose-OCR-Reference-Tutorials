---
category: general
date: 2026-06-25
description: Извлекайте текст из изображений с помощью библиотеки Python aocr — изучите
  пакетный OCR, установите режим распознавания «печать» и добавьте AI‑постпроцессор.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: ru
og_description: Извлекайте текст из изображений с помощью библиотеки Python aocr.
  Этот учебник демонстрирует пакетный OCR, режим распознавания печатного текста и
  необязательный AI‑постпроцессор.
og_title: Извлечение текста из изображений в Python – Полное руководство по пакетной
  обработке aocr
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Извлечение текста из изображений в Python с помощью aocr OCR Batch
url: /ru/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображений в Python с помощью aocr OCR Batch

Когда‑то вам нужно было **извлечь текст из изображений**, но вы чувствовали себя подавлённым из‑за десятков мелких шагов? Вы не одиноки. Будь то оцифровка сканированных форм, извлечение данных из чеков или создание поискового архива, получение надёжных результатов OCR в масштабе может ощущаться как подъём к крутому холму.

Хорошая новость? С **библиотекой aocr** вы можете запустить полноценный **Python OCR batch** всего в несколько строк. В этом руководстве мы пройдёмся по созданию OCR‑батча, загрузке всех поддерживаемых изображений из папки, выбору правильного **режима распознавания printed**, а также подключению **AI‑постпроцессора** для дополнительного повышения точности. К концу вы получите готовый к запуску скрипт, который извлекает текст из изображений и сообщает, сколько символов было получено для каждого файла.

## Что вы узнаете

- Как установить и импортировать пакет `aocr`.
- Как настроить `OcrBatch` для автоматической обработки тысяч файлов.
- Как выбрать оптимальный режим распознавания для печатных документов.
- (Опционально) Как подключить AI‑постпроцессор для очистки шумных результатов.
- Как вывести путь к каждому файлу вместе с длиной извлечённого текста.
- Советы по обработке крайних случаев, таких как неподдерживаемые форматы или пустые страницы.

### Предпосылки

- Python 3.8 или новее, установленный на вашем компьютере.  
- Базовое знакомство с написанием скриптов на Python (циклы, импорты и т.д.).  
- Доступ к папке со сканированными изображениями (PNG, JPG, TIFF и др.).  

Если всё это у вас есть, давайте начнём — внешних сервисов не требуется.

## Шаг 1: Установите библиотеку aocr

Сначала. Пакет `aocr` не входит в стандартную библиотеку, поэтому его нужно установить из PyPI.

```bash
pip install aocr
```

> **Pro tip:** Используйте виртуальное окружение (`python -m venv .venv`), чтобы изолировать зависимости.  

После установки вы можете импортировать основные классы.

```python
# core imports
import aocr
```

## Шаг 2: Создайте экземпляр OCR‑батча

`OcrBatch` — это «рабочая лошадка», которая будет обходить ваш каталог и отслеживать каждый файл‑изображение. Представьте её как конвейер, подающий картинки в OCR‑движок.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

На данный момент батч пуст, но мы заполним его на следующем шаге.

## Шаг 3: Добавьте все поддерживаемые изображения из папки (рекурсивно)

Вероятно, у вас вложенная структура папок — возможно, одна подпапка на клиента или месяц. Метод `add_folder` обходит дерево за вас, подбирая каждое изображение, которое умеет читать движок.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Замените `"YOUR_DIRECTORY/scanned_forms/"` реальным путём на вашей системе. После этого вызова `ocr_batch.file_paths` будет содержать список абсолютных имён файлов, а батч точно знает, сколько элементов ему предстоит обработать.

## Шаг 4: Выберите режим распознавания для печатного текста

Движок `aocr` поддерживает несколько режимов (handwritten, printed, mixed). Поскольку мы работаем с чистыми печатными формами, задаём соответствующий режим. Этот небольшой флаг может существенно повысить точность, потому что движок пропускает тяжёлые эвристики, необходимые для курсивных шрифтов.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Почему это важно:** Печатный текст имеет одинаковые базовые линии и формы символов, позволяя модели OCR применять более строгие словари символов. Если оставить режим «auto», вы можете получить лишний шум на сканах низкого разрешения.

## Шаг 5: (Опционально) Подключите AI‑постпроцессор

Если ваши сканы страдают от размытия, низкого контраста или необычных шрифтов, AI‑постпроцессор может очистить сырые OCR‑результаты перед передачей их дальше. Метод `set_ai_postprocessor` ожидает объект, реализующий интерфейс `process(text: str) -> str`.

Ниже минимальный пример с вымышленным классом `SimpleCleaner`. На практике вы можете подключить трансформер HuggingFace, собственную языковую модель или даже правило‑ориентированный проверщик орфографии.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Если пропустить этот шаг, батч просто вернёт необработанные строки OCR.

## Шаг 6: Запустите OCR для всего батча и соберите результаты

Теперь начинается тяжёлая работа. Метод `run` проходит по каждому файлу, запускает OCR‑движок, пропускает вывод через опциональный AI‑постпроцессор и возвращает список строк — по одной на каждое изображение.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Поскольку метод возвращает обычный список Python, вы можете обращаться с ним как с любой другой коллекцией — сохранять, записывать в CSV или загружать в базу данных.

## Шаг 7: Выведите каждый путь к файлу вместе с длиной извлечённого текста

Быстрая проверка — вывести, сколько символов было извлечено из каждого файла. Если страница пустая или OCR не сработал, вы увидите длину `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

Типичный вывод выглядит так:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Наличие `0` сразу подсказывает, какие файлы требуют дополнительного внимания (возможно, они повреждены или вовсе не являются изображениями).

## Обработка распространённых крайних случаев

### 1. Неподдерживаемые типы файлов

`aocr` тихо пропускает файлы, которые не может декодировать. Если подозреваете, что в папке есть PDF или BMP, отфильтруйте их заранее:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Большие батчи и потребление памяти

Обработка тысяч сканов высокого разрешения может сильно увеличить использование памяти. Снизьте нагрузку, обрабатывая данные порциями:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Пустые или низкоконтрастные страницы

Если страница выдаёт менее 10 символов, вы можете пометить её для ручной проверки:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Полный рабочий пример

Собрав всё вместе, получаем скрипт, который можно скопировать‑вставить и сразу запустить. Сохраните его как `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Ожидаемый вывод** (усечённый для краткости):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Запустите его так:

```bash
python batch_ocr.py
```

Если всё настроено правильно, вы увидите строку для каждого изображения, каждая из которых сообщает количество символов извлечённого текста.

## Часто задаваемые вопросы

**В: Работает ли это с PDF?**  
О: Не «из коробки». `aocr` обрабатывает только растровые изображения. Сначала конвертируйте PDF в PNG/TIFF (например, с помощью `pdf2image`).

**В: Можно ли переключить режим распознавания на рукописный?**  
О: Конечно — просто замените `aocr.RecognitionMode.PRINTED` на `aocr.RecognitionMode.HANDWRITTEN`. Ожидайте более медленное выполнение, но лучшие результаты для курсивных заметок.

**В: Что делать, если нужна многоязычная поддержка?**  
О: Библиотека поставляется с языковыми пакетами. Установите нужный модуль (`pip install aocr-lang-fr` для французского и т.д.) и задайте `ocr_batch.language = "fr"` перед запуском.

## Следующие шаги и связанные темы

- **Параллельная обработка:** Оберните выполнение батча в `concurrent.futures.ThreadPoolExecutor`, чтобы задействовать несколько ядер CPU.  
- **Сохранение результатов:** Запишите `ocr_results` в CSV или SQLite‑базу для последующего анализа.  
- **Интеграция с облачным AI:** Замените `SimpleCleaner` на трансформер‑модель из HuggingFace для передовой коррекции орфографии.  
- **Тонкая настройка aocr:** Если у вас есть собственный набор шрифтов, изучите `aocr.Trainer` для повышения точности режима printed.

---

Это всё — теперь у вас есть надёжный фундамент


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Извлечение текста из изображения с помощью Aspose OCR – пошаговое руководство](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Извлечение текста из изображений с использованием OCR‑операции по папкам](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Как пакетно выполнять OCR изображений со списком в Aspose.OCR для .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}