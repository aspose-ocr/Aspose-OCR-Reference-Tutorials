---
category: general
date: 2026-06-16
description: Извлекайте текст из файлов TIFF с помощью Python OCR. Узнайте, как пошагово
  преобразовать TIFF в текст, легко обрабатывая многостраничные документы.
draft: false
keywords:
- extract text from tiff
- convert tiff to text
- Python OCR multi‑page TIFF
- OCR language settings
- OCR engine Python
language: ru
og_description: Извлекайте текст из файлов TIFF с помощью OCR на Python. Следуйте
  этому руководству, чтобы преобразовать TIFF в текст, работать с многостраничными
  сканами и получать чистые результаты.
og_title: Извлечение текста из TIFF – Полное руководство по Python
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  headline: Extract Text from TIFF – Complete Python Guide
  type: TechArticle
- description: Extract text from TIFF files using Python OCR. Learn how to convert
    TIFF to text step‑by‑step, handling multi‑page documents with ease.
  name: Extract Text from TIFF – Complete Python Guide
  steps:
  - name: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
    text: '**Batch conversion** – Wrap the whole flow in a function `def ocr_tiff(path):`
      and iterate over a directory of TIFF files.'
  - name: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
    text: '**Output to files** – Instead of printing, write each page’s text to `page_{i}.txt`
      or concatenate everything into a single document.'
  - name: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
    text: '**Alternative OCR engines** – If you need higher accuracy, swap `ocr.OcrEngine()`
      for Tesseract (`pytesseract`) or Azure Cognitive Services—just keep the same
      “extract text from TIFF” logic.'
  - name: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
    text: '**Post‑processing** – Run spell‑check, language detection, or regex cleanup
      to tidy up the raw OCR output.'
  type: HowTo
tags:
- OCR
- Python
- TIFF
- Text extraction
title: Извлечение текста из TIFF — Полное руководство по Python
url: /ru/python-java/general/extract-text-from-tiff-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Извлечение текста из TIFF – Полное руководство на Python

Когда‑то вам нужно было **извлечь текст из TIFF**‑изображений, но вы не знали, с чего начать? Вы не одиноки — многие разработчики сталкиваются с этой проблемой при работе со сканированными архивами или устаревшими документами. Хорошая новость: с несколькими строками кода на Python вы можете **конвертировать TIFF в текст** мгновенно, даже если файл содержит десятки страниц.

В этом руководстве мы пройдем реальный пример: загрузим многостраничный TIFF, зададим язык OCR — французский, и получим распознанный текст с каждой страницы. К концу вы получите готовый к запуску скрипт, поймёте, зачем нужен каждый шаг, и узнаете, как адаптировать его под другие языки или форматы изображений.

## Предварительные требования

Прежде чем начать, убедитесь, что у вас есть:

- Python 3.8 или новее.
- Пакет `ocr` (или любой совместимый OCR‑библиотека, предоставляющая класс `OcrEngine`). Установить его можно командой `pip install ocr-lib` — замените название пакета на то, которое используете.
- Многостраничный TIFF‑файл (например, `french-scans.tif`), который нужно обработать.
- Базовые навыки написания скриптов на Python.

Никаких тяжёлых зависимостей, никаких внешних сервисов — только чистый Python и OCR‑движок.

---

## Шаг 1: Настройка OCR‑движка для **извлечения текста из TIFF**

Сначала нам нужен экземпляр OCR‑движка, и нужно указать, какой язык использовать. В нашем случае исходный материал на французском, поэтому задаём соответствующий язык.

```python
import ocr  # Replace with the actual import if your OCR library uses a different name

# Create the OCR engine
engine = ocr.OcrEngine()

# Tell the engine to look for French characters
engine.language = ocr.Language.FRENCH
```

**Почему это важно:**  
Настройка языка значительно повышает точность. Французские символы вроде «é» или «ç» будут распознаваться как произвольные знаки, если движок по умолчанию использует английский. Явно указав французский, мы предоставляем правильную карту символов.

> **Совет:** Если вы обрабатываете документы на нескольких языках, можете менять `engine.language` «на лету» перед каждым вызовом `recognize()`.

---

## Шаг 2: Загрузка многостраничного TIFF, который нужно **конвертировать TIFF в текст**

TIFF может содержать несколько кадров — каждый кадр воспринимается как отдельная страница. OCR‑библиотека абстрагирует это за нас, поэтому достаточно указать путь к файлу.

```python
# Path to your multi‑page TIFF
tiff_path = "YOUR_DIRECTORY/french-scans.tif"

# Load the file; the engine now knows how many pages it contains
engine.load_from_file(tiff_path)
```

**Внимание к граничным случаям:**  
Если путь к файлу неверен или TIFF повреждён, метод `load_from_file` выбросит исключение. Для продакшн‑кода оберните его в блок `try/except`:

```python
try:
    engine.load_from_file(tiff_path)
except Exception as e:
    print(f"Failed to load TIFF: {e}")
    raise
```

---

## Шаг 3: Запуск OCR для всего документа — ядро **извлечения текста из TIFF**

Теперь позволим движку выполнить свою магию. Вызов `recognize()` обрабатывает все страницы сразу и возвращает богатый объект результата.

```python
# Perform OCR on all pages at once
multi_result = engine.recognize()
```

**Что происходит «под капотом»?**  
Движок проходит по каждому кадру, применяет предобработку (выравнивание, бинаризацию), запускает нейронную сеть и собирает вывод. Поскольку мы вызвали `recognize()` один раз, библиотека может делить ресурсы между страницами, что быстрее, чем ручной цикл.

---

## Шаг 4: Извлечение распознанного текста из JSON‑результата — **конвертировать TIFF в текст** постранично

Объект результата можно сериализовать в JSON. В этом JSON‑файле будет массив `pages`, каждый элемент которого содержит поле `text`.

```python
# Convert the result to a Python dict (JSON-like)
result_dict = multi_result.to_json()

# Extract the list of pages
pages = result_dict["pages"]
```

Теперь у нас есть чистый список Python, где каждый элемент соответствует OCR‑выводу отдельной страницы.

---

## Шаг 5: Вывод или сохранение текста для каждой страницы — заключительный шаг **извлечения текста из TIFF**

Пройдемся по страницам и выведем извлечённый текст. При желании можно записать каждую страницу в отдельный файл `.txt`.

```python
for i, page in enumerate(pages, start=1):
    print(f"--- Page {i} ---")
    print(page["text"])
    print()  # Blank line for readability
```

### Ожидаемый вывод (пример)

```
--- Page 1 ---
Bonjour, ceci est un exemple de texte extrait d'une image TIFF.

--- Page 2 ---
Le deuxième page contient davantage d'informations en français.
```

Если OCR прошёл успешно, вы увидите чистый блок французских предложений для каждой страницы. Если появляются «мусорные» символы, проверьте настройку языка или попробуйте увеличить разрешение изображения перед OCR.

---

## Как справиться с распространёнными проблемами при **конвертации TIFF в текст**

| Проблема | Почему происходит | Быстрое решение |
|----------|-------------------|-----------------|
| **Пустой массив `pages`** | TIFF не был загружен корректно или не содержит кадров. | Проверьте путь к файлу и убедитесь, что TIFF не является одностраничным PNG, переименованным в TIFF. |
| **Непонятные символы** | Несоответствие языка или низкое качество изображения. | Установите правильный `engine.language` и выполните предобработку (например, увеличьте DPI). |
| **Переполнение памяти при больших TIFF** | Одновременная загрузка всех страниц требует много ОЗУ. | Обрабатывайте порциями: загружайте один кадр, распознавайте, освобождайте память, затем переходите к следующему. |
| **Ошибки Unicode при выводе** | Кодировка консоли не поддерживает акцентированные символы. | Используйте `print(page["text"].encode('utf-8').decode('utf-8'))` или настройте терминал на UTF‑8. |

---

## Расширение скрипта: от **извлечения текста из TIFF** к пакетной обработке

Теперь, когда у вас есть надёжная база, рассмотрите следующие шаги:

1. **Пакетное преобразование** — оберните весь процесс в функцию `def ocr_tiff(path):` и пройдитесь по каталогу с TIFF‑файлами.
2. **Сохранение в файлы** — вместо печати записывайте текст каждой страницы в `page_{i}.txt` или объединяйте всё в один документ.
3. **Альтернативные OCR‑движки** — если нужна более высокая точность, замените `ocr.OcrEngine()` на Tesseract (`pytesseract`) или Azure Cognitive Services — логика «извлечения текста из TIFF» останется той же.
4. **Постобработка** — применяйте проверку орфографии, определение языка или очистку с помощью регулярных выражений, чтобы улучшить сырой OCR‑вывод.

---

## Полный готовый к запуску скрипт

Ниже представлен полностью готовый код, который можно скопировать и вставить. В нём есть базовая обработка ошибок и опциональное сохранение текста каждой страницы в отдельные файлы.

```python
import ocr  # Adjust import based on your OCR library
import os

def extract_text_from_tiff(tiff_path: str, output_dir: str = None) -> list:
    """
    Loads a multi‑page TIFF, runs OCR, and returns a list of strings,
    one per page. Optionally saves each page to a .txt file.
    """
    # Initialize engine and set language
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.FRENCH

    # Load the TIFF file
    try:
        engine.load_from_file(tiff_path)
    except Exception as e:
        raise RuntimeError(f"Unable to load {tiff_path}: {e}")

    # Run OCR on all pages
    multi_result = engine.recognize()

    # Parse JSON result
    pages = multi_result.to_json()["pages"]
    texts = [page["text"] for page in pages]

    # If an output directory is provided, write each page to a file
    if output_dir:
        os.makedirs(output_dir, exist_ok=True)
        for i, text in enumerate(texts, start=1):
            file_path = os.path.join(output_dir, f"page_{i}.txt")
            with open(file_path, "w", encoding="utf-8") as f:
                f.write(text)

    return texts

if __name__ == "__main__":
    # Example usage – replace with your actual TIFF path
    tiff_file = "YOUR_DIRECTORY/french-scans.tif"
    # Optional: where to store per‑page text files
    out_folder = "extracted_pages"

    page_texts = extract_text_from_tiff(tiff_file, out_folder)

    for i, txt in enumerate(page_texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()
```

Запустите скрипт, укажите путь к `tiff_file`, и наблюдайте, как консоль заполняется чистыми французскими предложениями. Если задали `out_folder`, вы также найдёте серию файлов `page_#.txt`, готовых к дальнейшей обработке.

---

## Заключение

Мы только что **извлекли текст из TIFF**‑файлов с помощью простого Python‑OCR‑рабочего процесса, и теперь вы знаете, как **конвертировать TIFF в текст** надёжно. От инициализации движка с правильным языком до обхода JSON‑результата каждой страницы — каждый шаг был объяснён с «почему», чтобы вы могли адаптировать схему под другие языки, форматы изображений или крупные пакетные задачи.

Что дальше? Попробуйте заменить бекенд OCR на Tesseract, поэкспериментируйте с различными языковыми пакетами или интегрируйте вывод в поисковую базу данных. Возможности безграничны, когда вы умеете превращать отсканированные изображения в индексируемый текст.

Если возникли вопросы или есть идеи по улучшению, оставляйте комментарии. Приятного кодинга!


## Что изучать дальше?


Следующие руководства охватывают тесно связанные темы, расширяющие техники, продемонстрированные в этом пособии. Каждый ресурс содержит полностью рабочие примеры кода с пошаговыми объяснениями, чтобы вы могли освоить дополнительные возможности API и исследовать альтернативные подходы в своих проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Convert Image to Text – Perform OCR on Image from URL](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}