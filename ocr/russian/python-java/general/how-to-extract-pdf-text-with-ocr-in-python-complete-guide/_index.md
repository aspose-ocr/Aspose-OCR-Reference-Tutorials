---
category: general
date: 2026-06-19
description: Как извлечь PDF с помощью OCR в Python – пошаговое руководство, охватывающее
  извлечение текста из PDF, распознавание текста на изображении и пример OCR на Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: ru
og_description: Как извлекать PDF с помощью OCR в Python. Узнайте, как извлекать текст
  из PDF, распознавать текст на изображении, и посмотрите полный пример OCR на Python.
og_title: Как извлечь текст из PDF с помощью OCR в Python – Полный учебник
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Как извлечь текст из PDF с помощью OCR в Python — полное руководство
url: /ru/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как извлечь текст из PDF с помощью OCR в Python – Полное руководство

Когда‑нибудь задавались вопросом **как извлечь содержимое PDF**, если файл представляет собой просто отсканированное изображение? Вы не одиноки. Во многих реальных проектах — контракты, счета‑фактуры, исторические архивы — получаемый PDF не содержит выделяемого текста. Хорошая новость? Пара строк кода на Python могут превратить такие страницы‑изображения в поисковый, редактируемый текст.

В этом руководстве мы пройдём практический **OCR Python example**, который читает PDF, рендерит первую страницу как изображение, а затем **извлекает текст из PDF** с помощью OCR‑движка. К концу вы точно будете знать, как **читать PDF с OCR**, почему каждый шаг важен и как адаптировать код для многостраничных документов или разных языков.

## Что вы узнаете

- Установить и настроить надёжную OCR‑библиотеку для Python.  
- Преобразовать страницы PDF в изображения, подходящие для OCR.  
- **Распознавать текст с изображения** и получать чистые Unicode‑строки.  
- Распространённые подводные камни (PDF низкого разрешения, повернутые страницы) и как их избежать.  
- Расширить скрипт для обработки нескольких страниц или пакетной обработки.

**Prerequisites**: Python 3.8+, pip и базовое понимание виртуальных окружений. Предыдущий опыт работы с OCR не требуется — просто следуйте инструкциям.

---

## ## Как извлечь текст из PDF с помощью OCR в Python

Этот заголовок H2 содержит наш основной ключевой запрос именно там, где поисковые системы любят его видеть. Переходим сразу к коду.

### Шаг 1 – Установите необходимые пакеты

Сначала нам нужен OCR‑движок. В примере ниже используется популярный пакет **ocr** (тонкая обёртка над Tesseract). Если вы предпочитаете другой бекенд, концепции остаются теми же.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Совет:** В Linux также понадобится бинарный файл Tesseract: `sudo apt-get install tesseract-ocr`. Пользователи macOS могут установить его через Homebrew: `brew install tesseract`.

### Шаг 2 – Инициализируйте OCR‑движок и задайте язык

Теперь запускаем движок и указываем искать английские символы. Вы можете заменить `ocr.Language.English` на любой поддерживаемый код языка.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Почему это важно:** Указание языка существенно повышает точность, поскольку движок может применять языковые словари и модели символов.

### Шаг 3 – Загрузите страницу PDF как изображение

OCR работает с растровыми изображениями, а не с объектами PDF. Помощник `ocr.Image.from_pdf` рендерит выбранную страницу в bitmap. Измените `page_number` для других страниц (нумерация с нуля).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Особый случай:** Если PDF содержит векторную графику вместо отсканированных изображений, вы можете получить чёткое рендеринг. Для сканов низкого разрешения рассмотрите увеличение DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Шаг 4 – Распознавайте текст с отрендеренного изображения

Это сердце **ocr python example**. Движок обрабатывает bitmap и возвращает объект, содержащий извлечённую строку.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

Атрибут `ocr_result.text` содержит обычный текстовый вывод, сохраняющий разрывы строк там, где это возможно.

### Шаг 5 – Выведите или сохраните извлечённый текст

Наконец, выводим результат. В реальном приложении вы, вероятно, запишете его в файл или базу данных.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Запуск скрипта должен отобразить что‑то вроде:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Это полный **extract text from pdf** рабочий процесс с использованием OCR.

---

## ## Распознавать текст с изображения – Улучшение точности

Если вам нужен только **recognize text from image** (например, JPEG‑чек), можно пропустить шаг конвертации PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Советы для лучшего результата:**

- **Предобработать** изображение: перевести в градации серого, применить пороговую обработку или исправить наклон. Pillow делает это легко.  
- **Увеличить DPI** при рендеринге PDF: более высокое разрешение даёт OCR‑движку больше деталей.  
- **Включить конфигурацию OCR‑движка** для сегментации страниц (`ocr_engine.config = "--psm 6"` для однородных блоков).

---

## ## Читать PDF с OCR – Обработка нескольких страниц

Большинство контрактов охватывают несколько страниц. Перебор каждой страницы прост:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Эта функция **reads PDF with OCR**, конкатенирует вывод и вставляет чёткий маркер разрыва страницы. Затем вы можете передать `full_text` в поисковый индекс или сохранить как файл `.txt`.

---

## ## Распространённые проблемы и как их исправить

| Симптом | Вероятная причина | Решение |
|---------|-------------------|---------|
| Искажённые символы, много `?` | Неправильный язык или отсутствие файлов данных языка | Установите правильный языковой пакет Tesseract (`tesseract-ocr-<lang>`) и задайте `ocr_engine.language`. |
| Пропущенные строки или усечённые слова | Низкое DPI (менее 150) | Рендерите PDF с 300 DPI или выше (`dpi=300`). |
| Текст повернут или вверх‑вниз | Сканированная страница не выровнена | Используйте `ocr.Image.deskew(page_image)` перед распознаванием. |
| Медленная обработка больших PDF | Последовательная обработка страниц в одном потоке | Параллелизуйте с `concurrent.futures.ThreadPoolExecutor`. |

---

## ## Расширение OCR Python Example

- **Экспорт в PDF/A**: После извлечения вы можете встроить текст обратно в поисковый PDF с помощью `reportlab` или `pypdf2`.  
- **Определение языка**: Используйте `langdetect` на выводе OCR, чтобы динамически переключать `ocr_engine.language`.  
- **Пакетная обработка**: Пройдитесь по директории с `os.listdir` и примените `extract_all_pages` к каждому файлу.

---

## ## Ожидаемый вывод и проверка

Когда вы запустите скрипт на чистом скане на английском, вы должны увидеть аккуратный блок текста с правильной пунктуацией. Проверьте, выполнив:

1. Сравнение нескольких строк с оригинальным отсканированным изображением.  
2. Запуск простого подсчёта слов (`len(ocr_result.text.split())`), чтобы убедиться, что вывод не пустой.  
3. При желании, передайте результат в проверщик орфографии, например `pyspellchecker`, чтобы обнаружить ошибки OCR.

---

## Заключение

Мы рассмотрели **как извлечь PDF**, когда традиционный парсинг не работает, продемонстрировали полный **ocr python example** и объяснили, как **recognize text from image** и **read PDF with OCR** для одно‑ и много‑страничных сценариев. С помощью приведённых выше фрагментов кода вы теперь можете превратить любой отсканированный PDF в поисковый, редактируемый текст — без ручного перепечатывания.

Следующие шаги? Попробуйте переключить язык на испанский (`ocr.Language.Spanish`) или поэкспериментировать с методами предобработки изображений для повышения точности. Если вы создаёте систему управления документами, рассмотрите индексацию извлечённого текста в Elasticsearch для молниеносного поиска.

Есть вопросы или столкнулись с причудливым PDF? Оставьте комментарий, и счастливого кодинга!  

![Как извлечь PDF с помощью OCR в Python](image.png "Как извлечь PDF с помощью OCR в Python")


## Что вам стоит изучить дальше?


Следующие руководства охватывают тесно связанные темы, которые развивают техники, продемонстрированные в этом гайде. Каждый ресурс включает полностью работающие примеры кода с пошаговыми объяснениями, чтобы помочь вам освоить дополнительные возможности API и исследовать альтернативные подходы в собственных проектах.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}