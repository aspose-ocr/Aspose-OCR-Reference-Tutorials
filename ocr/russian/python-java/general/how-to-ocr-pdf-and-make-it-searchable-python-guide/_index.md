---
category: general
date: 2026-01-12
description: Изучите, как выполнять OCR PDF в Python и быстро делать PDF доступным
  для поиска. Конвертируйте отсканированный PDF, извлекайте текст из PDF и применяйте
  OCR к отсканированному PDF с помощью Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: ru
og_description: Как выполнить OCR PDF в Python? Этот пошаговый учебник покажет, как
  преобразовать отсканированные PDF‑файлы в поисковые PDF и извлечь текст с помощью
  Aspose OCR.
og_title: Как выполнить OCR PDF и сделать его поисковым – руководство по Python
tags:
- OCR
- Python
- PDF processing
title: Как выполнить OCR PDF и сделать его поисковым – руководство по Python
url: /ru/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Как распознать PDF и сделать его поисковым – Руководство на Python

Когда‑нибудь задумывались **как распознать PDF** файлы, не тратя состояние на коммерческое программное обеспечение? Вы не одиноки. Многие разработчики сталкиваются с проблемой, когда нужно превратить отсканированный контракт, счёт‑фактуру или любой PDF, основанный на изображениях, в поисковый документ. Хорошая новость? С несколькими строками кода на Python и Aspose OCR вы можете конвертировать отсканированный PDF, извлечь текст из PDF и, наконец, сделать PDF поисковым за считанные минуты.

В этом руководстве мы пройдём всё, что вам понадобится: от установки библиотеки, настройки языка, обработки отсканированного PDF до сохранения результата в виде поискового PDF, содержащего как оригинальное изображение, так и скрытый текстовый слой. К концу вы получите переиспользуемый скрипт, который можно добавить в любой проект — без ручного копирования и вставки.

---

## Что понадобится

- **Python 3.8+** (код работает на 3.9, 3.10 и новее)
- Действующая лицензия **Aspose OCR for Python** (бесплатная пробная версия подходит для экспериментов)
- Отсканированный PDF‑файл (например, `scanned_contract.pdf`), который вы хотите сделать поисковым
- Базовые навыки работы с командной строкой и виртуальными окружениями (опционально, но рекомендуется)

> **Pro tip:** Если у вас ещё нет лицензии, зарегистрируйтесь на 30‑дневную пробную версию на сайте Aspose; пробная версия полностью функциональна для целей разработки.

---

## Как распознать PDF с помощью Aspose OCR (Primary Keyword in H2)

Первый шаг — получить правильный пакет. Aspose OCR предоставляет чистый, высокоуровневый API, который скрывает детали низкоуровневой обработки изображений.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

После установки пакета вы можете приступить к написанию скрипта.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Почему нужно задавать язык?**  
> Точность OCR сильно зависит от языковой модели. Явно указав движку, что ожидается английский текст, вы уменьшаете количество ложных срабатываний и ускоряете обработку.

---

## Шаг 2: Конвертировать отсканированный PDF в поисковый PDF

Теперь, когда движок готов, укажите ему ваш отсканированный документ. Метод `process_pdf` возвращает объект `PdfResult`, содержащий как оригинальные данные изображения, так и распознанный текст.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Если вам нужно **конвертировать отсканированные PDF** файлы пакетно, просто пройдитесь по каталогу и вызовите `process_pdf` для каждого файла. Движок обрабатывает многостраничные PDF «из коробки».

---

## Шаг 3: Сохранить результат как поисковый PDF (Make PDF Searchable)

Последний элемент головоломки — сохранить поисковую версию. Aspose OCR делает это в одну строку:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

Когда вы откроете `contract_searchable.pdf` в любом PDF‑просмотрщике, вы увидите оригинальное отсканированное изображение, но теперь сможете **искать любое слово**, которое распознал движок OCR. Скрытый текстовый слой невидим глазу, но полностью индексируем.

---

### Полный скрипт – готов к запуску

Ниже приведён полностью готовый к выполнению пример. Скопируйте‑вставьте его в файл с именем `make_searchable.py` и при необходимости поправьте пути под свою среду.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Ожидаемый вывод:**  
Запуск скрипта печатает строку‑подтверждение и создаёт `contract_searchable.pdf`. Откройте файл, нажмите `Ctrl + F` и введите любое слово, присутствующее в оригинальном отсканированном изображении — вы сразу увидите совпадения.

---

## Часто задаваемые вопросы и особые случаи

### 1. Что если PDF содержит несколько языков?

Можно передать список языков движку:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR попытается распознать текст на обоих языках в пределах одной страницы.

### 2. Как работать с низкокачественными сканами?

Если исходные изображения имеют менее 150 dpi, точность OCR может пострадать. Предобработайте PDF с помощью инструмента вроде `pdfimages`, извлеките страницы, увеличьте их с помощью Pillow и передайте полученные изображения обратно в `process_pdf`.

### 3. Можно ли извлечь чистый текст без создания поискового PDF?

Конечно. Объект `PdfResult` предоставляет свойство `text`:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Это решает задачу **extract text pdf**, когда нужен только сырой набор символов.

### 4. Есть ли способ пакетно обработать папку PDF?

Да — оберните функцию `ocr_to_searchable` простым циклом:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Теперь вы можете **конвертировать отсканированные pdf** файлы массово одной командой.

---

## Советы по производительности

- **Повторное использование движка**: Создание нового `OcrEngine` для каждого файла добавляет накладные расходы. Инстанцируйте его один раз и переиспользуйте при множественных вызовах.
- **Параллельная обработка**: Для больших пакетов рассмотрите `concurrent.futures.ThreadPoolExecutor` — Aspose OCR потокобезопасен для операций только чтения.
- **Управление памятью**: При обработке очень больших PDF (сотни страниц) вызывайте `gc.collect()` после каждого файла, чтобы освободить память.

---

## Заключение

Мы рассмотрели, **как распознать PDF** файлы на Python, превратили эти сканы в **поисковые PDF** и даже показали, как **извлечь текст PDF** напрямую. С Aspose OCR вы получаете надёжный движок, который справляется с многостраничными документами, несколькими языками и высокой точностью распознавания — всё это в паре строк кода.

Попробуйте на своих контрактах, счётах или архивных научных работах. Овладев базовыми навыками, экспериментируйте с продвинутыми возможностями — пользовательскими словарями, предобработкой изображений или интеграцией результата в полнотекстовый поисковый индекс, например Elasticsearch.

Есть дополнительные вопросы о **ocr scanned pdf python** или нужна помощь с трудным сканом? Оставляйте комментарий ниже, и счастливого кодинга!

--- 

![пример как распознать pdf](image-placeholder.png){alt="пример как распознать pdf"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}