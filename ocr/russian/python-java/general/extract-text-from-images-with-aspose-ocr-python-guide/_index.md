---
category: general
date: 2026-03-18
description: Узнайте, как извлекать текст из изображений и преобразовывать текст сканированных
  изображений в редактируемые строки с помощью Aspose OCR в Python. Включён пошаговый
  код.
draft: false
keywords:
- extract text from images
- convert scanned images text
- Aspose OCR Python
- batch OCR processing
- image to text conversion
language: ru
og_description: Извлекайте текст из изображений с помощью Aspose OCR в Python. Этот
  учебник показывает, как преобразовать текст сканированных изображений всего за несколько
  строк кода.
og_title: Извлечение текста из изображений с помощью Aspose OCR – руководство по Python
tags:
- OCR
- Python
- Aspose
- Image Processing
title: Извлечение текста из изображений с помощью Aspose OCR – руководство по Python
url: /ru/python-java/general/extract-text-from-images-with-aspose-ocr-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из изображений с помощью Aspose OCR – Руководство на Python

Когда‑то вам нужно **извлечь текст из изображений**, но вы не знали, с чего начать? Вы не одиноки — разработчики постоянно сталкиваются с проблемой преобразования отсканированных PDF, шумных скриншотов или сфотографированных чеков в поисковые, редактируемые строки.  

Хорошая новость? С Aspose OCR для Python вы можете **массово конвертировать текст сканированных изображений**, не покидая свою IDE. В этом руководстве мы пройдём полный, готовый к запуску пример, показывающий, как это сделать, почему каждый шаг важен и на что обратить внимание.

## Что вы узнаете

- Как настроить библиотеку Aspose OCR в среде Python.  
- Как подготовить список файлов изображений (PNG, JPG, TIFF и т.д.).  
- Как выполнить пакетный OCR одним вызовом метода.  
- Как получить и отобразить извлечённый текст для каждого файла.  
- Как справиться с типичными подводными камнями, такими как неподдерживаемые форматы и использование памяти при больших файлах.  

К концу вы получите переиспользуемый скрипт, который может **извлекать текст из изображений** по запросу — идеально для автоматизации ввода данных, индексации документов или подачи в последующие NLP‑конвейеры.

---

![Extract text from images example](/images/ocr-extract-text.png "extract text from images")

*Текст альтернативы изображения: “извлечение текста из изображений с помощью Aspose OCR в Python”*

## Предварительные требования

- Python 3.8 или новее (в коде используются f‑строки).  
- Действительная лицензия Aspose OCR для Python или бесплатный пробный ключ.  
- Изображения, которые вы хотите обработать, хранятся локально (любая комбинация PNG, JPG или TIFF).  

Если у вас уже есть виртуальное окружение — отлично, если нет, создайте его с помощью:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate
```

Теперь вы готовы установить SDK.

## Шаг 1: Установить SDK Aspose OCR

Aspose распространяет свой OCR‑движок через PyPI, поэтому достаточно одной команды `pip`:

```bash
pip install aspose-ocr
```

> **Совет:** Зафиксируйте версию (например, `aspose-ocr==22.12`), чтобы избежать неожиданных несовместимостей в будущем.

## Шаг 2: Импортировать класс OCR‑движка

Основной класс, с которым вы будете работать, — `OcrEngine`. Импортируйте его в начале вашего скрипта:

```python
# Step 2: Import the OCR engine class
from asposeocr import OcrEngine
```

> *Почему это важно:* Импорт только необходимого снижает время запуска, особенно когда позже скрипт будет встроен в более крупное приложение.

## Шаг 3: Определить файлы изображений для обработки

Создайте список Python, содержащий полные пути ко всем изображениям, которые нужно просканировать. Замените `YOUR_DIRECTORY` на реальный путь к папке.

```python
# Step 3: Define the image files to be processed
image_files = [
    "YOUR_DIRECTORY/page1.png",
    "YOUR_DIRECTORY/page2.jpg",
    "YOUR_DIRECTORY/page3.tif"
]
```

> **Особый случай:** Если у вас сотни файлов, рассмотрите генерацию списка программно с помощью `glob.glob('*.png')`, чтобы не редактировать его вручную.

## Шаг 4: Выполнить OCR для всех изображений сразу

Aspose OCR предоставляет удобный метод `processMultiple`, который возвращает список объектов `OcrResult` — по одному для каждого входного файла.

```python
# Step 4: Run OCR on all images at once
ocr_engine = OcrEngine()               # instantiate the engine
ocr_results = ocr_engine.processMultiple(image_files)
```

> *Зачем пакетная обработка?* Обработка каждого изображения отдельно создаёт дополнительную нагрузку (инициализация движка, загрузка нативных библиотек). Пакетный вызов уменьшает нагрузку на CPU и ускоряет общую работу.

### Обработка ошибок без сбоев

Если изображение нельзя прочитать (повреждённый файл, неподдерживаемый формат), `processMultiple` выбросит исключение. Оберните вызов в блок `try/except`, чтобы скрипт не завершился аварийно:

```python
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as e:
    print(f"⚠️ OCR failed: {e}")
    ocr_results = []   # fallback to empty list
```

## Шаг 5: Вывести извлечённый текст для каждого файла

Пройдитесь по результатам, сопоставив каждый `OcrResult` с исходным именем файла. Метод `getText()` возвращает распознанную строку.

```python
# Step 5: Output the extracted text for each file
for index, result in enumerate(ocr_results, start=1):
    file_path = image_files[index - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")   # add a blank line for readability
```

### Ожидаемый вывод

Запуск полного скрипта на трёх простых скриншотах может дать примерно следующее:

```
--- Text from file YOUR_DIRECTORY/page1.png ---
Invoice #12345
Date: 2024‑07‑01
Total: $256.78

--- Text from file YOUR_DIRECTORY/page2.jpg ---
Welcome to the Annual Report
Prepared by: Finance Dept.

--- Text from file YOUR_DIRECTORY/page3.tif ---
© 2025 Acme Corp. All rights reserved.
```

Если в изображении нет распознаваемых символов, вы увидите пустую строку — ничего не ломается, и вы можете решить, помечать ли такой файл для ручной проверки.

## Бонус: Точная настройка точности OCR

Aspose OCR предлагает несколько необязательных параметров, с которыми стоит поэкспериментировать:

| Параметр | Что делает | Когда использовать |
|----------|------------|---------------------|
| `ocr_engine.setLanguage('eng')` | Принудительно задаёт модель английского языка (снижает количество ложных срабатываний). | В основном английские документы. |
| `ocr_engine.setResolution(300)` | Повышает точность при сканах с низким DPI. | Сканы ниже 200 dpi. |
| `ocr_engine.setPageSegMode('single_block')` | Рассматривает всё изображение как один блок текста. | Простые чеки или удостоверения личности. |

Эти строки можно добавить сразу после создания `ocr_engine`:

```python
ocr_engine.setLanguage('eng')
ocr_engine.setResolution(300)
ocr_engine.setPageSegMode('single_block')
```

## Распространённые подводные камни и как их избежать

1. **Большие TIFF‑стэки** — Многостраничный TIFF может потреблять гигабайты ОЗУ, если загрузить его полностью. Разбейте файл на отдельные страницы перед передачей в `processMultiple`.  
2. **Нелатинские скрипты** — Если нужно **извлекать текст из изображений**, содержащих кириллицу, арабский или китайский, измените код языка соответственно (`'rus'`, `'ara'`, `'chi_sim'`).  
3. **Пробелы в путях файлов** — Путь Windows с пробелами может вызвать `FileNotFoundError`. Оберните каждый путь в raw‑строку (`r"C:\My Folder\image.png"`) или используйте `os.path.abspath`.  

Устранение этих проблем заранее избавит вас от непонятных ошибок во время выполнения.

---

## Полный рабочий пример

Ниже представлен полностью готовый скрипт, который можно скопировать в файл `batch_ocr.py`. В нём учтены все рекомендации, обсуждённые выше.

```python
# batch_ocr.py
# -------------------------------------------------
# Complete example: extract text from images using Aspose OCR (Python)
# -------------------------------------------------

from asposeocr import OcrEngine
import os

# -------------------------------------------------
# Configuration – adjust these values for your environment
# -------------------------------------------------
IMAGE_DIR = "YOUR_DIRECTORY"   # <-- replace with your folder path
SUPPORTED_EXT = (".png", ".jpg", ".jpeg", ".tif", ".tiff")

# Build a list of image file paths automatically
image_files = [
    os.path.join(IMAGE_DIR, f)
    for f in os.listdir(IMAGE_DIR)
    if f.lower().endswith(SUPPORTED_EXT)
]

if not image_files:
    print("⚠️ No supported image files found in the specified directory.")
    exit(1)

# -------------------------------------------------
# Initialize OCR engine with optional tweaks
# -------------------------------------------------
ocr_engine = OcrEngine()
ocr_engine.setLanguage('eng')          # English language model
ocr_engine.setResolution(300)          # Boost low‑dpi accuracy
ocr_engine.setPageSegMode('single_block')  # Treat whole image as one block

# -------------------------------------------------
# Run batch OCR and handle potential errors
# -------------------------------------------------
try:
    ocr_results = ocr_engine.processMultiple(image_files)
except Exception as exc:
    print(f"❌ OCR processing failed: {exc}")
    ocr_results = []

# -------------------------------------------------
# Display extracted text
# -------------------------------------------------
for idx, result in enumerate(ocr_results, start=1):
    file_path = image_files[idx - 1]
    print(f"--- Text from file {file_path} ---")
    print(result.getText())
    print("\n")
```

Сохраните, активируйте виртуальное окружение и запустите:

```bash
python batch_ocr.py
```

Вы увидите извлечённые строки, выведенные в консоль, готовые к дальнейшей обработке (например, сохранению в базу данных или передаче в модель естественного языка).

---

## Заключение

В этом руководстве мы показали, как **извлекать текст из изображений** с помощью Aspose OCR для Python, охватив всё от установки до пакетной обработки и обработки ошибок. Скрипт компактен, полностью рабочий и легко расширяется — независимо от того, нужно ли вам **конвертировать текст сканированных изображений** в CSV‑файлы, наполнять поисковый индекс или просто автоматизировать ввод данных.

Готовы к следующему шагу? Попробуйте связать этот OCR‑конвейер с объединителем PDF, чтобы создавать поисковые PDF, или подключить его к триггеру облачного хранилища, чтобы каждый загруженный скан обрабатывался мгновенно. Возможности безграничны, а у вас теперь есть надёжная база для дальнейшего развития.

Есть вопросы или идеи по улучшению? Оставляйте комментарий ниже, и happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}